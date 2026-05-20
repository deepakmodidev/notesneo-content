---
title: "Unit 2: Data Transmission in Ad Hoc Networks"
description: "Broadcast Storm Problem, Broadcasting, Multicasting, Geocasting, and TCP over Ad Hoc Networks"
author: "Deepak Modi"
date: "2026-05-10"
pdfUrl: ""
---

## Syllabus:

Data Transmission: Broadcast storm problem, Broadcasting, Multicasting and Geocasting. TCP over Ad Hoc: TCP protocol overview, TCP and MANETs, Solutions for TCP over ad hoc.

---

## 🎯 PYQ Analysis for Unit 2

### **High Priority Topics** (15 marks questions)

1. **TCP over Ad-hoc Wireless Networks (TCP + Solutions)** — (May 2023: 15, Jul 2022: 15, Dec 2023: 15)
2. **Broadcast Storm Problem + Transmission Control Protocol** — (May 2023: 7+8, Jul 2022: 7+8)
3. **Geocasting (with application)** — (Dec 2025: 8 marks)
4. **Multicast (with application)** — (May 2025: 8 marks)
5. **Hidden-Terminal & Exposed-Terminal Problem (how avoided)** — (Dec 2025: 7 marks)

### **Medium Priority Topics** (Short answers)

1. **Broadcast Storm Problem** — Dec 2025 (2.5 marks)
2. **TCP Protocol** — Dec 2023 (2.5 marks)
3. **Geocasting** — May 2023 (2.5 marks)
4. **Multicasting** — Jul 2022 (2.5 marks)
5. **TCP Variations (2 of them) with advantages/disadvantages** — May 2025, Dec 2025 (7 marks)
6. **Broadcast Storm Problem — How to avoid?** — May 2025 (7 marks)

---

## **Section 1: Broadcasting in MANETs**

### **1.1 What is Broadcasting?**

**Broadcasting** is a one-to-all communication model where a single source node transmits a packet that must be received by **all other nodes** in the network.

In wired networks, broadcasting is straightforward — switches handle it at the hardware level. In **MANETs (Mobile Ad Hoc Networks)**, broadcasting is challenging because:
- There is no central infrastructure
- Nodes act as both hosts and routers
- Topology changes dynamically due to node mobility
- Wireless medium is shared — transmissions can interfere

**Use cases of broadcasting in MANETs:**
- Route discovery (e.g., RREQ packets in AODV)
- Network-wide announcements
- Topology updates (e.g., in OLSR)
- Emergency alerts

---

### **1.2 Simple Flooding**

**Simple flooding** is the most basic broadcasting mechanism. Every node that receives a broadcast packet for the first time **rebroadcasts it** to all its neighbors.

#### **How Simple Flooding Works:**

```
Step 1: Source node S broadcasts packet P.
Step 2: All neighbors of S receive P and rebroadcast it.
Step 3: Each node that receives P for the first time rebroadcasts it.
Step 4: Nodes that have already seen P discard duplicates.
Step 5: Process continues until all reachable nodes have received P.
```

#### **ASCII Diagram — Simple Flooding:**

```
        A
       / \
      B   C
     / \ / \
    D   E   F
         \
          G

S = Source node A broadcasts packet P

Step 1:  A --> B, C (A broadcasts)
Step 2:  B --> D, E  (B rebroadcasts)
         C --> E, F  (C rebroadcasts)
Step 3:  D --> (no new neighbors)
         E --> G     (E rebroadcasts — first time)
         E discards duplicate from C
         F --> (no new neighbors)
Step 4:  G receives P — done

All nodes A, B, C, D, E, F, G have received P.
```

#### **Advantages of Simple Flooding:**
- ✅ Simple to implement — no state required
- ✅ Guarantees delivery if the network is connected
- ✅ Works well in sparse networks

#### **Disadvantages of Simple Flooding:**
- ❌ Causes **Broadcast Storm Problem** in dense networks
- ❌ High redundant transmissions waste bandwidth
- ❌ Collisions due to simultaneous transmissions
- ❌ Heavy contention at the MAC layer
- ❌ Does not scale with network size

---

### **1.3 The Broadcast Storm Problem**

> PYQ: What is broadcast storm problem? (Dec 2025, 2.5 marks)  
> PYQ: What is broadcast storm problem? How to avoid this problem? (May 2025, 7 marks)  
> PYQ: Explain Broadcast storm problem. (May 2023, 7 marks; Jul 2022, 8 marks)

#### **Definition:**

The **Broadcast Storm Problem** is a critical phenomenon in wireless ad hoc networks where naive flooding causes a **massive number of redundant transmissions**, leading to severe network congestion, collisions, and degraded performance.

This problem was formally studied and named in a well-known 1999 research paper on mobile ad hoc networks.

#### **Causes of the Broadcast Storm Problem:**

1. **Redundancy:** Multiple neighbors of a node may all rebroadcast the same packet, covering nearly identical areas — wasted transmissions.
2. **Contention:** Many nodes transmit at the same time, causing MAC-layer collisions.
3. **Collision:** Hidden terminals cause simultaneous transmissions → packet loss.
4. **Dense networks:** The more nodes in a neighborhood, the worse the storm.

#### **ASCII Diagram — Broadcast Storm (Redundant Transmissions):**

```
Dense Network Scenario:

     [A]--[B]--[C]
      |  X  |  X  |
     [D]--[E]--[F]
      |  X  |  X  |
     [G]--[H]--[I]

Source: A broadcasts RREQ

Without storm control:
- A transmits to B, D, E  (1 transmission)
- B retransmits to A, C, D, E  (covers same area as A)
- D retransmits to A, B, E, G, H  (mostly already covered)
- E retransmits to B, C, D, F, G, H, I (covers what B, D already covered)

Result:
  Total transmissions = N (nearly every node retransmits)
  Coverage area overlap = very high
  Useful new coverage per retransmission = very low
  Collisions = many (nodes transmit simultaneously)

  This is the BROADCAST STORM.
```

#### **Effects of Broadcast Storm:**
- **Network congestion** — channel saturated with redundant packets
- **High packet collision rate** — simultaneous transmissions interfere
- **Increased latency** — nodes must wait and retry
- **Battery drain** — unnecessary transmissions waste energy (critical in sensor networks)
- **Channel throughput drops** dramatically
- **Broadcast packets may actually be lost** — the storm defeats the purpose of broadcasting

#### **Quantifying the Problem:**

In a network with N nodes each with k neighbors:
- **Simple flooding** → up to **N transmissions**
- **Useful transmissions** (those that actually extend coverage) → much fewer
- **Redundancy ratio** = (Total Tx - Useful Tx) / Total Tx → can be > 80% in dense networks

---

### **1.4 Solutions to the Broadcast Storm Problem**

Several techniques have been proposed to reduce redundant transmissions while still ensuring broadcast delivery. These fall into five main categories:

---

#### **1.4.1 Probability-Based Methods**

**Concept:** Instead of always rebroadcasting, each receiving node rebroadcasts with a **probability p** (where 0 < p < 1).

```
On receiving broadcast packet:
  Generate random number r ∈ [0, 1]
  if r < p:
      rebroadcast the packet
  else:
      discard (don't rebroadcast)
```

**Fixed Probability Scheme:**
- Every node uses a fixed probability p (e.g., p = 0.6 or 0.8)
- Simple, no state needed

**Counter-Adaptive Probability:**
- p is adjusted based on how many times the packet has been received
- More copies received → lower probability (neighbors already rebroadcast it)

**Advantages:**
- ✅ Simple, requires no additional information
- ✅ Reduces redundant transmissions significantly

**Disadvantages:**
- ❌ No delivery guarantee — some nodes may not receive the broadcast
- ❌ Choosing the right p is difficult
- ❌ Works poorly in sparse networks (low p → message may not reach all)

---

#### **1.4.2 Counter-Based Methods**

**Concept:** Each node counts how many times it has received the same broadcast packet. If the count exceeds a **threshold C**, it decides NOT to rebroadcast.

```
On receiving broadcast packet P:
  counter[P] += 1
  if counter[P] == 1:
      Set timer (wait before rebroadcasting)
  if counter[P] >= C before timer expires:
      Cancel timer → do NOT rebroadcast
  if timer expires and counter[P] < C:
      Rebroadcast P
```

**Rationale:** If a node receives the same packet many times from many neighbors, those neighbors have already covered the area — no need to rebroadcast.

**Advantages:**
- ✅ More adaptive than pure probability
- ✅ Works better in dense networks

**Disadvantages:**
- ❌ Still requires threshold tuning
- ❌ Sparse network: threshold may never be reached → all rebroadcast

---

#### **1.4.3 Distance-Based Methods**

**Concept:** A node decides to rebroadcast only if the **distance** between itself and the sender of the broadcast is **greater than a threshold d**.

```
On receiving broadcast packet P from node X:
  dist = distance(self, X)
  if dist > d_threshold:
      rebroadcast P
  else:
      discard P (X's transmission already covers our area)
```

**Rationale:** If a node is very close to the sender, the sender's transmission radius likely already covers the node's neighbors too — no need to rebroadcast.

```
ASCII:
  [Sender S] ------d------- [Node A]
  |<--- R (radio range) --->|

If d > threshold (node far from sender) → rebroadcast
If d < threshold (node close to sender) → don't rebroadcast
```

**Requirements:** Nodes must know their location (e.g., via GPS).

**Advantages:**
- ✅ Significant reduction in redundant transmissions
- ✅ Geometrically motivated — good spatial coverage logic

**Disadvantages:**
- ❌ Requires location information (GPS or similar)
- ❌ Threshold selection is environment-dependent

---

#### **1.4.4 Location-Based Methods**

**Concept:** A node rebroadcasts only if its additional coverage area (area covered by it but NOT by the sender) exceeds a threshold.

```
Additional Coverage = Area(node's range) - Area(overlap with sender's range)

if Additional Coverage > threshold:
    rebroadcast
else:
    discard
```

#### **ASCII Diagram — Location-Based:**

```
     [Sender S]         [Node A]         [Node B]
     (  range  )    (   range  )      (  range   )
          |<----- overlap ----->|
                                    |<-- additional coverage -->|

A's additional coverage is small → don't rebroadcast
B's additional coverage is large → DO rebroadcast
```

**Advantages:**
- ✅ Most accurate — directly minimizes wasted coverage
- ✅ Provably reduces storm with high delivery ratio

**Disadvantages:**
- ❌ Requires location info for self AND sender
- ❌ More complex computation

---

#### **1.4.5 Neighbor Knowledge Methods — MPR (MultiPoint Relays)**

**Concept:** Each node maintains knowledge of its **2-hop neighborhood**. It selects a small set of 1-hop neighbors (called **MultiPoint Relays — MPRs**) such that every 2-hop neighbor is covered by at least one MPR.

Only MPR nodes are allowed to rebroadcast a packet — all other nodes discard it.

This approach is used in **OLSR (Optimized Link State Routing)**.

#### **MPR Selection Algorithm:**

```
Node X selects MPRs as follows:
1. Find all 2-hop neighbors of X (nodes reachable in 2 hops)
2. If a 2-hop neighbor is reachable via ONLY ONE 1-hop neighbor,
   that 1-hop neighbor MUST be an MPR.
3. Among remaining uncovered 2-hop neighbors, greedily select
   1-hop neighbors that cover the most uncovered 2-hop neighbors.
4. Repeat until all 2-hop neighbors are covered.
```

#### **ASCII Diagram — MPR:**

```
2-hop neighborhood of S:

       [N1]---[N4]
      /    \
[S]--[N2]---[N5]
      \    /
       [N3]---[N6]

S's 1-hop neighbors: N1, N2, N3
S's 2-hop neighbors: N4, N5, N6

MPR Selection:
- N4 only reachable via N1 → N1 is MPR
- N6 only reachable via N3 → N3 is MPR
- N5 reachable via N1 or N2 → N1 already MPR, so N5 covered
- MPR set = {N1, N3}  (N2 is NOT MPR)

Only N1 and N3 rebroadcast S's packets.
N2 receives but DISCARDS — no storm!
```

**Advantages:**
- ✅ Dramatically reduces number of rebroadcasting nodes
- ✅ Delivery guarantee maintained (MPRs cover all 2-hop neighbors)
- ✅ Used in OLSR — proven in practice

**Disadvantages:**
- ❌ Requires knowledge of 2-hop topology (HELLO messages needed)
- ❌ MPR set must be recomputed when topology changes
- ❌ Control overhead for maintaining neighbor tables

---

#### **Comparison Table: Broadcast Storm Solutions**

| Method | Info Required | Delivery Guarantee | Overhead | Best For |
|---|---|---|---|---|
| Simple Flooding | None | Yes | Very High | Sparse networks |
| Probability-based | None | No (probabilistic) | Low | Medium density |
| Counter-based | Duplicate count | Partial | Low | Dense networks |
| Distance-based | Location (self + sender) | Partial | Medium | GPS-enabled nodes |
| Location-based | Location (self + sender) | High | Medium-High | GPS-enabled nodes |
| MPR (Neighbor knowledge) | 2-hop topology | Yes | Medium | OLSR, dense networks |

---

## **Section 2: Multicasting in MANETs**

> PYQ: What is multicast? Explain any one application of multicast in detail. (May 2025, 8 marks)  
> PYQ: What is Multicasting? (Jul 2022, 2.5 marks)

### **2.1 What is Multicasting?**

**Multicasting** is a **one-to-many** communication model where packets from a single source are delivered to a **specific group** of nodes (multicast group members), not all nodes.

```
Unicast:    S ---------> D       (one source, one destination)
Broadcast:  S ---------> ALL     (one source, all nodes)
Multicast:  S ---------> {D1, D2, D3}  (one source, group members)
```

**Multicast Group:** A logical set of nodes identified by a **group address**. Nodes can join or leave the group dynamically.

**Applications of Multicasting:**
- Video conferencing (group call)
- Military tactical networks (team communication)
- Collaborative computing
- Software updates to a group of nodes

---

### **2.2 Challenges of Multicasting in MANETs**

Multicasting in fixed networks uses **multicast trees** (e.g., PIM, DVMRP). In MANETs, this is much harder:

1. **Dynamic Topology:** Node mobility causes frequent link breaks → multicast trees/meshes break and need repair.
2. **No Fixed Infrastructure:** No multicast-capable routers — every node must participate.
3. **Asymmetric Links:** Wireless links may be one-directional.
4. **Limited Resources:** Battery power and bandwidth are limited.
5. **Decentralized Group Management:** No central server to track group membership.
6. **Scalability:** As group size or network size grows, overhead increases.
7. **Merging/Partitioning:** Network partitions may split the multicast tree.

---

### **2.3 Multicast Routing Approaches**

Two main approaches exist for multicast routing in MANETs:

#### **Tree-Based Multicast Routing**

A **shared or source-based tree** connects the source to all group members. Packets are forwarded along the tree.

```
        [Source S]
           |
          [A]
         / \
       [B]  [C]
       |      \
      [D1]   [D2]

Tree rooted at S, leaves are multicast group members.
Packets flow down the tree branches.
```

**Types:**
- **Source Tree:** Separate tree per source (optimal paths but high state)
- **Shared Tree:** One tree for all sources (less state, sub-optimal paths)

**Protocols:** MAODV (Multicast AODV), AMRIS, MZR

**Pros:**
- ✅ Efficient bandwidth usage (no duplicate packets on shared links)
- ✅ Simple packet forwarding (just follow the tree)

**Cons:**
- ❌ Fragile — node mobility breaks the tree
- ❌ Tree repair takes time → increased latency
- ❌ Single point of failure (tree root or key intermediate node)

---

#### **Mesh-Based Multicast Routing**

Instead of a tree, nodes form a **mesh (graph with multiple paths)** connecting source and group members. Multiple redundant paths exist.

```
        [Source S]
       / \
     [A]  [B]
     |  X  |
    [C]  [D]
       \ /
       [E] (member)

Mesh: multiple paths from S to E.
If link A-C breaks, packets can go via A-D or B-D.
```

**Protocols:** ODMRP (On-Demand Multicast Routing Protocol)

**Pros:**
- ✅ Robust to node mobility and link failures
- ✅ Multiple paths → better packet delivery ratio

**Cons:**
- ❌ Duplicate packets (same packet may arrive via multiple paths)
- ❌ Higher bandwidth usage than trees

---

### **2.4 MAODV — Multicast AODV**

**MAODV** is an extension of the AODV unicast routing protocol to support multicast. It maintains a **shared multicast tree** rooted at a **multicast group leader**.

#### **Key Concepts:**

- **Multicast Group Leader (MGL):** The node that roots the shared tree. Elected among current members.
- **Multicast Group Sequence Number (MGSN):** Tracks freshness of multicast tree info.
- **Multicast Tree:** A spanning tree connecting source and all group members.

#### **MAODV Route Discovery:**

```
Node wants to JOIN multicast group G:
  1. Broadcast RREQ with multicast group address G
  2. An existing member of G (or the MGL) replies with RREP
  3. The joining node connects to the tree via the replying node
  4. Tree is updated (new branch added)

Node wants to SEND to group G:
  1. If node is on the tree → forward packet along tree branches
  2. If node is NOT on tree → unicast RREQ to find tree, then send
```

#### **ASCII Diagram — MAODV Join:**

```
Existing Multicast Tree:
     [MGL]---[A]---[M1]
               \
               [M2]

New node N wants to join:
  N --> RREQ (group G) --> A --> MGL

  MGL/A sends RREP back to N:
  MGL --> RREP --> A --> N

  Tree updated:
     [MGL]---[A]---[M1]
               \
               [M2]
                \
                [N] ← new branch added
```

#### **Tree Maintenance in MAODV:**

- Nodes send **periodic HELLO** messages
- If HELLO is missed → link break detected
- **Prune:** Remove broken branches
- **Graft/Repair:** Find new path to reconnect

**Advantages of MAODV:**
- ✅ Extends proven AODV protocol
- ✅ On-demand — no overhead when no multicast traffic
- ✅ Works for both unicast and multicast

**Disadvantages:**
- ❌ Tree fragile under mobility
- ❌ MGL is a single point of failure
- ❌ Tree repair can be slow → packet loss during repair

---

### **2.5 ODMRP — On-Demand Multicast Routing Protocol**

**ODMRP** is a **mesh-based**, on-demand multicast protocol. Instead of a tree, it creates a **forwarding group** — a subset of nodes that forward multicast packets.

#### **Key Concepts:**

- **Forwarding Group:** Set of nodes that forward multicast packets (not just group members — also intermediate nodes)
- **Join Query:** Broadcast by source to discover group members and build mesh
- **Join Reply:** Unicast from group members back to source
- **Mesh:** Multiple overlapping paths from source to all members

#### **ODMRP Operation — Two Phases:**

**Phase 1: Route Discovery (Join Query)**

```
1. Source S periodically broadcasts JOIN QUERY
   (contains: source IP, multicast group, sequence number)
2. Each intermediate node:
   - Records upstream node in routing table
   - Rebroadcasts JOIN QUERY (if not seen before)
3. JOIN QUERY floods entire network
```

**Phase 2: Join Reply (Mesh Creation)**

```
4. Group members that receive JOIN QUERY:
   - Generate JOIN REPLY (unicast back to upstream node)
5. Each intermediate node receiving JOIN REPLY:
   - Marks itself as FORWARDING GROUP member
   - Unicasts JOIN REPLY to its upstream node
6. Process continues until JOIN REPLY reaches source S
7. Result: Forwarding group = set of nodes that relay multicast data
```

#### **ASCII Diagram — ODMRP Join Query / Reply:**

```
Network:
  S ---A---B---M1 (member)
  |         |
  C ---D ---M2 (member)

Phase 1: JOIN QUERY floods from S
  S→A, S→C (broadcast)
  A→B, C→D (rebroadcast)
  B→M1, D→M2 (reaches members)

Phase 2: JOIN REPLY flows back
  M1→B→A→S  (B and A become forwarding group)
  M2→D→C→S  (D and C become forwarding group)

Forwarding Group = {A, B, C, D}
(These nodes forward multicast data from S)

Data Delivery:
  S multicasts → forwarding group relays to M1 and M2
```

#### **ODMRP Refresh:**

- Source periodically sends JOIN QUERY (even if group unchanged)
- This refreshes the forwarding group and adapts to topology changes
- Nodes not included in a refresh cycle remove themselves from forwarding group

**Advantages of ODMRP:**
- ✅ Robust to node mobility — mesh has redundant paths
- ✅ No tree maintenance overhead
- ✅ High packet delivery ratio even with mobility

**Disadvantages:**
- ❌ Duplicate packet delivery (multiple paths)
- ❌ Periodic JOIN QUERY floods → overhead
- ❌ Forwarding group includes non-members → energy waste

---

### **2.6 Comparison: Tree-Based vs Mesh-Based Multicasting**

| Feature | Tree-Based (MAODV) | Mesh-Based (ODMRP) |
|---|---|---|
| **Structure** | Spanning tree | Forwarding mesh |
| **Redundancy** | No redundant paths | Multiple redundant paths |
| **Robustness to mobility** | Low (tree breaks easily) | High (mesh survives failures) |
| **Packet delivery ratio** | Lower under mobility | Higher under mobility |
| **Bandwidth efficiency** | High (no duplicates) | Lower (duplicate packets) |
| **Latency** | Low when tree stable | Low |
| **Control overhead** | Moderate (tree repair) | Moderate (periodic floods) |
| **State maintenance** | Per-node tree state | Forwarding group flag |
| **Scalability** | Moderate | Good |
| **Best for** | Low mobility scenarios | High mobility scenarios |

---

## **Section 3: Geocasting in MANETs**

> PYQ: What is Geocasting? Explain any one application of Geocasting in detail. (Dec 2025, 8 marks)  
> PYQ: What is Geocasting? (May 2023, 2.5 marks)

### **3.1 What is Geocasting?**

**Geocasting** is a special form of multicasting where the **multicast group is defined by geographic location** rather than explicit group membership. A packet is delivered to **all nodes within a specified geographic region**.

```
Multicast:  Deliver to nodes that explicitly JOINED group G
Geocast:    Deliver to ALL nodes currently located within region R
```

**Geographic Region Types:**
- Circle (center + radius)
- Rectangle (bounding box)
- Polygon (arbitrary shape)

**Key Characteristic:** The group is **implicit** — any node inside the region is automatically a recipient. No explicit join/leave required.

---

### **3.2 How Geocasting Differs from Multicasting**

| Feature | Multicasting | Geocasting |
|---|---|---|
| **Group definition** | Explicit (nodes join) | Implicit (geographic region) |
| **Group membership** | Static until leave | Dynamic (nodes move in/out) |
| **Routing basis** | Group address | Geographic coordinates |
| **Location required** | No | Yes (GPS or localization) |
| **Scalability** | Group size dependent | Region size dependent |
| **Application** | Group communication | Location-aware services |

---

### **3.3 GeoTORA Protocol**

**GeoTORA** is a geocasting protocol that combines **geographic information** with the **TORA (Temporally Ordered Routing Algorithm)** protocol.

#### **Key Concepts:**

- Uses **DAG (Directed Acyclic Graph)** rooted at the destination region
- Packets flow "downhill" toward the geocast region
- **Height metric:** Nodes closer to the geocast region have lower height
- **Routing rule:** Forward packets to neighbors with lower height

#### **GeoTORA Operation:**

```
1. Source S sends geocast packet to region R
2. GeoTORA establishes a DAG toward region R:
   - Nodes inside R have height = 0 (destination)
   - Other nodes have height = geographic distance to R
3. Packet forwarded from higher-height to lower-height nodes
4. When packet reaches region R, it's delivered to all nodes inside

ASCII:
  S (h=5) --> A (h=3) --> B (h=1) --> [Region R, h=0]
               \                          |
               C (h=2) ---------> D (h=1)

Packets flow toward decreasing height → toward region R
```

**Advantages of GeoTORA:**
- ✅ Adapts to network topology (TORA handles link failures)
- ✅ Multiple paths to region (DAG structure)

**Disadvantages:**
- ❌ Requires location information
- ❌ Complex height metric computation
- ❌ TORA convergence can be slow

---

### **3.4 LBM — Location-Based Multicast**

**LBM (Location-Based Multicast)** is a simpler geocasting approach that uses geographic forwarding with a **restricted forwarding zone**.

#### **Key Concept — Forwarding Zone:**

```
Source S          Region R (geocast target)
  *                      [######]
  |                      [######]
  |<---- forwarding zone ------->|

Only nodes within the forwarding zone relay the geocast packet.
Nodes outside the zone discard it.
```

**Forwarding Zone:** A rectangle (or region) containing both the source and the geocast destination region. Only nodes inside this zone participate in forwarding.

#### **LBM Operation:**

```
1. Source S broadcasts geocast packet with:
   - Target region R coordinates
   - Forwarding zone boundaries
2. A receiving node checks:
   a. Is the packet already received? → discard
   b. Am I inside the forwarding zone? → rebroadcast
   c. Am I inside target region R? → deliver to application
   d. Otherwise → discard
3. Flooding is restricted to the forwarding zone
4. Result: geocast packet delivered to all nodes in R
```

#### **ASCII Diagram — LBM:**

```
   S                  Forwarding Zone               R
   *===========================================[####]
   |  Nodes here relay packets                [####]
   |                                          [####]
   |
   Nodes outside zone (above/below line) → discard
```

**Advantages of LBM:**
- ✅ Simple — restricted flooding within zone
- ✅ No per-node state required
- ✅ Efficient — limits flood to relevant area

**Disadvantages:**
- ❌ Rectangular zone may be too large or too small
- ❌ Sparse zone → packet may not reach all of R
- ❌ Requires location info

---

### **3.5 Applications of Geocasting**

1. **Local Advertising:** Broadcast advertisements to nodes within a shopping mall, airport, or stadium zone.
2. **Emergency Alerts:** Send disaster warnings or evacuation instructions to nodes in an affected geographic area.
3. **Traffic Information:** Alert vehicles in a specific road segment about accidents, congestion, or speed limits (VANETs).
4. **Military Operations:** Send tactical orders to all soldiers within an operation zone.
5. **Environmental Monitoring:** Query sensor nodes deployed in a specific geographic field.
6. **Location-based games:** Notify players within a virtual game zone.

---

## **Section 4: TCP Protocol Overview**

> PYQ: What is TCP protocol? (Dec 2023, 2.5 marks)  
> PYQ: Explain Transmission control protocol. (May 2023, 8 marks; Jul 2022, 7 marks)  
> PYQ: What is TCP? Discuss with an example TCP over Ad-hoc wireless networks. (Dec 2023, 15 marks)

### **4.1 TCP Basics**

**TCP (Transmission Control Protocol)** is a **connection-oriented, reliable, full-duplex** transport layer protocol defined in **RFC 793**.

#### **Key Features of TCP:**

| Feature | Description |
|---|---|
| **Connection-oriented** | Requires handshake before data transfer |
| **Reliable delivery** | Guarantees all data arrives, in order |
| **Flow control** | Receiver controls sender rate (receive window) |
| **Congestion control** | Sender adapts to network congestion |
| **Error detection** | Checksums detect corruption |
| **Byte-stream** | Delivers ordered, contiguous byte stream |
| **Full-duplex** | Simultaneous bidirectional data flow |

---

### **4.2 TCP Three-Way Handshake**

```
Client                      Server
  |                            |
  |------- SYN (seq=x) ------->|   Step 1: Client initiates
  |                            |
  |<-- SYN-ACK (seq=y,ack=x+1)-|   Step 2: Server acknowledges
  |                            |
  |------- ACK (ack=y+1) ----->|   Step 3: Client confirms
  |                            |
  |====== DATA TRANSFER =======|
  |                            |

SYN = Synchronize sequence numbers
ACK = Acknowledge receipt
After 3-way handshake, connection established.
```

---

### **4.3 TCP Congestion Control**

TCP's **fundamental assumption:** Packet loss = network congestion.

TCP uses the **congestion window (cwnd)** to limit the number of unacknowledged packets in flight.

#### **TCP Congestion Control Phases:**

```
cwnd
 ^
 |          /
 |        /   Congestion Avoidance (linear)
 |      /     (+1 per RTT)
 |    /
 |  / Slow Start (exponential, +1 per ACK)
 | /
 |/___________________________________________> time
  ssthresh
```

#### **Phase 1: Slow Start**

```
Initial: cwnd = 1 MSS (Maximum Segment Size)
On each ACK received: cwnd += 1 MSS
→ cwnd doubles every RTT (exponential growth)
Until: cwnd >= ssthresh (slow start threshold)
```

#### **Phase 2: Congestion Avoidance**

```
When cwnd >= ssthresh:
On each ACK received: cwnd += 1/cwnd (approximately)
→ cwnd increases by ~1 MSS per RTT (linear growth)
Until: packet loss detected (timeout or triple duplicate ACK)
```

#### **Phase 3: Fast Retransmit**

```
Trigger: 3 duplicate ACKs received (same ACK repeated 3 times)
Interpretation: A packet was lost, but later packets arrived.
Action: Immediately retransmit the lost segment (don't wait for timeout)
```

#### **Phase 4: Fast Recovery (TCP Reno)**

```
After fast retransmit (3 dup ACKs):
  ssthresh = cwnd / 2
  cwnd = ssthresh + 3 MSS
  Continue in Congestion Avoidance
(NOT back to Slow Start — network not fully congested)

After Timeout:
  ssthresh = cwnd / 2
  cwnd = 1 MSS
  Restart Slow Start (severe penalty)
```

#### **Complete TCP Congestion Control State Machine:**

```
         START
           |
           v
     [Slow Start]
     cwnd=1, grows exponentially
           |
    cwnd >= ssthresh
           |
           v
  [Congestion Avoidance]
     cwnd grows linearly
           |
    +----- +-------+
    |               |
3 dup ACKs       Timeout
    |               |
    v               v
[Fast Retransmit] ssthresh=cwnd/2
    |             cwnd=1
ssthresh=cwnd/2    |
cwnd=ssthresh+3    v
    |         [Slow Start]
    v
[Fast Recovery]
cwnd grows from ssthresh
```

---

## **Section 5: TCP and MANETs — Problems**

### **5.1 Why TCP Performs Poorly in MANETs**

TCP was designed for **wired networks** with these assumptions:
1. Packet loss is **rare** and caused by **congestion**
2. **Bidirectional symmetric links**
3. **Stable paths** that don't change frequently
4. **Low bit error rate** on links

In **MANETs**, ALL these assumptions are violated. This causes TCP to behave suboptimally or catastrophically.

---

### **5.2 Problem 1: Mobility-Induced Route Failures**

```
Scenario:
  S ---TCP---> A ----> B ----> D

  Node B moves away from A → Link A-B breaks
  
  A cannot forward packets → buffers fill → packets dropped
  Routing protocol (AODV/DSR) begins route discovery

  TCP sees: no ACKs from D
  TCP interprets: CONGESTION! (but it's actually a link failure)
  TCP action:
    - Reduces cwnd aggressively
    - Triggers slow start
    - May time out and reduce cwnd to 1

  Route is repaired: S--A--C--B--D (new path)
  But TCP is now in slow start:
    → Long time to recover to full speed
    → Throughput severely degraded unnecessarily
```

#### **ASCII Diagram — Route Failure vs TCP Behavior:**

```
Time --->
t=0:  S ======data=====> A --> B --> D  (normal operation)
t=1:  B moves,  A-B link BREAKS
t=2:  No ACKs reach S
t=3:  TCP: "Congestion!" → reduces cwnd (WRONG decision)
t=4:  AODV finds new route: A-C-D
t=5:  Route restored but TCP cwnd = 1 → slow start
t=6-10: TCP slowly rebuilds cwnd → wasted time
t=10: Full throughput restored (much later than necessary)

Throughput:
  ████████████████░░░░░░░░░░░░░████  (gap during mobility)
                  ^ link break  ^ recovery complete
```

---

### **5.3 Problem 2: Wireless Link Errors (Bit Errors)**

**Wireless links have high Bit Error Rate (BER)** compared to wired links due to:
- Signal fading
- Interference
- Multipath propagation
- Noise

```
When a wireless bit error causes packet corruption:
  - Packet is dropped at MAC layer
  - TCP sees: no ACK (or duplicate ACK)
  - TCP interprets: CONGESTION!
  - TCP reduces cwnd → WRONG! (error, not congestion)
  - Link is not congested at all
  - Performance degrades unnecessarily
```

Even a **1% bit error rate** on each of 5 hops = only (0.99)^5 ≈ 95% success per packet → 5% loss → TCP constantly throttled.

---

### **5.4 Problem 3: Hidden Terminal Problem**

> PYQ: Explain the hidden-terminal problem and the exposed-terminal problem. How can it be avoided? (Dec 2025, 7 marks)

```
Topology:
  A   C   B
  *   *   *
  |<R>|<R>|

A is out of range of B (|R| = radio range)
A cannot hear B's transmissions.

Scenario:
  A sends to C (for TCP connection S-A-C-D)
  B also sends to C simultaneously
  C: COLLISION! Both packets lost.
  
  TCP sees: ACKs lost → interprets CONGESTION
  TCP reduces cwnd → WRONG! It's a collision.
  Both A and B keep retransmitting → more collisions
  This is the "hidden terminal" causing TCP misbehavior.
```

---

### **5.5 Problem 4: Route Oscillation**

```
Routing protocol switches between two routes due to mobility:
  Route 1: S-A-B-D (5 hops, RTT = 50ms)
  Route 2: S-C-D   (2 hops, RTT = 20ms)

  Packets from S take different routes:
  P1, P2 go via route 1 (50ms delay)
  P3, P4 go via route 2 (20ms delay)

  D receives: P3, P4 (early), P1, P2 (late) → OUT OF ORDER

  TCP at D: sends duplicate ACKs for P1, P2 (since P3,P4 received first)
  TCP at S: sees 3 dup ACKs → fast retransmit P1, P2
  → SPURIOUS RETRANSMITS (P1, P2 were not lost!)
  → Wasted bandwidth + unnecessary cwnd reduction
```

---

### **5.6 Problem 5: Asymmetric Routes**

```
Forward path:  S-->A-->B-->D  (high bandwidth, 3 hops)
Reverse path:  D-->X-->Y-->Z-->S  (low bandwidth, 4 hops)

TCP ACKs flow on reverse path.
If reverse path is bottleneck:
  - ACKs arrive slowly or get dropped
  - TCP at S: thinks congestion → reduces cwnd
  - Data pipe S→D underutilized despite high-bandwidth forward path

Also: ACK compression (many ACKs queued) → burst of ACKs
→ S sends burst of data → overflow at bottleneck
```

---

### **5.7 Summary: TCP Misbehavior in MANETs**

| Problem | Root Cause | TCP Interpretation | Actual Problem | Effect |
|---|---|---|---|---|
| Route failure | Node mobility | Congestion | Link break | Unnecessary cwnd reduction |
| Bit errors | Wireless channel | Congestion | Transmission error | Unnecessary cwnd reduction |
| Hidden terminal | Wireless topology | Congestion | Collision | Thrashing, retransmits |
| Route oscillation | Dynamic routing | Congestion | Reordering | Spurious retransmits |
| Asymmetric routes | Wireless topology | Congestion | Bandwidth mismatch | Underutilization |

---

## **Section 6: Solutions for TCP over Ad Hoc**

> PYQ: Discuss different solutions for TCP over Adhoc network in detail. (May 2023, Jul 2022, 15 marks)  
> PYQ: Explain any two variations in TCP protocol with their advantages and disadvantages. (May 2025, Dec 2025, 7 marks)  
> PYQ: What is TCP? Discuss with an example TCP over Ad-hoc wireless networks. (Dec 2023, 15 marks)

### **6.1 Indirect TCP (I-TCP)**

**Concept:** Split the TCP connection at a **base station** (or proxy node at the boundary between wired and wireless). The end-to-end TCP connection is broken into two separate connections:

1. **Fixed TCP connection:** Source ↔ Base Station (standard TCP over wired network)
2. **Wireless TCP connection:** Base Station ↔ Mobile Host (optimized TCP for wireless)

#### **ASCII Diagram — I-TCP Architecture:**

```
  [Server S]                [Base Station / Proxy]              [Mobile D]
      |                              |                               |
      |<====== Standard TCP ========>|<===== Modified TCP ==========>|
      |    (wired, standard          |    (wireless, modified        |
      |     congestion control)      |     for bit errors)           |

Two separate TCP connections — server doesn't know about wireless segment.
```

#### **I-TCP Operation:**

```
1. Server S establishes TCP connection to Base Station (BS)
2. BS establishes separate TCP connection to Mobile D
3. BS acts as PROXY:
   - Receives data from S (standard TCP ACK back to S)
   - Forwards data to D (over wireless TCP)
4. If wireless link has errors:
   - BS handles retransmissions locally
   - S does NOT see the wireless errors → S's TCP undisturbed
5. BS buffers data until D confirms receipt
```

**Advantages:**
- ✅ Wired TCP is completely isolated from wireless problems
- ✅ Easy to deploy (no changes to server or client)
- ✅ Wireless segment can be optimized independently

**Disadvantages:**
- ❌ **Breaks TCP's end-to-end semantics** — S gets ACK before D receives data
- ❌ BS is a bottleneck and single point of failure
- ❌ Requires Base Station — not suitable for pure MANETs (no infrastructure)
- ❌ High BS overhead (must buffer and manage two connections)
- ❌ Does not work in multi-hop MANETs (only infrastructure mode)

---

### **6.2 Snoop Protocol**

**Concept:** A **snooping agent** at the base station monitors TCP packets transparently (TCP is unmodified). It **caches TCP packets** and performs **local retransmissions** when it detects packet loss on the wireless link.

#### **ASCII Diagram — Snoop Protocol:**

```
  [Server S]    [Base Station (Snoop Agent)]    [Mobile D]
      |                    |                         |
      |====== data =======>|--- data -------------->  |
      |                    |   (snoop caches copy)    |
      |                    |                         |
      |                    |<--- NACK/dup ACK --------|  (wireless loss)
      |                    |                         |
      |                    |--- RETRANSMIT ---------->|  (local retransmit!)
      |                    |                         |
      |                    |<-- ACK ------------------|
      |<====== ACK ========|                         |
      |  (S gets ACK                                 |
      |  S does NOT see wireless loss)               |
```

#### **Snoop Agent Behavior:**

```
Snoop agent monitors:
  - Data packets from S to D → cache them
  - ACKs from D to S → process them

On detecting loss (dup ACK from D or timeout):
  - Locally retransmit cached packet to D
  - Suppress duplicate ACKs from reaching S
    (so S doesn't think there's congestion)

If loss is due to:
  - Wireless error → snoop handles locally (S undisturbed)
  - Congestion → snoop lets dup ACK pass to S (S reduces cwnd)
```

**Advantages:**
- ✅ **Transparent** — no changes to server or client TCP
- ✅ Fast local recovery from wireless errors
- ✅ S's congestion control undisturbed by wireless losses
- ✅ Maintains end-to-end TCP semantics (mostly)

**Disadvantages:**
- ❌ Doesn't work if packets are **encrypted** (can't snoop encrypted TCP)
- ❌ Requires infrastructure (base station)
- ❌ Snoop agent adds complexity and must handle soft handoff
- ❌ Doesn't address mobility-induced route failures in pure MANETs
- ❌ Limited to single-hop wireless (base station to mobile)

---

### **6.3 TCP-ELFN — Explicit Link Failure Notification**

**Concept:** Extend routing protocol to send an **Explicit Link Failure Notification (ELFN)** to TCP when a route failure is detected. This allows TCP to distinguish between congestion and link failure.

#### **TCP-ELFN Operation:**

```
Normal TCP:
  Route fails → TCP sees no ACKs → assumes CONGESTION → reduces cwnd

TCP-ELFN:
  Route fails → Routing protocol (AODV/DSR) detects failure
              → Sends ELFN message to TCP sender
              → TCP knows: this is a ROUTE FAILURE, not congestion

TCP behavior on receiving ELFN:
  1. TCP enters "standby mode"
     - Freezes cwnd (does NOT reduce it)
     - Stops retransmit timer
     - Saves current cwnd and ssthresh
  2. TCP periodically sends PROBE packets to check if route restored
  3. When route restored:
     - Resume with SAME cwnd (not slow start!)
     - → Much faster recovery than standard TCP
```

#### **ASCII Diagram — TCP-ELFN:**

```
Time -->
t=0:  S ----data---> A -->B-->D
t=1:  Link B-D breaks
t=2:  AODV detects failure → sends ELFN to S
t=3:  S receives ELFN:
        TCP state: FREEZE cwnd, enter standby
        No cwnd reduction! (knows it's link failure, not congestion)
t=4:  AODV finds new route: A-C-D
t=5:  S sends PROBE packet, gets ACK (new route works)
t=6:  S resumes with SAME cwnd → fast recovery!

Without ELFN:  throughput = [████░░░░░░░░░░░████]  (long recovery)
With ELFN:     throughput = [████░░░████]  (short pause, fast resume)
```

**Advantages:**
- ✅ No cwnd reduction on link failure → fast recovery
- ✅ Correctly attributes cause of packet loss
- ✅ Simple to implement at routing layer

**Disadvantages:**
- ❌ Requires modification to both TCP and routing protocol
- ❌ ELFN may not always arrive (if route completely broken)
- ❌ Doesn't help with random bit errors on wireless links
- ❌ Probe period adds latency before recovery

---

### **6.4 TCP-FEEDBK**

**Concept:** The routing layer provides **explicit feedback** to the TCP layer about the state of the network. Based on this feedback, TCP adjusts its behavior appropriately.

#### **TCP-FEEDBK Feedback Types:**

```
Feedback messages from routing layer to TCP:

1. ROUTE_BREAK: Route to destination broken
   TCP response: Freeze cwnd, stop retransmit timer, wait for route

2. ROUTE_RESTORED: New route found to destination
   TCP response: Resume with same cwnd (no slow start)

3. CONGESTION: Routing layer detects congestion (queue buildup)
   TCP response: Reduce cwnd (standard congestion response)

4. LINK_ERROR: Wireless bit error (not congestion)
   TCP response: Retransmit without reducing cwnd
```

**Advantages:**
- ✅ Most accurate — routing layer has precise failure info
- ✅ Handles multiple failure modes differently
- ✅ Can prevent both unnecessary cwnd reduction AND missed congestion signals

**Disadvantages:**
- ❌ Complex cross-layer design — tight coupling between TCP and routing
- ❌ Significant implementation changes needed
- ❌ Routing layer must classify failures (congestion vs link error) — not always easy

---

### **6.5 ATCP — Ad Hoc TCP**

**Concept:** ATCP inserts an **intermediate layer between TCP and IP** that monitors network state and modifies TCP behavior by using:
- **ECN (Explicit Congestion Notification)**
- **NDP (Network Delay Probing)**

#### **ATCP Architecture:**

```
  Application
      |
    TCP (unmodified)
      |
   [ATCP Layer]  ← new layer — monitors and controls TCP
      |
     IP
      |
  Network
```

#### **ATCP Network States and Actions:**

ATCP defines 4 network states and reacts accordingly:

```
State 1: NORMAL
  Condition: ACKs arriving normally
  Action: Let TCP run normally (no intervention)

State 2: CONGESTION
  Condition: ECN bit set in received packets
             (network router detected congestion)
  Action: Let TCP reduce cwnd normally
          (correct TCP behavior for real congestion)

State 3: LINK FAILURE / DISCONNECTION
  Condition: NDP detects no route to destination
  Action: PUT TCP in PERSIST MODE
            - freeze cwnd
            - stop retransmit timer
            - no cwnd reduction
          Wait for route restoration

State 4: PACKET REORDERING
  Condition: Out-of-order packets arrive (not loss)
  Action: Suppress duplicate ACKs
          Prevent spurious fast retransmit
```

#### **ASCII Diagram — ATCP State Machine:**

```
         +----------+
    +--->|  NORMAL  |<---+
    |    +----------+    |
    |         |          |
  Route    ECN set    Route
 restored    |        fails
    |         v          |
    |   +----------+     |
    |   |CONGESTION|     |
    |   +----------+     |
    |                    |
    |    +----------+    |
    +----| LINK FAIL|----+
         +----------+
              |
         TCP in persist
         mode (frozen)
```

**Advantages:**
- ✅ Correctly distinguishes congestion from link failure from reordering
- ✅ Uses standard ECN (no new protocol needed)
- ✅ No modification to TCP or IP layers
- ✅ Works in pure MANETs (no infrastructure needed)
- ✅ Handles all major TCP problems in MANETs

**Disadvantages:**
- ❌ Requires ECN support in network routers/nodes
- ❌ ATCP layer adds complexity
- ❌ NDP adds overhead for continuous probing

---

### **6.6 Comparison Table: Solutions for TCP over Ad Hoc**

| Solution | Key Mechanism | TCP Modified? | Routing Modified? | Infrastructure Needed? | Handles Bit Errors? | Handles Route Failure? | Handles Reordering? |
|---|---|---|---|---|---|---|---|
| **I-TCP** | Split connection at proxy | No | No | Yes (BS) | Yes | Partial | Yes |
| **Snoop** | Cache + local retransmit | No | No | Yes (BS) | Yes | No | No |
| **TCP-ELFN** | Explicit failure notification | Yes | Yes | No | No | Yes | No |
| **TCP-FEEDBK** | Routing feedback to TCP | Yes | Yes | No | Yes | Yes | Partial |
| **ATCP** | ECN + NDP, intermediate layer | No | No | No | Partial | Yes | Yes |

---

### **6.7 Summary: Which Solution to Use?**

```
Decision Tree:

Is infrastructure (base station) available?
  YES → Use Snoop (transparent) or I-TCP (simple)
  NO  → Pure MANET: use ATCP or TCP-ELFN

Is encryption used?
  YES → Can't use Snoop → use ATCP or TCP-ELFN
  NO  → Snoop is a good choice

Is congestion the primary concern?
  YES → Standard TCP (with ECN)
  NO  → Route failures dominate → ATCP or TCP-ELFN

Require no protocol changes?
  YES → ATCP (new layer, no changes to TCP/IP)
  Need cross-layer → TCP-FEEDBK
```

---

## **Quick Revision Points**

### Broadcasting
- **Simple Flooding:** Node rebroadcasts every new packet — guaranteed delivery, but causes broadcast storm
- **Broadcast Storm:** Redundant transmissions + collisions + contention in dense networks
- **Broadcast Storm Problem** was formally named and studied in 1999 research on ad hoc networks
- **5 Solutions:** Probability-based, Counter-based, Distance-based, Location-based, Neighbor Knowledge (MPR)
- **MPR (OLSR):** Select minimum set of 1-hop neighbors that cover all 2-hop neighbors → only MPRs rebroadcast

### Multicasting
- **Tree-based (MAODV):** Shared multicast tree, efficient but fragile under mobility
- **Mesh-based (ODMRP):** Forwarding group via JOIN QUERY/REPLY floods, robust but duplicate packets
- **ODMRP phases:** (1) JOIN QUERY floods from source, (2) JOIN REPLY unicast back → forwarding group created
- **Tree vs Mesh:** Tree = efficient; Mesh = robust

### Geocasting
- **Geocasting:** Deliver to all nodes in a geographic region (implicit group)
- **GeoTORA:** DAG-based, height = distance to region, forward toward lower height
- **LBM:** Forwarding zone (rectangle) — only nodes inside zone relay packets
- **Applications:** Emergency alerts, local ads, VANET traffic info

### TCP Basics
- **Three-way handshake:** SYN → SYN-ACK → ACK
- **Slow Start:** cwnd doubles per RTT (exponential)
- **Congestion Avoidance:** cwnd +1 per RTT (linear)
- **Fast Retransmit:** 3 dup ACKs → retransmit immediately
- **KEY ASSUMPTION:** Packet loss = congestion (WRONG in MANETs!)

### TCP Problems in MANETs
1. **Mobility:** Route failure → TCP wrongly reduces cwnd
2. **Bit errors:** Wireless errors → TCP wrongly reduces cwnd
3. **Hidden terminal:** Collisions → TCP triggered response
4. **Route oscillation:** Reordering → spurious retransmits
5. **Asymmetric routes:** ACK bottleneck → data pipe underutilized

### TCP Solutions
- **I-TCP:** Split at base station — isolates wired from wireless TCP
- **Snoop:** Cache at BS, local retransmit, suppress dup ACKs
- **TCP-ELFN:** Routing notifies TCP of link failure → freeze cwnd
- **TCP-FEEDBK:** Routing provides typed feedback (route break/restore/congestion/error)
- **ATCP:** Layer between TCP and IP; uses ECN + NDP; 4 states (Normal/Congestion/LinkFail/Reorder)

---

## **Expected Exam Questions**

### **15-mark Questions**

1. What is TCP? Discuss with an example TCP over Ad-hoc wireless networks. *(Dec 2023)*
2. Discuss different solutions for TCP over Adhoc network in detail. *(May 2023, Jul 2022)*
3. Explain Broadcast storm problem and Transmission control protocol. *(May 2023: 7+8, Jul 2022: 7+8)*

### **7–8 mark Questions**

1. What is broadcast storm problem? How to avoid this problem? *(May 2025)*
2. What is multicast? Explain any one application of multicast in detail. *(May 2025)*
3. What is Geocasting? Explain any one application of Geocasting in detail. *(Dec 2025)*
4. Explain the hidden-terminal problem and the exposed-terminal problem. How can it be avoided? *(Dec 2025)*
5. Explain any two variations in TCP protocol with their advantages and disadvantages. *(May 2025, Dec 2025)*

### **Short Answer (2.5–3 marks)**

1. What is broadcast storm problem? *(Dec 2025)*
2. What is TCP protocol? *(Dec 2023)*
3. What is Geocasting? *(May 2023)*
4. What is Multicasting? *(Jul 2022)*

---

_These notes were compiled by [Deepak Modi](https://deepakmodi.dev)_  
_Last updated: May 2026_
