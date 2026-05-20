---
title: "Unit 4: Data Retrieval, Security & Platforms"
description: "WSN Routing/Transport layers, Security (IDS, Key Management), TinyOS/nesC Platforms, and Sensor Network Simulators"
author: "Deepak Modi"
date: "2026-05-10"
pdfUrl: ""
---

## Syllabus:

Data Retrieval in Sensor Networks: Routing layer, Transport layer, High-level application layer support; Adapting to the inherent dynamic nature of WSNs; Sensor Networks and mobile robots.

Security: Security in Ad Hoc networks, Key management, Secure routing, Cooperation in MANETs, Intrusion Detection systems.

Sensor Network Platforms and Tools: Sensor Network Hardware, Berkeley motes, Sensor Network Programming Challenges, Node-Level Software Platforms - Operating System: TinyOS – Imperative Language: nesC, Dataflow style language: TinyGALS, Node-Level Simulators, ns2 and its sensor network extension, TOSSIM.

---

## 🎯 PYQ Analysis for Unit 4

### **High Priority Topics** (15 marks questions)

1. **TinyOS — Features, Limitations & Resource-Constrained Support** — (May 2025: 15, Dec 2025: 15)
2. **Intrusion Detection System + Network Simulator** — (May 2023: 15, Dec 2023: 15, Jul 2022: 15)
3. **Dynamic Nature of WSNs + Secure Routing** — (May 2023: 15)
4. **Cooperation in MANETs + Sensor Network Tools** — (Jul 2022: 15)
5. **Intrusion Detection System + Sensor Networks & Mobile Robots** — (Jul 2022: 15)
6. **QoS in WSN + Transport Layer Issues** — (Dec 2023: 7+8=15)
7. **Routing Issues in WSN + Localization** — (Dec 2023: 7+8=15)

### **Medium Priority Topics** (Short answers / 7–8 marks)

1. **Dynamic Nature of WSN** — Dec 2025 (2.5 marks)
2. **Intrusion Detection System** — Dec 2025 (2.5 marks)
3. **Passive Attacks** — Dec 2025 (2.5 marks)
4. **TinyOS** — May 2023 (2.5 marks)
5. **Tiny GALS** — May 2025 (3 marks)
6. **Key Management** — May 2023 (2.5 marks)
7. **Secure Routing** — Jul 2022 (2.5 marks)
8. **Berkeley Motes** — Jul 2022 (2.5 marks)
9. **NS-2 Functionalities** — May 2025, Dec 2025 (8 marks)
10. **TOSSIM Simulator** — May 2025 (7 marks)
11. **Security Challenges in WSN (four major)** — Dec 2025 (7 marks)

---

## **Section 1: Routing Layer in Sensor Networks**

> PYQ: Appraise the issues related to routing in wireless sensor networks. (Dec 2023, 7 marks)

### **1.1 Why WSN Routing is Different**

Traditional routing (IP-based) assumes globally unique addresses, fixed topology, and abundant resources. WSN routing is fundamentally different due to:

| Factor | Traditional Network | Wireless Sensor Network |
|--------|---------------------|------------------------|
| Addressing | Global IP addresses | No global IDs (data-centric) |
| Energy | Power from grid | Battery-constrained |
| Topology | Relatively stable | Highly dynamic (node failures) |
| Data model | Point-to-point | Many-to-one (to sink) |
| Scale | Thousands of nodes | Potentially millions |
| Redundancy | Low | High (many sensors measure same area) |

**Key challenges:**
- **Energy efficiency** is the primary design goal — routing must minimize energy consumption
- **No global addressing** — nodes identified by location or data attributes, not IP
- **Data-centric** — queries and interest target data attributes ("temperature > 50°C") not node IDs
- **In-network processing** — aggregation and filtering happen inside the network, not just at sink
- **Lossy links** — wireless channel unreliable, need to handle retransmissions

---

### **1.2 Data-Centric vs Address-Centric Routing**

**Address-Centric Routing (traditional):**
- Packets sent from source address to destination address
- Each node has unique ID
- Routes established between specific node pairs
- Problem: in WSN, you don't care WHICH node measured data, just WHAT was measured

**Data-Centric Routing:**
- Queries expressed in terms of data attributes (e.g., "find all nodes with humidity > 70%")
- Nodes process queries and send matching data toward sink
- Enables in-network aggregation (combine readings from nearby nodes)
- Eliminates redundant transmissions of similar data
- Example: Instead of asking node #47 for temp, ask "any node in sector A with temp > 30°C"

---

### **1.3 Flooding and Gossiping**

#### **Flooding**
The simplest routing mechanism — every node that receives a packet retransmits it to all neighbors.

```
        Source
          |
     [Broadcast]
    /     |     \
  N1      N2     N3
  /\      /\     /\
N4 N5  N6 N7  N8 N9   ... until packet reaches Sink
```

**Advantages:**
✅ No route discovery or maintenance required
✅ Simple to implement
✅ Robust — packets reach destination via multiple paths

**Disadvantages:**
❌ **Implosion**: A node receives duplicate copies of same data from multiple neighbors
❌ **Overlap**: Nodes in same region send redundant identical data
❌ **Blindness**: No awareness of energy levels — routes not energy-optimized
❌ **Broadcast storm**: Exponential packet explosion

#### **Gossiping**
A variant of flooding — instead of broadcasting to ALL neighbors, a node randomly selects ONE neighbor to forward the packet.

✅ Reduces broadcast storm problem
❌ Slow propagation — packet may take long winding path
❌ No guarantee of delivery (packet may keep bouncing)

---

### **1.4 Directed Diffusion**

**Directed Diffusion** is a data-centric, energy-efficient routing protocol that operates in three phases.

> **Analogy**: Think of it like a grocery store putting a "Wanted" poster on the wall (interest). Suppliers who have matching items bring them in (data flows in). The store then picks its best supplier and places a regular order with them (reinforcement).

#### **Phase 1: Interest Propagation**

The sink broadcasts an **interest** — a description of data it wants (e.g., "give me temperature readings from this region every 30 seconds"). Each intermediate node stores this interest in a **gradient** table, recording what data is needed and which direction to send it.

```
         SINK
          |
    [Interest propagates]
    /      |      \
   A       B       C
  /|\     /|\     /|\
 D E F   G H I   J K L    (all nodes receive interest)
```

- Multiple gradients may exist from different paths (one per neighboring direction)

#### **Phase 2: Data Propagation**

Once interest is established, source nodes that match the query begin sending **data** along available gradients (initially low-rate exploratory data).

```
Source (node D) has temperature data:
D --> A --> SINK   (one possible path)
D --> E --> B --> SINK   (another path — exploratory)
```

Data flows from source toward sink along gradient paths. Initially ALL paths carry low-rate data.

#### **Phase 3: Reinforcement (Path Optimization)**

The sink or intermediate nodes **reinforce** the best path (highest quality, lowest latency, most energy-efficient) by sending reinforcement back along that path.

```
SINK detects: path D-->A-->SINK is best (low latency)
SINK sends reinforcement to A (increase data rate on this path)
A sends reinforcement to D
Now D sends full-rate data only via D-->A-->SINK
Other paths suppressed
```

```
Full Directed Diffusion Flow:

Step 1: Interest Propagation (SINK → all nodes)
  SINK ---interest---> A,B,C ---interest---> D,E,F,G,...

Step 2: Gradient Setup (at each node)
  Each node records gradient entry:
  [data_type, rate, direction_to_sink]

Step 3: Low-rate Data Flow (sources → SINK via all paths)
  D ---data---> A ---data---> SINK
  D ---data---> E ---data---> B ---data---> SINK

Step 4: Reinforcement (SINK reinforces best path)
  SINK ---reinforce---> A ---reinforce---> D

Step 5: High-rate Data (only via reinforced path)
  D ===(high rate)===> A ===(high rate)===> SINK
```

**Advantages:**
✅ Energy efficient — path reinforcement eliminates redundant transmissions
✅ Data-centric — works without global addressing
✅ In-network processing (aggregation at intermediate nodes)
✅ Robust to failures — can reinforce alternate path

**Disadvantages:**
❌ Not suitable for continuous monitoring (designed for query-based)
❌ Overhead of interest propagation phase
❌ Complex implementation

---

### **1.5 SPIN (Sensor Protocol for Information via Negotiation)**

**SPIN** addresses the implosion and overlap problems of flooding using a **negotiation-based** approach. Before sending actual data, nodes first advertise what they have and only send data if a neighbor needs it.

> **Analogy**: Instead of photocopying and handing flyers to everyone on the street (flooding), you put a notice on a board — "I have the temperature reading from sector A." Only people who don't already have it come and ask you for a copy.

#### **Three Message Types:**

| Message | Purpose |
|---------|---------|
| **ADV** | Advertisement — "I have new data X" |
| **REQ** | Request — "Please send me data X" |
| **DATA** | Actual data payload |

#### **SPIN Protocol Flow:**

```
Step 1: Node A has new data
A --[ADV: "I have temp_data_7"]--> Neighbors (B, C, D)

Step 2: B already has temp_data_7 (ignores ADV)
        C doesn't have it → C sends REQ
C --[REQ: "Send temp_data_7"]--> A

Step 3: A sends DATA only to C
A --[DATA: temp_data_7]--> C

Step 4: C now has data, advertises to its neighbors
C --[ADV: "I have temp_data_7"]--> Neighbors (D, E, F)

... process repeats
```

```
SPIN Negotiation Diagram:

    A(has data)           B(already has data)
         |                        
    ADV ---> B  (B ignores - already has it)
    ADV ---> C  (C wants it - sends REQ)
    ADV ---> D  (D wants it - sends REQ)
         |
    DATA --> C
    DATA --> D
         |
    C now advertises to its neighbors...
```

**SPIN-BC** (Broadcast Channel variant):
- ADV broadcast to all neighbors
- Interested nodes send REQ
- DATA sent (broadcast or unicast)

**SPIN-EC** (Energy Conserving variant):
- Nodes participate only if they have sufficient energy
- Resource-aware negotiation

**Advantages:**
✅ Eliminates implosion (negotiation ensures no duplicate DATA)
✅ Eliminates overlap (metadata negotiation prevents redundant sends)
✅ Adaptive (handles node failures — other nodes still propagate data)

**Disadvantages:**
❌ Does not guarantee delivery (if a node has no interested neighbors, data is lost)
❌ ADV/REQ overhead for every data item
❌ Does not compute energy-efficient paths

---

### **1.6 Hierarchical Routing: LEACH**

**LEACH (Low Energy Adaptive Clustering Hierarchy)** organizes sensor nodes into clusters. Each cluster has a **Cluster Head (CH)** that aggregates data from cluster members and forwards to sink.

#### **Key Idea:**
Instead of ALL nodes sending data to sink (wasting energy on long transmissions), only cluster heads communicate directly with sink. Regular nodes send short-range transmissions to their local CH.

#### **Cluster Head Selection:**

> **Analogy**: Think of a class project where every student flips a coin each round. The coin is weighted — students who haven't been team leader recently have a higher chance of winning. This way, leadership rotates fairly over time.

Each node independently decides to be a CH by a **probabilistic coin flip**:
- Each node has a target probability p of being a CH (e.g., 5% of nodes should be CHs)
- Nodes that were recently a CH are excluded (to spread energy load)
- Remaining eligible nodes flip a weighted coin — the longer since they were last CH, the higher their chance
- If selected, node broadcasts "I am a Cluster Head"

#### **LEACH Rounds:**

```
LEACH Protocol - Each Round:

SETUP PHASE:
1. Nodes decide CH status (probabilistic)
2. CHs broadcast advertisement
3. Non-CH nodes join nearest CH (TDMA schedule assigned)

+--Setup Phase--+--Steady State Phase (data transfer)--+
|               |                                       |
| CH Election   | Slot1 Slot2 Slot3 ... (TDMA frame)   |
| Advertisement |  N1 -->CH  N2-->CH  N3-->CH ...       |
| Cluster Join  |  CH aggregates & forwards to SINK     |
+---------------+---------------------------------------+
     (short)              (long, repeat many times)
```

#### **LEACH Architecture Diagram:**

```
        [SINK / Base Station]
               ^
               | (long-range radio)
               |
    +----------+----------+
    |                     |
  [CH1]                 [CH2]
  /  |  \              /  |  \
N1  N2   N3          N4  N5   N6     (short-range to CH)
    
Cluster 1          Cluster 2

Nodes N1,N2,N3 send short-range to CH1
CH1 aggregates (avg/max/min) and sends compressed data to SINK
```

#### **LEACH Phases:**

1. **Advertisement Phase**: CHs broadcast "I am a cluster head" using CSMA
2. **Cluster Formation**: Non-CH nodes choose closest CH (strongest signal), send join request
3. **Schedule Creation**: CH creates TDMA schedule for cluster members
4. **Data Transmission**: Members send in their time slot; CH aggregates and forwards to sink
5. **Round restarts**: New CH election begins (distributes energy load)

**Advantages:**
✅ Energy load distributed (rotation of CH role)
✅ In-network aggregation (CH compresses data)
✅ Localized coordination (scalable)
✅ TDMA within cluster (no collisions)

**Disadvantages:**
❌ Single-hop to sink from CH — doesn't scale for large areas
❌ CH still far from sink consumes heavy energy
❌ Random CH selection may result in poor CH placement
❌ Multi-hop LEACH variants (LEACH-C, PEGASIS) needed for larger deployments

---

### **1.7 Comparison Table: Routing Protocols**

| Feature | Flooding | Directed Diffusion | SPIN | LEACH |
|---------|----------|-------------------|------|-------|
| **Addressing** | Broadcast | Data-centric | Data-centric | Cluster-based |
| **Energy Efficiency** | ❌ Very poor | ✅ Good | ✅ Good | ✅ Very good |
| **Implosion** | ❌ Yes | ✅ No | ✅ No | ✅ No |
| **Overhead** | Low | Medium (gradients) | Medium (ADV/REQ) | Medium (setup) |
| **Aggregation** | ❌ No | ✅ Yes | ❌ Limited | ✅ Yes (at CH) |
| **Topology** | Flat | Flat | Flat | Hierarchical |
| **Fault Tolerance** | ✅ High | ✅ Good | ✅ Good | ❌ CH failure |
| **Scalability** | ❌ Poor | ✅ Good | ✅ Good | ✅ Good |
| **Path Optimization** | ❌ No | ✅ Reinforcement | ❌ No | Partial |

---

## **Section 2: Transport Layer in Sensor Networks**

> PYQ: Appraise the QoS related measures in wireless sensor networks. (Dec 2023, 7 marks)  
> PYQ: Outline the issues related to the transport layer in wireless sensor networks. (Dec 2023, 8 marks)  
> PYQ: What is Quality of Service (QOS)? (Dec 2023, 2.5 marks)

### **2.1 Why TCP is NOT Suitable for WSN**

TCP was designed for wired networks with reliable links and stable topology. In WSNs:

| TCP Assumption | WSN Reality |
|---------------|-------------|
| Packet loss = congestion | Packet loss often due to wireless channel noise |
| End-to-end connections | Sensor data flows from many sources to ONE sink |
| Reliable delivery needed everywhere | Only event data reaching sink matters |
| Symmetric traffic | Mostly asymmetric (many sensors → one sink) |
| ACK-based reliability | ACKs waste energy on energy-constrained nodes |
| Connection setup overhead | Too heavy for tiny sensor packets |
| Large window sizes | Not meaningful for small data bursts |

**TCP Misbehavior in WSN:**
- Wireless loss triggers congestion window reduction → unnecessary throttling
- End-to-end retransmissions bypass in-network processing
- Per-connection state is expensive
- Header overhead is too large for small sensor payloads

---

### **2.2 Transport Layer Requirements in WSN**

1. **Reliability**: Data should reach sink (event reliability), or program code should reach nodes (node reliability)
2. **Congestion Control**: Detect and avoid congestion in the network without TCP's false triggers
3. **Energy Efficiency**: Minimize retransmissions, avoid excessive ACKs
4. **Scalability**: Handle large numbers of nodes
5. **Directional Awareness**: Upward flow (sensor→sink) vs downward flow (sink→sensor) have different requirements

---

### **2.3 PSFQ (Pump Slowly Fetch Quickly)**

**PSFQ** is designed for **downward reliability** — reliably delivering data/code from sink to sensor nodes (e.g., firmware updates, query injection).

> **Analogy**: Like downloading a large file slowly so the network doesn't get overwhelmed — but if you miss a chunk, you immediately and aggressively ask your nearby peer for just that missing piece, not the whole file again.

#### **Core Principle:**
- **Pump Slowly**: Sink injects data at a slow, controlled rate (to avoid overwhelming nodes)
- **Fetch Quickly**: If a node misses a segment, it immediately and aggressively fetches it from neighbors

#### **Three Operations:**

| Operation | Description |
|-----------|-------------|
| **Pump** | Sink sends data segments slowly (with delays between segments) |
| **Fetch** | If node detects gap in sequence, NAK sent to upstream neighbor, fetch missing segment |
| **Report** | Optional: nodes report delivery status back to sink |

```
PSFQ Operation:

SINK: ----[Seg1]---[Seg2]---[Seg3]---[Seg4]---> (slow injection)
                                      
Node A receives Seg1, Seg2, Seg4 (misses Seg3)
Node A detects gap: Seq3 missing
Node A sends NACK to upstream neighbor B
B has Seg3 → B sends Seg3 to A quickly
A reconstructs complete data: Seg1 Seg2 Seg3 Seg4 ✅
```

**Key Features:**
- Local recovery (only nearest node with segment helps, not all the way to sink)
- Each node caches recently received segments for a window of time
- Hop-by-hop reliability (not end-to-end)
- Designed for **infrequent, critical** transmissions (code updates, configuration)

✅ Energy efficient (local recovery avoids long retransmission paths)
✅ Reliable delivery for sink-to-node direction
❌ Not suitable for real-time or streaming sensor data

---

### **2.4 ESRT (Event-to-Sink Reliable Transport)**

**ESRT** provides **upward reliability** — reliable delivery of event data from sensors to the sink.

> **Analogy**: Like a call center manager watching the queue. If too few calls are getting through (reliability low), tell agents to work faster. If the lines are jammed (congestion), tell agents to slow down first. The goal is the right number of calls getting through — not every single call.

#### **Key Concept: Event Reliability**
ESRT defines reliability not in terms of packet delivery ratio but in terms of **sufficient data reaching the sink to accurately characterize an event**.

If sink receives enough readings from a region to determine "fire detected in sector B," that's reliable — even if some individual packets are lost.

#### **Two Main Functions:**

**1. Reliability Control:**
- Sink monitors incoming data rate vs required rate
- If data rate is too low → sink tells nodes to increase reporting frequency
- If data rate is too high → sink tells nodes to decrease (save energy)

**2. Congestion Control:**
- Sink detects congestion from packet drops and increasing delay
- Sink instructs nodes to reduce transmission rate

```
ESRT States:

    f = reporting frequency (events/second)
    η = reliability observed at sink

    States:
    +-----------+-----------+------------------------------+
    | η < ηreq  | Congested | Decrease f (reduce load)     |
    | η < ηreq  | No Cong.  | Increase f (get more data)   |
    | η ≥ ηreq  | Congested | Decrease f (maintain reliab) |
    | η ≥ ηreq  | No Cong.  | Optimal state ✅             |
    +-----------+-----------+------------------------------+
```

**ESRT Control Loop:**

```
Sink monitors data:
  If reliability low AND no congestion → f ↑ (nodes send more)
  If reliability low AND congested    → f ↓ (reduce congestion first)
  If reliability ok  AND congested    → f ↓ (maintain reliability, reduce energy)
  If reliability ok  AND no congestion → optimal, maintain f
```

✅ Energy efficient (sink-controlled, nodes don't compute routes)
✅ Handles congestion and reliability jointly
❌ Control messages from sink may not reach all nodes
❌ Assumes sink can monitor all traffic

---

### **2.5 CODA (Congestion Detection and Avoidance)**

**CODA** focuses specifically on **congestion control** in sensor networks — distinct from reliability.

#### **Three Mechanisms:**

**1. Congestion Detection:**
- Each node monitors its buffer occupancy and channel load
- If buffer occupancy exceeds threshold → congestion detected locally

**2. Open-Loop Hop-by-Hop Backpressure:**
- Congested node broadcasts BACKPRESSURE message to upstream neighbors
- Upstream nodes reduce their transmission rates
- Propagates backward through the network

**3. Closed-Loop Multi-Source Regulation:**
- For persistent congestion, sink sends SUPPRESS message
- Sources receiving SUPPRESS reduce transmission rates
- Sink adjusts suppression threshold based on observed event rate

```
CODA Flow:

Sources S1, S2, S3 → Node M (congested) → Node R → SINK

Step 1: M detects congestion (buffer 90% full)
Step 2: M broadcasts BACKPRESSURE to S1, S2, S3
Step 3: S1, S2, S3 reduce transmission rates
Step 4: If congestion persists, SINK sends SUPPRESS to sources
Step 5: Sources further reduce rates or defer transmissions
```

✅ Local (fast) congestion response via backpressure
✅ Global control via sink suppression
✅ Lightweight (no per-flow state)
❌ Backpressure may not reach all sources in large networks

---

## **Section 3: Application Layer Support**

### **3.1 Data Aggregation and Fusion**

**Data Aggregation**: Combining multiple data readings into a single (or fewer) packet(s) to reduce the total number of transmissions.

**Data Fusion**: Processing and combining data to produce higher-level information (e.g., average temperature from multiple sensors).

#### **Why Aggregation is Critical:**

```
Without aggregation:
S1 --[25°C]--> Sink
S2 --[26°C]--> Sink    (3 separate transmissions)
S3 --[25°C]--> Sink

With aggregation at node A:
S1 --[25°C]--> A
S2 --[26°C]--> A  →  A computes avg=25.3°C  →  A --[25.3°C]--> Sink
S3 --[25°C]--> A

Energy saved: 3 transmissions reduced to 1
```

#### **Aggregation Functions:**
| Function | Example |
|----------|---------|
| **MIN/MAX** | Maximum temperature in region |
| **AVG** | Average humidity across sector |
| **SUM** | Total count of detected events |
| **COUNT** | Number of nodes reporting |
| **HISTOGRAM** | Distribution of readings |

**Tree-based Aggregation**: Data flows up a spanning tree toward sink, with aggregation at each internal node.

**Challenges:**
- False readings from faulty nodes corrupt aggregates
- Aggregation adds latency (must wait for all children before forwarding)
- Security: malicious aggregator can corrupt results

---

### **3.2 Querying Paradigms**

#### **SQL-like Declarative Queries (TinyDB)**

**TinyDB** treats the sensor network as a distributed database. Users issue SQL-like queries:

```sql
SELECT nodeid, temperature
FROM sensors
WHERE temperature > 30
SAMPLE PERIOD 5s
LIFETIME 1min;
```

```sql
SELECT AVG(light), MAX(temperature)
FROM sensors
WHERE location='room_A'
SAMPLE PERIOD 10s;
```

TinyDB disseminates the query through the network, nodes evaluate locally, and results flow back to the query initiator through an aggregation tree.

**Query Model:**
- **Epoch-based**: Query runs repeatedly every SAMPLE PERIOD
- **Aggregation operators**: AVG, MIN, MAX, COUNT, SUM
- **Filters**: WHERE clause reduces data before transmission
- **Lifetime**: Query expires automatically

#### **Event-based Paradigm:**
- Nodes report only when a specific event occurs (threshold crossing, motion detected)
- No periodic reporting — saves energy when no events occur
- Example: "Report when temperature exceeds 50°C"

---

### **3.3 Time Synchronization: TPSN**

**TPSN (Timing-sync Protocol for Sensor Networks)** provides network-wide time synchronization, critical for:
- TDMA scheduling (nodes transmit in assigned time slots)
- Data fusion (correlate readings from different nodes by timestamp)
- Security protocols (replay attack detection needs timestamps)
- Duty cycling (synchronized sleep/wake cycles)

#### **TPSN Two Phases:**

**Phase 1: Level Discovery**
- Sink is level 0 (reference clock)
- Sink broadcasts "level 0" message
- Nodes that hear it become level 1
- Level 1 nodes broadcast, creating level 2 nodes, etc.
- Spanning tree formed

**Phase 2: Synchronization**
- Starting from level 1, each node exchanges timing messages with parent:

```
Node B (level 1) synchronizes with Sink (level 0):

Time:  t1        t2         t3          t4
        |         |          |           |
  B: ---[SYNC req sent]---[ACK received]------
  S:         ---[SYNC req received]---[ACK sent]---

t1 = B sends SYNC request
t2 = S receives SYNC request
t3 = S sends ACK with (t2, t3) embedded
t4 = B receives ACK

Clock offset = [(t2 - t1) + (t3 - t4)] / 2
Propagation delay = [(t4 - t1) - (t3 - t2)] / 2

B adjusts its clock by the computed offset.
```

✅ High accuracy (accounts for both offset and propagation delay)
✅ Scalable (hierarchical tree structure)
❌ Energy cost of synchronization messages
❌ Re-sync needed periodically (clocks drift)

---

### **3.4 Localization**

> PYQ: Present an overview of localization in wireless sensor network. (Dec 2023, 8 marks)

Most sensor applications need to know WHERE a sensor is located. GPS is too expensive (cost, energy, size) for every node.

#### **GPS-free Localization Approaches:**

**Anchor-based:**
- Few nodes have GPS (anchors/beacons)
- Regular nodes estimate position relative to anchors using:
  - **RSSI (Received Signal Strength Indicator)**: Stronger signal = closer
  - **ToA (Time of Arrival)**: Measure round-trip time for distance
  - **AoA (Angle of Arrival)**: Directional antennas measure angle

**DV-Hop:**
- Nodes estimate hop count to anchors
- Distance = hop count × avg hop distance
- Trilateration gives position from 3+ anchors

```
Trilateration Example:
  Anchor A at (0,0):    unknown node is 3m away → circle of r=3
  Anchor B at (5,0):    unknown node is 4m away → circle of r=4
  Anchor C at (2,4):    unknown node is 2m away → circle of r=2
  
  Intersection of 3 circles gives node position
```

---

## **Section 4: Dynamic Nature of WSNs and Mobile Robots**

> PYQ: Define dynamic nature of WSN. (Dec 2025, 2.5 marks)  
> PYQ: Explain Dynamic nature of WSNs and Secure routing in WSNs. (May 2023, 2×7.5=15 marks)  
> PYQ: Explain Sensor Networks & mobile robots. (Jul 2022, 7.5 marks)

### **4.1 Adapting to Dynamic Changes**

WSNs must operate despite:
- **Node failures**: Battery depletion, hardware faults, environmental damage
- **New nodes joining**: Replacement nodes, added density
- **Topology changes**: Link quality variation, node mobility
- **Channel variations**: Interference, multipath fading

#### **Self-Organization:**

```
Initial deployment:
  N1 -- N2 -- N3 -- SINK
         |
         N4

N2 fails (battery dead):

  N1        N3 -- SINK
              \
               N4

Self-healing response:
  N1 discovers N3 via neighbor discovery
  N1 -- N3 -- SINK  (new route)
  Network re-converges automatically
```

**Mechanisms for self-organization:**
- **Periodic beacon messages**: Nodes broadcast "I'm alive" messages
- **Neighbor tables**: Each node maintains list of live neighbors
- **Route rediscovery**: On next data send, new routes found
- **Clustering reformation**: LEACH rounds naturally redistribute cluster heads

#### **Self-Healing Properties:**
- **Redundancy**: Multiple paths to sink — if one fails, data routes around
- **Reactive protocols**: AODV-style on-demand route discovery
- **Proactive protocols**: Periodic updates maintain routing tables
- **Gradient-based**: Directed Diffusion can reinforce alternate path

---

### **4.2 Sensor Networks and Mobile Robots**

**Problem with Static WSN:**
- Nodes near the sink (gateway region) carry much more traffic than distant nodes → **hotspot problem**
- These gateway nodes deplete energy faster, creating coverage holes near sink
- Data collection from remote areas requires long multi-hop paths → high latency, high energy

**Mobile Sinks / Mobile Data Collectors:**

A mobile robot or unmanned vehicle traverses the sensor field to collect data.

```
Static WSN (hotspot problem):
  S1 S2 S3 --> Gateway_node --> SINK
  G G G ----> Gateway_node (overloaded, dies early)

Mobile Sink (robot):
  Robot moves through field:
  S1 S2 S3 --> [Robot in zone 1] collects data
  Moves to zone 2...
  S4 S5 S6 --> [Robot in zone 2] collects data
  
  Nodes communicate only short-range to nearby robot
  No multi-hop needed
```

#### **Benefits of Mobile Sinks:**
✅ **Eliminates hotspot energy drain** — no gateway nodes overloaded
✅ **Reduces hop count** — robot comes close to sources, fewer hops needed
✅ **Energy balanced** — all nodes expend similar energy
✅ **Higher data quality** — robot can request retransmissions locally
✅ **Large coverage** — robot covers entire field over time

#### **Challenges of Mobile Sinks:**
❌ **Latency**: Data stored at sensor until robot arrives (store-and-forward)
❌ **Prediction**: Sensors need to know robot trajectory to route data
❌ **Control**: Robot path planning is complex optimization problem
❌ **Rendezvous**: Sensors and robot must be in range at the right time

#### **Robot-Sensor Collaboration:**
- Sensors detect events and transmit location to robot
- Robot navigates to event location for detailed investigation
- Robot acts as mobile relay between isolated sensor clusters
- Robot can deploy new sensor nodes in gaps

---

## **Section 5: Security in Ad Hoc Networks**

> PYQ: Explain any four major challenges of security in WSN. (Dec 2025, 7 marks)  
> PYQ: List the different types of passive attacks. (Dec 2025, 2.5 marks)

### **5.1 Why Security is Hard in MANETs/WSNs**

| Factor | Security Implication |
|--------|---------------------|
| **No infrastructure** | No central authentication server; distributed trust needed |
| **Wireless medium** | Communications overheard by anyone in range |
| **Open deployment** | Nodes in hostile/unattended environments (easy to capture) |
| **Resource constraints** | Heavy crypto (RSA) too expensive; must use lightweight primitives |
| **No physical security** | Attacker can physically capture node and extract keys |
| **Dynamic topology** | Trust relationships change as nodes move/fail |
| **Multi-hop routing** | Data passes through untrusted intermediate nodes |

---

### **5.2 Security Requirements**

| Requirement | Definition | Threat if Violated |
|-------------|------------|-------------------|
| **Confidentiality** | Only authorized parties read data | Eavesdropping |
| **Integrity** | Data not modified in transit | Packet tampering |
| **Authentication** | Verify sender's identity | Spoofing, impersonation |
| **Availability** | Network remains operational | DoS, jamming |
| **Non-repudiation** | Sender cannot deny sending message | Dispute over data origin |
| **Freshness** | Data is recent (not replayed) | Replay attacks |
| **Authorization** | Only authorized nodes perform certain actions | Unauthorized control |

---

### **5.3 Attack Taxonomy**

#### **Passive Attacks (Eavesdropping):**

Attacker only listens — does not inject or modify traffic.

**Eavesdropping:**
- Attacker captures wireless transmissions
- Learns data content, node locations, communication patterns
- Defense: Encryption (AES, RC5)

**Traffic Analysis:**
- Even with encryption, attacker analyzes traffic patterns
- Who communicates with whom, how often, traffic volume
- Can infer events (e.g., traffic surge = something happened)
- Defense: Traffic padding, anonymization protocols

#### **Active Attacks:**

Attacker actively injects, modifies, or disrupts traffic.

**Jamming:**
- Attacker transmits interference signals to disrupt communication
- Simple: continuous noise; Sophisticated: jam only during ACKs
- Defense: Spread spectrum (FHSS, DSSS), frequency hopping

**Spoofing:**
- Attacker sends packets with forged source address
- Impersonates legitimate nodes
- Defense: Authentication (MAC codes, digital signatures)

**Sybil Attack:**
- Single malicious node presents MULTIPLE fake identities
- Appears as many nodes in routing protocols, voting schemes
- Can corrupt distributed algorithms (e.g., LEACH CH election)
- Defense: Identity certification, radio resource testing

```
Sybil Attack:
  Attacker M presents as M, M', M'', M'''
  Network thinks 4 legitimate nodes exist
  M controls all 4 "nodes" → manipulates routing
```

**Wormhole Attack:**

```
Wormhole Attack Diagram:

  A -- B -- C -- D -- E
       |              |
       +====Wormhole==+  (attacker has out-of-band high-speed link)
       (Attacker at B)   (Attacker at E)

Normal routing: A→B→C→D→E (4 hops)
Wormhole: Attacker at B tunnels packets to E
  A→B (legit), B tunnels to E via wormhole, E forwards to sink
  B and E appear as direct neighbors (1 hop!) to network
  Routing protocol prefers short paths → all traffic flows through wormhole
  Attacker can now drop, delay, or modify all traffic
```

- Two colluding attackers create private tunnel between distant network points
- Makes distant nodes appear as neighbors
- Attracts routing traffic through the tunnel
- Defense: Geographic routing (verify physical proximity), timing-based (leashes)

**Blackhole Attack:**
- Malicious node advertises best route to all destinations
- Attracts all traffic, then drops packets
- Defense: Multiple path routing, path verification

**Sinkhole Attack:**
- Attacker creates "attractive" node (claims great routes, high energy)
- Surrounding nodes route through attacker node
- All nearby traffic captured
- Defense: Multi-path routing, trust evaluation

**Denial of Service (DoS):**
- Flooding the network with fake/useless packets
- Depletes energy of legitimate nodes processing junk
- Defense: Rate limiting, puzzles (nodes must solve computational challenge)

---

## **Section 6: Key Management**

> PYQ: Briefly explain Key Management. (May 2023, 2.5 marks)

### **6.1 Why Key Management is Critical**

- Encryption requires **keys** shared between communicating parties
- In centralized networks: key server distributes keys
- In WSN: **no centralized server available** during operation
- Keys must be established **before deployment** (pre-distribution) or via distributed protocols
- If key is compromised (node captured) → entire network may be exposed

---

### **6.2 Symmetric vs Asymmetric Key**

| Aspect | Symmetric Key | Asymmetric (Public Key) |
|--------|--------------|------------------------|
| **Algorithm** | AES, RC5, DES | RSA, ECC |
| **Key size** | 128-256 bits | 1024-4096 bits (RSA) |
| **Computation** | Fast | Very slow |
| **Energy** | Low | **Very high (prohibitive for WSN)** |
| **Key distribution** | Requires pre-shared key or secure channel | Public key distributed openly |
| **WSN suitability** | ✅ Preferred | ❌ Generally too expensive |

**RSA on sensor node (e.g., ATmega128)**: A single RSA-1024 operation takes ~8 seconds and millions of instructions → **completely impractical** for WSN.

**ECC (Elliptic Curve Cryptography)**: Public key crypto with shorter keys — more feasible for sensors, but still ~10× more expensive than symmetric. Used in limited cases.

---

### **6.3 Key Pre-Distribution: Eschenauer-Gligor Scheme**

**Random Key Pre-Distribution**:

#### **Algorithm:**
1. Generate a large **key pool** P of random keys (e.g., 10,000 keys)
2. Before deployment, each node randomly selects a **key ring** of k keys from P (e.g., k=200)
3. After deployment, neighboring nodes check if they share any key(s)
4. If two nodes share at least one key → they can communicate securely
5. If no shared key → use multi-hop path through nodes that DO share keys

```
Key Pool P = {K1, K2, K3, ... K10000}

Node A's key ring: {K1, K45, K234, K567, K891, ...}  (200 random keys)
Node B's key ring: {K45, K123, K456, K891, K1024, ...} (200 random keys)

Shared keys: K45, K891 → A and B can communicate!

Node C's key ring: {K2, K3, K100, K200, ...}
A∩C = {} → No shared key
A and C communicate via multi-hop through nodes that bridge the key rings
```

#### **Probability of Shared Key:**

With a large key pool (e.g., 10,000 keys) and each node picking 200, roughly **1 in 3 neighbor pairs** will share at least one key — enough for good connectivity without every node needing every key.

**Key Establishment:**
- Nodes broadcast key identifiers (not the keys themselves)
- Find common key ID with neighbor
- Use that shared key to establish secure link

**Limitations:**
❌ Node capture reveals k keys → compromises all links using those keys
❌ Not 100% connectivity guaranteed (some nodes may have no shared keys)
❌ No forward secrecy (old sessions compromised if key revealed)

---

### **6.4 Pair-wise Key Establishment**

**Pair-wise keys**: Each pair of nodes gets a unique key — if one key is compromised, only that pair's link is exposed.

**Challenge**: n nodes require n(n-1)/2 keys — for 1000 nodes, that's ~500,000 keys. Too many to store on limited-memory sensor nodes.

**q-composite random key scheme**: Requires q shared keys (not just 1) between nodes before communication — harder to compromise.

**PIKE (Peer Intermediaries for Key Establishment)**: 
- Arrange nodes in virtual √n × √n grid
- Use pre-distributed keys with row/column intermediaries
- O(√n) keys per node instead of O(n)

---

### **6.5 Key Revocation**

When a node is compromised (captured by attacker), its keys must be revoked:

- **Centralized revocation**: Sink broadcasts revocation list — requires knowing which node is compromised
- **Self-reporting**: Node detects anomaly and broadcasts revocation of neighbor
- **Vote-based**: Multiple nodes vote to revoke a suspected compromised node (resist single false accusation)
- **Key refreshing**: Periodically replace old keys with new ones — limits window of compromise

**Challenge**: Revocation messages must be authenticated (attacker may try to revoke legitimate nodes).

---

## **Section 7: Secure Routing**

> PYQ: Briefly explain Secure routing. (Jul 2022, 2.5 marks)  
> PYQ: Explain Secure routing in WSNs. (May 2023, 7.5 marks)

### **7.1 Threats to Routing Protocols**

Routing protocols in MANETs/WSNs are particularly vulnerable because:
- Every node participates in routing — any malicious node can corrupt routes
- No central authority to verify routing information
- Routing updates broadcast over insecure wireless channel

**Routing Attacks:**
| Attack | Description |
|--------|-------------|
| **Route tampering** | Modify routing packets to redirect traffic |
| **False routing info** | Advertise non-existent routes or incorrect metrics |
| **Selective forwarding** | Drop specific packets while forwarding others |
| **Route hijacking** | Claim to have best route, attract all traffic |
| **Replay** | Retransmit old valid routing messages |

---

### **7.2 SEAD (Secure Efficient Ad hoc Distance vector)**

**SEAD** secures distance-vector routing (like DSDV) against attackers who modify or replay routing updates.

**Key Mechanism: One-way Hash Chains**

```
Hash chain: H^n(x) → H^(n-1)(x) → ... → H^2(x) → H(x) → x
  (each element is hash of next element)

Property: Easy to compute H(y) given y
           Hard to compute y given H(y) (one-way)
```

**How SEAD Works:**
1. Each node pre-generates a hash chain: h0, h1, h2, ... hn
2. When advertising route with metric m at sequence number s, attach hash element h[m]
3. Receiver verifies using previously received hash element h[m-1]
4. Attacker cannot forge a better route (would need to invert hash)
5. Cannot replay old updates (sequence numbers + hash chain prevent it)

✅ Prevents route tampering and replay attacks
✅ Very low overhead (hash computation is cheap)
❌ Proactive — high overhead in large dynamic networks
❌ Does not protect against rushing or wormhole attacks

---

### **7.3 Ariadne (Secure On-Demand Routing)**

**Ariadne** is based on **DSR (Dynamic Source Routing)** and provides:
- Authentication of route request/reply messages
- Prevention of route tampering by intermediate nodes

**Core Mechanisms:**
1. **TESLA (delayed key authentication)**: Each node broadcasts a message authenticated with a key, but only reveals the key later (after a short time delay). Recipients verify the message once the key is released. This proves the message was authentic without revealing the key too early for attackers to abuse it.
2. **Per-hop hashing**: Each intermediate node adds its own hash to the route record — like each person signing a relay baton as it passes through.
3. **Route verification**: Destination checks the entire chain of hashes to verify no hop was forged or modified.

```
Ariadne Route Discovery:

S ---[signed RREQ]--> A ---[+A's hash]--> B ---[+B's hash]--> D

D verifies: each hop's contribution is authentic
D sends RREP back along reverse path (also authenticated)
```

✅ Strong authentication of every hop in route
✅ Prevents false path advertisement
❌ Requires time synchronization (for TESLA key disclosure)
❌ High computation overhead for key management

---

### **7.4 SAODV (Secure AODV)**

**SAODV** extends AODV with digital signatures and hash chains:

- **RREQ/RREP messages** signed by the originator — attackers cannot forge packets as coming from a legitimate node
- **Hop count** protected by a hash chain — each hop uses the next element in the chain, so nobody can claim a shorter route without breaking the hash
- Intermediate nodes cannot fake the hop count (tampering breaks verification)
- Destination verifies the signature before trusting the reply

> **Analogy**: The source signs the packet like a document, and the hop count is protected by a seal that advances with each hop — tamper with either, and the seal breaks.

✅ Prevents modification of critical fields (hop count, sequence number)
✅ Source authentication via digital signature
❌ Signature verification expensive (asymmetric crypto)
❌ No protection against compromise of routing nodes themselves

---

## **Section 8: Cooperation and Intrusion Detection in MANETs**

> PYQ: Explain Intrusion Detection System. (Dec 2025, 2.5 marks)  
> PYQ: Explain Intrusion Detection System and Network Simulator. (May 2023, Dec 2023, 2×7.5=15 marks)  
> PYQ: Explain Intrusion Detection System and Sensor Networks & mobile robots. (Jul 2022, 7.5×2=15 marks)  
> PYQ: Explain Cooperation in MANETs and Sensor Network tools. (Jul 2022, 7.5×2=15 marks)

### **8.1 The Cooperation Problem**

In a MANET, nodes **must** forward packets for others to function as a network. But forwarding packets:
- Consumes battery energy
- Is a cost for the forwarding node with no direct benefit

**Selfish Nodes**: Nodes that participate in route discovery but **refuse to forward** others' packets (free-riding — they benefit from routing but don't contribute).

If many nodes are selfish → network fails even without external attackers.

**Question**: How do we **incentivize cooperation** or **detect non-cooperation**?

---

### **8.2 WATCHDOG Mechanism**

**WATCHDOG** detects misbehaving nodes that fail to forward packets.

> **Analogy**: Like a neighborhood watch — you hand a message to your neighbor and secretly listen to see if they pass it on to the next house. If they don't within a reasonable time, you mark them as untrustworthy.

**How it Works:**

```
Route: A → B → C → D

A sends packet to B (for forwarding to C):

WATCHDOG at A:
  A puts copy of packet in buffer
  A listens (promiscuously) for B's transmission
  If A hears B transmit the packet to C → OK, remove from buffer
  If timeout expires and A never hears B transmit → B suspected of misbehavior

A records: "B failed to forward 1 packet"
If failures exceed threshold → B marked as misbehaving → report to PATHRATER
```

```
Wireless overhearing:
  A ---[packet for C]---> B
  A listens on channel...
  B ---[packet for C]---> C  (A can hear this if in range — overhearing)
  A confirms B forwarded correctly
```

**Limitations:**
❌ **Ambiguous collisions**: B may have forwarded but A didn't hear (collision)
❌ **Partial dropping**: B drops some packets but not all — hard to detect
❌ **Collusion**: Two malicious nodes cooperate to evade detection
❌ **Transmission power**: B may lower power so A can't overhear
❌ **Does not work well with directional antennas**

---

### **8.3 PATHRATER**

**PATHRATER** complements WATCHDOG by using misbehavior reports to select reliable routes.

**Rating System:**
- Each node maintains a **rating** for every other node it knows
- Initial rating: 0.5 (neutral/unknown)
- Good behavior: rating increases toward 1.0
- Misbehavior reported by WATCHDOG: rating decreases toward 0.0

**Path Rating:**
- When choosing a route, PATHRATER computes a **path metric** = average of node ratings along path
- Routes through well-behaved nodes preferred
- Routes through suspected misbehaving nodes avoided

```
Path A→B→C→D→E:
  Rating of B = 0.9 (good)
  Rating of C = 0.3 (suspected misbehaving)
  Rating of D = 0.8 (good)
  
  Path metric = avg(0.9, 0.3, 0.8) = 0.67

Path A→F→G→E:
  Rating of F = 0.85, G = 0.88
  Path metric = avg(0.85, 0.88) = 0.87  ← preferred!
```

✅ Incentivizes good behavior (misbehaving nodes get bypassed)
✅ Routing naturally improves as ratings converge
❌ Ratings can be manipulated (false reports from malicious nodes)
❌ Slow to converge in large networks
❌ New nodes start with neutral rating — exploitable

---

### **8.4 Intrusion Detection Systems (IDS) in MANETs**

An **IDS** monitors the network for signs of malicious activity and raises alerts.

#### **Types of Detection:**

**1. Anomaly Detection:**
- Establish baseline of "normal" behavior
- Flag deviations from baseline as suspicious
- Example: Node normally forwards 100 packets/min; suddenly drops to 5 → anomaly
- ✅ Can detect unknown attacks
- ❌ High false positive rate; difficult to define "normal" in dynamic MANET

**2. Misuse Detection (Signature-based):**
- Maintain database of known attack signatures/patterns
- Match observed behavior against signatures
- Example: Detect sequence number manipulation (SAODV violation)
- ✅ Low false positives for known attacks
- ❌ Cannot detect novel attacks; signatures must be updated

#### **Distributed IDS Architecture for MANETs:**

```
+--Local IDS Agent---+    +--Local IDS Agent---+
|  Monitor           |    |  Monitor           |
|  Detect anomalies  |<-->|  Detect anomalies  |
|  Local response    |    |  Local response    |
+--------------------+    +--------------------+
         |                          |
         +--------[Cooperative]-----+
                   |
         Global IDS Decision
         (consensus among neighbors)
```

**Architecture Layers:**

| Layer | Function |
|-------|---------|
| **Data collection** | Promiscuous monitoring, audit logs |
| **Local detection** | Each node runs local IDS agent |
| **Cooperative detection** | Nodes share intrusion evidence with neighbors |
| **Global response** | Consensus-based revocation, isolation of intruder |

**Challenges of IDS in MANET:**
- No central point to collect all traffic — each node sees only local traffic
- Dynamic topology means behavior baseline shifts
- Resource constraints limit IDS complexity
- Cooperative IDS requires secure communication between IDS agents
- False accusation can isolate legitimate nodes

---

## **Section 9: Sensor Network Hardware — Berkeley Motes**

> PYQ: Briefly explain Berkeley Motes. (Jul 2022, 2.5 marks)

### **9.1 What is a Mote?**

A **mote** is a tiny, self-contained sensor node designed for wireless sensor networks. The term "mote" (particle of dust) reflects the goal of making sensor nodes as small and inexpensive as possible.

**Core components of any mote:**
```
+--------------------------------------------------+
|                  MOTE                            |
|  +------------+  +--------+  +--------------+   |
|  |    MCU     |  | Radio  |  |   Sensors    |   |
|  | (process)  |  |(comm.) |  | (temp,light) |   |
|  +------------+  +--------+  +--------------+   |
|  +-------------------+  +--------------------+  |
|  |      Memory       |  |   Power (Battery)  |  |
|  | Flash + RAM       |  |   AA/AAA/coin cell |  |
|  +-------------------+  +--------------------+  |
+--------------------------------------------------+
```

---

### **9.2 Berkeley Mote Generations**

| Mote | Year | MCU | Radio | Flash | RAM | Notes |
|------|------|-----|-------|-------|-----|-------|
| **WeC** | 1998 | AT90LS8535 | TR1000 (916 MHz) | 512B | 512B | First mote prototype |
| **Mica** | 2001 | ATmega128 | TR1000 | 512KB | 4KB | Introduced TinyOS |
| **Mica2** | 2002 | ATmega128 | CC1000 | 512KB | 4KB | Better radio, longer range |
| **MicaZ** | 2004 | ATmega128 | CC2420 (802.15.4/ZigBee) | 512KB | 4KB | IEEE 802.15.4 standard |
| **TelosB** | 2004 | MSP430 | CC2420 (802.15.4) | 1MB Flash | 10KB RAM | USB programming, low power |

---

### **9.3 TelosB / MicaZ Specifications (Exam Focus)**

#### **TelosB (Telos "Berkeley"):**

```
+--------------------------------------------------+
|                  TelosB Mote                     |
|                                                  |
|  MCU: TI MSP430 @ 8 MHz                         |
|  Radio: Chipcon CC2420 (IEEE 802.15.4, 2.4 GHz) |
|  RAM: 10 KB                                      |
|  Flash: 1 MB (program + data storage)            |
|  Interface: USB (for programming + power)        |
|  Sensors: onboard temp, humidity, light, PAR     |
|  Antenna: onboard PCB antenna                   |
|  Power: 2× AA batteries                         |
|  Data rate: 250 kbps                            |
|  Range: ~50-125m outdoor                        |
+--------------------------------------------------+
```

#### **MicaZ:**

```
+--------------------------------------------------+
|                  MicaZ Mote                      |
|                                                  |
|  MCU: Atmel ATmega128 @ 7.37 MHz                |
|  Radio: Chipcon CC2420 (IEEE 802.15.4, 2.4 GHz) |
|  RAM: 4 KB                                       |
|  Flash: 512 KB program + 4 MB data flash        |
|  Interface: 51-pin expansion connector          |
|  Power: 2× AA batteries                         |
|  Data rate: 250 kbps                            |
|  Range: up to 75m indoor / 300m outdoor         |
+--------------------------------------------------+
```

#### **CC2420 Radio (IEEE 802.15.4):**
- Frequency: 2.4 GHz (16 channels)
- Data rate: 250 kbps
- **CSMA/CA** medium access
- **Hardware AES-128** encryption/decryption
- Supports ACKs and retransmissions in hardware

---

### **9.4 Mote Block Diagram**

```
                  +---------+
                  | Sensors |
                  | (Temp,  |
                  |  Light, |
                  |  Humid) |
                  +----+----+
                       | (ADC/I2C/SPI)
+----------+      +----v----+      +----------+
| External |      |         |      |          |
| Storage  +------+   MCU   +------+  Radio   +---)))  Antenna
| (Flash)  |      | (CPU+   |  SPI |  Module  |
|          |      |  RAM)   |      | CC2420   |
+----------+      +----+----+      +----------+
                       |
                  +----v----+
                  |  Power  |
                  | Mgmt /  |
                  | Battery |
                  +---------+
```

---

## **Section 10: TinyOS and nesC**

> PYQ: What is TinyOS? (May 2023, 2.5 marks)  
> PYQ: Explain the features and limitations of Tiny OS. (May 2025, 15 marks)  
> PYQ: Explain how the TinyOS operating system supports resource constrained hardware platforms. Discuss in detail. (Dec 2025, 15 marks)

### **10.1 What is TinyOS?**

**TinyOS** is an **open-source, event-driven operating system** designed specifically for resource-constrained sensor nodes (motes).

Developed at UC Berkeley, TinyOS is written in **nesC** (network embedded systems C).

#### **Key Design Philosophy:**
- **Extremely small footprint**: fits in 4KB ROM, works with 256 bytes RAM
- **Component-based**: functionality divided into reusable components
- **Event-driven**: no blocking calls — asynchronous events drive execution
- **No dynamic memory allocation**: all memory statically allocated at compile time
- **Cooperative scheduling**: no preemptive multitasking

---

### **10.2 TinyOS Architecture**

```
+----------------------------------------------+
|             Application (Blink, Surge, etc.) |
+----------------------------------------------+
|         TinyOS Components (Timer, Leds, etc.) |
|  +--------+  +-------+  +---------+          |
|  | TimerC |  | LedsC |  | Radio   |  ...     |
|  +--------+  +-------+  +---------+          |
+----------------------------------------------+
|       Hardware Abstraction Layer (HAL)       |
|  +--------+  +--------+  +---------+        |
|  |  MCU   |  | Radio  |  | Sensors |        |
|  +--------+  +--------+  +---------+        |
+----------------------------------------------+
|            Hardware (ATmega, CC2420, etc.)   |
+----------------------------------------------+
```

#### **Execution Model:**

```
Event occurs (interrupt):
  → Event handler runs (fast, non-blocking)
  → May post a task to task queue
  
Task queue:
  → Tasks run to completion (non-preemptive)
  → No context switching needed
  → Lightweight scheduling

Event:
  Interrupt → Handler → Post task → Return
  
Task:
  Dequeued → Execute to completion → Next task
```

**Key Features:**
- **Commands**: Called by application to request service (synchronous, non-blocking call downward)
- **Events**: Signaled by hardware/components to notify application (asynchronous, upward)
- **Tasks**: Deferred computation, posted to run in background

---

### **10.3 nesC (Network Embedded Systems C)**

**nesC** is the programming language used to write TinyOS applications. It extends C with a component model.

#### **Component Model:**

Two types of components in nesC:

| Component Type | Description |
|---------------|-------------|
| **Module** | Contains actual implementation code (variables, functions) |
| **Configuration** | Wires modules together (no code, just connections) |

#### **Interface:**

An interface specifies a set of functions. Each interface has:
- **Commands**: Functions called by upper component (client calls provider)
- **Events**: Functions signaled by lower component (provider signals client)

```
interface Timer {
  command void start(uint32_t interval);  // command: client calls this
  event void fired();                      // event: provider signals this
}
```

#### **nesC Component Example — BlinkC:**

```c
// BlinkAppC.nc (Configuration — wires components)
configuration BlinkAppC {
}
implementation {
  components MainC, BlinkC, LedsC;
  components new TimerMilliC() as Timer0;

  BlinkC -> MainC.Boot;           // Blink uses Boot interface from Main
  BlinkC.Leds -> LedsC;           // Blink uses Leds from LedsC
  BlinkC.Timer -> Timer0;         // Blink uses Timer from Timer0
}

// BlinkC.nc (Module — actual logic)
module BlinkC {
  uses interface Timer<TMilli>;   // uses Timer interface
  uses interface Leds;            // uses Leds interface
  uses interface Boot;            // uses Boot interface
}
implementation {
  event void Boot.booted() {
    call Timer.start(TIMER_REPEAT, 1000);  // start 1s repeating timer
  }

  event void Timer.fired() {
    call Leds.led0Toggle();  // toggle LED on every timer event
  }
}
```

```
Wiring Diagram:
  BlinkC ----Boot----> MainC
  BlinkC ----Leds----> LedsC
  BlinkC ----Timer---> TimerMilliC
```

#### **nesC Compilation:**

```
nesC source files (.nc)
        |
   [nesC compiler (ncc)]
        |
   C code generated
        |
   [GCC for target MCU]
        |
   Binary image (.elf)
        |
   Flash to mote
```

**nesC Key Properties:**
- **Whole-program analysis**: Compiler analyzes entire component graph
- **Race condition detection**: Detects potential data races at compile time
- **Static memory**: No malloc/free — safe, predictable
- **Inline expansion**: Small functions inlined for efficiency

---

### **10.4 TinyGALS (Dataflow Style)**

> PYQ: Explain Tiny GALS. (May 2025, 3 marks)

**TinyGALS (TinyOS Global Asynchronous Locally Synchronous)** is an alternative programming model for TinyOS that uses a **dataflow** paradigm.

#### **GALS Model:**

```
Globally Asynchronous:
  - Communication between components is asynchronous (buffered queues)
  - No global lock or synchronization primitive needed

Locally Synchronous:
  - Within each component, execution is synchronous and predictable
  - Component processes events one at a time
```

```
TinyGALS Architecture:

+-------------+   async queue   +-------------+   async queue   +--------+
|  Component  | ----[buffer]--> |  Component  | ----[buffer]--> |  Sink  |
|  A (local   |                 |  B (local   |                 |        |
|   sync)     |                 |   sync)     |                 |        |
+-------------+                 +-------------+                 +--------+
    ^                                   ^
    | (local synchronous within)        | (local synchronous within)
    v                                   v
```

**Comparison with nesC event model:**

| Aspect | TinyOS/nesC | TinyGALS |
|--------|-------------|---------|
| **Style** | Event-driven, call/signal | Dataflow, actor-based |
| **Inter-component** | Synchronous function call | Asynchronous queued messages |
| **Concurrency** | Task queue, interrupts | Actors run independently |
| **Complexity** | Lower | Higher |
| **Throughput** | Lower | Higher for pipelines |

---

## **Section 11: Simulators**

> PYQ: Write the functionalities of NS-2 in the simulation of sensor network. (May 2025, Dec 2025, 8 marks)  
> PYQ: Mention the use of TOSSIM simulator in modelling wireless network. (May 2025, 7 marks)  
> PYQ: Explain Network Simulator. (May 2023, Dec 2023, 7.5–8 marks)  
> PYQ: Explain Sensor Network tools. (Jul 2022, 7.5 marks)

### **11.1 ns2 and Sensor Network Extension**

**ns2 (Network Simulator 2)** is a widely-used, discrete event network simulator for general network research.

#### **ns2 Architecture:**

```
+------------------------------------------+
|              User (Tcl script)           |
+------------------------------------------+
|         OTcl (Object-oriented Tcl)       |
|    [Topology, Protocol config scripts]   |
+------------------------------------------+
|          C++ Core (fast simulation)      |
|  [Packet handling, protocol impl, etc.]  |
+------------------------------------------+
|              Event Scheduler             |
+------------------------------------------+
```

- Written in **C++ and Tcl/OTcl** (split programming)
- Configuration via Tcl scripts (topology, traffic, protocols)
- C++ handles performance-critical simulation
- **Output**: trace files analyzed with AWK/Perl scripts

#### **Sensor Network Extension for ns2 (SensorSim / MIT's extension):**

Base ns2 lacks sensor-specific features. Extensions add:
- **Energy model**: Tracks energy consumption per node (TX, RX, sleep, idle states)
- **Radio propagation models**: Two-ray ground, Shadowing model for wireless
- **Sensor models**: Simulate sensing range, detection probability
- **Aggregation support**: In-network data fusion simulation

You configure simulations using Tcl scripts — define nodes, set energy parameters (initial energy, transmit/receive power), configure protocols, and run the simulator. The output is a trace file you analyze with scripts to measure performance.

**Advantages of ns2:**
✅ Widely used — huge protocol library (AODV, DSDV, DSR built-in)
✅ Detailed packet-level simulation
✅ Community support, many sensor extensions available

**Disadvantages:**
❌ Slow for large sensor networks (1000+ nodes)
❌ Sensor-specific features require external extensions
❌ Complex Tcl/C++ split makes modification hard
❌ Does not simulate actual TinyOS code

---

### **11.2 TOSSIM (TinyOS Simulator)**

**TOSSIM** is a simulator specifically designed to simulate **TinyOS applications** — it can run the actual TinyOS code, not just a model.

#### **Key Innovation: Same Code for Simulation and Hardware**

```
                TinyOS Application Code (.nc)
                           |
              +------------+------------+
              |                         |
        [Compile for                [Compile for
          TOSSIM]                   real hardware
              |                         |
        [TOSSIM                   [Mote binary]
         library]                       |
              |                         |
        [Runs on PC]              [Flash to mote]
        [Simulates many            [Runs on real
         virtual motes]             sensor node]
```

No code changes needed — same `.nc` files compile to both simulation and hardware.

#### **TOSSIM Architecture:**

```
+------------------------------------------+
|      TinyOS Application (nesC code)      |
+------------------------------------------+
|     TOSSIM Simulation Library            |
|  +--------+  +---------+  +-----------+ |
|  | Radio  |  |  Timer  |  |  Sensor   | |
|  | Model  |  |  Model  |  |  Model    | |
|  +--------+  +---------+  +-----------+ |
|  +---------------------------------+    |
|  |      Event Scheduler            |    |
|  +---------------------------------+    |
+------------------------------------------+
|         Host OS (Linux/Mac/Windows)      |
+------------------------------------------+
```

#### **TOSSIM Radio Model:**

**Bit-level radio simulation:**
- Models each bit individually (not just packet-level)
- Captures interference, collisions at bit level
- Uses a **link-layer model** based on measured real-world data
- Supports RSSI (received signal strength) modeling

```
TOSSIM Link Model:
  For each pair of nodes (A, B):
    gain = signal strength from A to B (dBm)
    If received power > threshold → packet received
    Noise model adds random interference
    Bit errors computed from SNR → packet error rate
```

#### **TOSSIM Python Interface:**

TOSSIM provides a Python scripting interface to set up simulations without modifying the nesC code:
- Create virtual nodes and boot them at different times
- Define radio links between node pairs with realistic signal strengths (in dBm)
- Step through simulation events one at a time or in bulk
- Inspect node state, debug output, and print logs from the simulated nodes

This lets you test your TinyOS application in simulation before flashing it to real hardware.

#### **TOSSIM vs ns2 Comparison:**

| Feature | ns2 | TOSSIM |
|---------|-----|--------|
| **Language** | Tcl/C++ | nesC/C (TinyOS) |
| **Abstraction** | Protocol model | Actual code execution |
| **Code reuse** | ❌ Must rewrite for ns2 | ✅ Same code as hardware |
| **Radio model** | Various models | Bit-level, empirical |
| **Scale** | ✅ Thousands of nodes | ❌ ~100s of nodes (slower) |
| **Accuracy** | Protocol-level | ✅ Bit-level, very accurate |
| **Protocol support** | Wide (IP, AODV, etc.) | TinyOS protocols only |
| **Debug** | Trace file analysis | Printf, Python interaction |
| **Sensor models** | Via extensions | TinyOS sensor components |

---

## **Quick Revision Points**

### Section 1 — Routing

- **WSN routing**: energy-aware, data-centric, no global IDs
- **Flooding problems**: implosion, overlap, blindness
- **Directed Diffusion phases**: interest propagation → data propagation → reinforcement
- **SPIN messages**: ADV (advertise), REQ (request), DATA
- **LEACH**: probabilistic CH election (weighted coin flip, recent CHs excluded), cluster formation, TDMA schedule, data aggregation at CH

### Section 2 — Transport

- **TCP not suitable**: wireless loss misinterpreted as congestion, symmetric assumption wrong
- **PSFQ**: sink→nodes reliability; pump slowly, fetch quickly via NAK + local recovery
- **ESRT**: sensors→sink reliability; sink controls reporting frequency, 4 states based on reliability + congestion
- **CODA**: congestion control; backpressure from congested nodes + sink SUPPRESS

### Section 3 — Application

- **Data aggregation**: combine sensor readings at intermediate nodes (MIN/MAX/AVG/SUM)
- **TinyDB**: SQL-like declarative queries on sensor network ("SELECT AVG(temp) ... SAMPLE PERIOD 5s")
- **TPSN**: time sync; spanning tree from sink; pairwise sync using t1,t2,t3,t4 timestamps
- **Localization**: GPS-free via RSSI/ToA + trilateration from anchors

### Section 4 — Dynamic & Robots

- **Self-organization**: periodic beacons, neighbor tables, route rediscovery after failures
- **Hotspot problem**: gateway nodes near sink overloaded → die early
- **Mobile sink benefits**: eliminates hotspot, reduces hop count, balances energy
- **Mobile sink drawback**: latency (store-and-forward until robot arrives)

### Section 5 — Security

- **Security hard because**: no infrastructure, wireless (eavesdrop), resource-constrained, physically exposed
- **Security requirements**: CIA + availability + non-repudiation + freshness
- **Passive**: eavesdropping, traffic analysis
- **Active**: jamming, spoofing, Sybil, wormhole, blackhole, sinkhole, DoS
- **Wormhole**: two colluding nodes create tunnel, attract routing traffic, can drop/modify
- **Sybil**: one attacker presents multiple fake identities

### Section 6 — Key Management

- **Symmetric preferred** in WSN (AES, RC5) — RSA too expensive (8s per operation on ATmega)
- **Eschenauer-Gligor**: pool of P keys, each node picks k random keys, communicate if share ≥1 key
- **Probability of shared key** ≈ 0.33 for P=10000, k=200
- **Key revocation**: vote-based, centralized revocation list, periodic refresh

### Section 7 — Secure Routing

- **SEAD**: secures distance-vector routing using one-way hash chains; prevents route tampering/replay
- **Ariadne**: secures DSR using TESLA; per-hop authentication of route discovery
- **SAODV**: secures AODV with digital signatures (source auth) + hash chains (hop count protection)

### Section 8 — Cooperation & IDS

- **Selfish nodes**: refuse to forward to save battery → network fails
- **WATCHDOG**: promiscuous listening to verify neighbor forwards packets
- **PATHRATER**: rate nodes 0-1 based on WATCHDOG; prefer routes through high-rated nodes
- **IDS types**: anomaly detection (baseline deviation) vs misuse detection (signature matching)
- **Distributed IDS**: local agents cooperate via information sharing + consensus response

### Section 9 — Hardware

- **Mote components**: MCU + Radio + Sensors + Memory + Battery
- **TelosB**: MSP430 @ 8MHz, CC2420 radio, 10KB RAM, 1MB Flash, USB, onboard sensors, 2× AA
- **MicaZ**: ATmega128 @ 7.37MHz, CC2420 radio, 4KB RAM, 512KB Flash
- **CC2420**: 2.4GHz, 250kbps, IEEE 802.15.4, hardware AES-128

### Section 10 — TinyOS/nesC

- **TinyOS**: event-driven, component-based, no dynamic memory, cooperative scheduling
- **nesC component types**: Module (code) + Configuration (wiring)
- **Interface**: Commands (called downward) + Events (signaled upward)
- **BlinkC**: Boot.booted() → Timer.start(); Timer.fired() → Leds.toggle()
- **TinyGALS**: globally async (queued inter-component msgs), locally sync (ordered within component)

### Section 11 — Simulators

- **ns2**: general network simulator, Tcl+C++, packet-level, needs extensions for sensors
- **TOSSIM**: TinyOS-specific, runs actual nesC code, bit-level radio, same code as hardware
- **TOSSIM advantage**: code portability (simulate AND deploy same code)
- **TOSSIM disadvantage**: limited scale (~100s nodes), TinyOS-only

---

## **Expected Exam Questions**

### **15-mark Questions**

1. Explain the features and limitations of Tiny OS. *(May 2025)*
2. Explain how the TinyOS operating system supports resource constrained hardware platforms. *(Dec 2025)*
3. Explain Intrusion Detection System and Network Simulator. *(May 2023, Dec 2023)*
4. Explain Intrusion Detection System and Sensor Networks & mobile robots. *(Jul 2022)*
5. Explain Cooperation in MANETs and Sensor Network tools. *(Jul 2022)*
6. Explain Dynamic nature of WSNs and Secure routing in WSNs. *(May 2023)*
7. Appraise the QoS related measures + Outline the issues related to the transport layer in WSN. *(Dec 2023)*
8. Appraise the issues related to routing in WSN + Present an overview of localization in WSN. *(Dec 2023)*

### **7–8 mark Questions**

1. Write the functionalities of NS-2 in the simulation of sensor network. *(May 2025, Dec 2025)*
2. Mention the use of TOSSIM simulator in modelling wireless network. *(May 2025)*
3. Explain any four major challenges of security in WSN. *(Dec 2025)*

### **Short Answer (2.5–3 marks)**

1. Explain Intrusion Detection System. *(Dec 2025)*
2. Define dynamic nature of WSN. *(Dec 2025)*
3. List the different types of passive attacks. *(Dec 2025)*
4. Explain Tiny GALS. *(May 2025)*
5. What is TinyOS? *(May 2023)*
6. Briefly explain Key Management. *(May 2023)*
7. Briefly explain Secure routing. *(Jul 2022)*
8. Briefly explain Berkeley Motes. *(Jul 2022)*

---

_These notes were compiled by [Deepak Modi](https://deepakmodi.dev)_  
_Last updated: May 2026_
