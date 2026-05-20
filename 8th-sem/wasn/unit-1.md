---
title: "Unit 1: Introduction to Ad Hoc Networks"
description: "MANET Characteristics, Applications, Challenges, and Routing Algorithms (Topology-based, Position-based, and Other Routing)"
author: "Deepak Modi"
date: "2026-05-10"
pdfUrl: ""
---

## Syllabus:

**Introduction to Ad Hoc Networks:** Characteristics of MANETs, Applications of MANETs and challenges of MANETs - Routing in MANETs: Criteria for classification, Taxonomy of MANET routing algorithms, Topology based routing algorithms, Position based routing algorithms, Other routing algorithms.

---

## 🎯 PYQ Analysis for Unit 1

### **High Priority Topics** (15 marks questions)

1. **Characteristics & Applications of MANETs** — (May 2023: 15 marks, Dec 2023: 15 marks, Jul 2022: 15 marks)
2. **Applications + Challenges of MANETs** — (Dec 2023: 15 marks, Jul 2022: 15 marks)
3. **Routing Algorithms of MANETs / Routing Taxonomy** — (Jul 2022: 15 marks, May 2025: 8+7=15)
4. **Position-Based Routing Algorithms** — (Dec 2023: 15 marks)
5. **Characteristics of Wireless Channel** — (Dec 2023: 15 marks)
6. **Challenges in Designing Routing Algorithms** — (Dec 2025: 8 marks)
7. **Demand Routing Protocol (Reactive)** — (Dec 2025: 7 marks)

### **Medium Priority Topics** (Short answers)

1. **Characteristics of MANET** — Dec 2025 (2.5 marks)
2. **Reactive vs Proactive Routing** — Dec 2025, May 2025, Dec 2023 (2.5–3 marks)
3. **Hidden Terminal Problem** — May 2025 (3 marks)
4. **Routing Table** — May 2025 (3 marks)
5. **Routing Layer** — May 2023 (2.5 marks)
6. **MANET** — May 2023, Jul 2022 (2.5 marks)
7. **Issues in Adhoc Wireless Sensor Network** — Dec 2025 (8 marks)

---

## **Section 1: Introduction to Ad Hoc Networks**

### **1.1 What is an Ad Hoc Network?**

**Definition:**

An **Ad Hoc Network** is a **self-organizing, decentralized wireless network** in which mobile nodes communicate with each other **directly** (or via intermediate nodes) without relying on any **fixed infrastructure** such as base stations, access points, or wired backbones.

> The term "ad hoc" is Latin for **"for this purpose"** — implying the network is formed on-the-fly, temporarily, for a specific purpose.

**Key Idea:**

In a traditional **infrastructure-based network** (e.g., Wi-Fi with a router), every device connects to a central access point. In an **ad hoc network**, there is **no central controller** — every node participates in routing and forwarding packets.

**Traditional vs Ad Hoc Network:**

```
INFRASTRUCTURE-BASED (Wi-Fi):

   Node A ──────► Access Point ──────► Node B
                  (Fixed AP)

AD HOC NETWORK:

   Node A ──────► Node C ──────► Node B
                  (No AP — nodes relay for each other)
```

**Formal Definition:**

An ad hoc network is a collection of **wireless mobile nodes** that dynamically form a **temporary network** without the use of any existing network infrastructure or centralized administration.

---

### **1.2 Types of Ad Hoc Networks**

There are three primary types of ad hoc networks, each suited for a different use case:

```
                      ┌─────────────────────────┐
                      │   Ad Hoc Networks        │
                      └────────────┬────────────┘
                                   │
             ┌─────────────────────┼──────────────────────┐
             ▼                     ▼                      ▼
    ┌────────────────┐   ┌───────────────────┐   ┌─────────────────────┐
    │  MANET         │   │  VANET            │   │  WSN                │
    │ (Mobile Ad Hoc)│   │ (Vehicular Ad Hoc)│   │ (Wireless Sensor)   │
    └────────────────┘   └───────────────────┘   └─────────────────────┘
  General-purpose        Vehicles as nodes       Tiny sensor nodes
  mobile networks        on roads/highways       monitoring environment
```

#### **1. MANET (Mobile Ad Hoc Network)**
- Most general form.
- Mobile nodes (laptops, smartphones) move freely.
- Topology changes rapidly.
- No fixed infrastructure.
- Example: Soldiers communicating on battlefield.

#### **2. VANET (Vehicular Ad Hoc Network)**
- Nodes are **vehicles** (cars, buses, trucks).
- Nodes move at high speed along roads.
- Special challenges: very high mobility, frequent disconnections.
- Applications: traffic management, collision avoidance, GPS-free navigation.

#### **3. WSN (Wireless Sensor Network)**
- Nodes are small **sensor devices** with limited battery, memory, and CPU.
- Deployed in an area to **monitor physical phenomena** (temperature, pressure, humidity).
- Nodes are often stationary (unlike MANET).
- Data flows toward a **sink/gateway** node.
- Applications: environmental monitoring, smart agriculture, healthcare.

---

### **1.3 Infrastructure vs Ad Hoc Networks — Comparison**

| Feature | Infrastructure Network | Ad Hoc Network |
|---------|------------------------|----------------|
| **Central Authority** | Yes (Access Point / Base Station) | No (fully distributed) |
| **Fixed Infrastructure** | Required (routers, APs, towers) | Not required |
| **Setup Time** | Long (hardware installation) | Quick (plug-and-play) |
| **Scalability** | Good (hierarchical) | Limited |
| **Routing** | Done by routers | Done by each node |
| **Cost** | High (infrastructure required) | Low |
| **Mobility Support** | Limited (handoff needed) | High (nodes move freely) |
| **Reliability** | High (controlled environment) | Lower (interference, fading) |
| **Security** | Easier to control | Harder (no central authority) |
| **Example** | Wi-Fi, 4G/5G cellular | Military mesh, disaster networks |

---

## **Section 2: Characteristics of MANETs**

> PYQ: What are the characteristics of MANET. (Dec 2025, 2.5 marks)  
> PYQ: Explain the characteristics of Mobile Ad hoc Networks (MANETs). (May 2025, 8 marks)  
> PYQ: Discuss the characteristics & applications of MANETs in detail. (May 2023, 15 marks)  
> PYQ: Discuss the characteristics of wireless channel. (Dec 2023, 15 marks)  
> PYQ: Briefly explain MANET. (May 2023, Jul 2022, 2.5 marks)

### **2.1 Overview**

A **MANET (Mobile Ad Hoc Network)** is a special class of wireless ad hoc network where all participating nodes are mobile. Understanding its characteristics is essential to appreciate why standard network protocols cannot be directly applied.

---

### **2.2 Key Characteristics**

#### **1. Dynamic Topology**

- Nodes in a MANET move **freely and unpredictably** in any direction.
- As nodes move, links between them **appear and disappear** constantly.
- The network topology (map of connections) changes **rapidly and continuously**.
- This makes routing very challenging because routes that were valid a moment ago may no longer exist.

```
Time T1:         Time T2 (nodes moved):
A──B──C          A    B──C
      |               |
      D          A──D
(A can reach D)  (B disconnected from A)
```

#### **2. Distributed Operation (No Central Authority)**

- There is **no dedicated router, server, or base station**.
- Every node acts simultaneously as a **host** (source/destination) and a **router** (forwarder).
- All network functions (routing, security, addressing) are distributed among nodes.
- This is both a strength (no single point of failure) and a weakness (harder to coordinate).

#### **3. Multi-hop Routing**

- In a MANET, two nodes that want to communicate may not be within direct wireless range.
- Data must travel through **multiple intermediate nodes**, each forwarding the packet to the next.
- This is called **multi-hop communication**.

```
Source ──► Node A ──► Node B ──► Node C ──► Destination
            hop1       hop2       hop3
```

- Each hop introduces **delay and potential packet loss**.

#### **4. Bandwidth-Constrained Wireless Links**

- Wireless links have much **lower bandwidth** than wired links.
- The shared wireless medium causes **interference** when multiple nodes transmit simultaneously.
- Bandwidth is further reduced by **multipath fading**, **noise**, and **signal attenuation**.
- This limits the throughput available to each node.

#### **5. Energy-Constrained Nodes (Battery-Powered)**

- MANET nodes are typically **battery-powered** devices (laptops, smartphones, sensors).
- Every operation — transmission, reception, processing — consumes battery.
- Nodes must **conserve energy** to extend network lifetime.
- A node with dead battery is completely lost from the network.
- Routing protocols must be **energy-aware** to avoid draining certain nodes faster.

#### **6. Limited Physical Security**

- Wireless links **broadcast** signals in all directions — anyone nearby can intercept them.
- Nodes can join or leave the network without authentication.
- There is no physical perimeter (like a locked server room) to secure the network.
- Common attacks: **eavesdropping**, **replay attacks**, **man-in-the-middle**, **Sybil attacks**, **blackhole attacks**.

#### **7. Self-Organizing and Self-Healing**

- **Self-organizing:** Nodes automatically discover neighbors, form routes, and configure themselves — no manual setup.
- **Self-healing:** If a node fails or a link breaks, the network automatically finds alternate routes.
- This makes MANETs resilient and fault-tolerant in theory.

#### **8. Scalability Challenges**

- As the number of nodes increases, routing overhead (control messages) grows significantly.
- More nodes = more movement = more topology changes = more route updates.
- Protocols that work for 50 nodes may collapse with 500 nodes.
- Designing **scalable** MANET protocols is an active research area.

#### **9. Variable Capacity Links**

- Link quality in a MANET is **not constant** — it fluctuates based on:
  - Distance between nodes
  - Obstacles (walls, buildings)
  - Interference from other devices
  - Relative speed (Doppler effect)

#### **10. Heterogeneous Devices**

- MANET can include devices with very different capabilities:
  - Old smartphones with slow CPUs
  - Modern tablets with fast GPUs
  - Embedded sensors with tiny memory
- Protocols must work with the **weakest common capability**.

---

### **2.3 Summary Table — MANET Characteristics**

| Characteristic | Description | Challenge Caused |
|---------------|-------------|------------------|
| Dynamic topology | Nodes move freely | Routes break frequently |
| Distributed operation | No central control | Hard to coordinate |
| Multi-hop routing | Intermediate nodes relay data | Increased delay, routing complexity |
| Bandwidth constrained | Wireless has low capacity | Congestion, packet loss |
| Energy constrained | Battery-powered | Nodes die, uneven load |
| Limited security | Open wireless medium | Attacks, eavesdropping |
| Self-organizing | Auto-configuration | Protocol design complexity |
| Scalability issues | Routing overhead grows | Performance degrades at scale |

---

## **Section 3: Applications of MANETs**

> PYQ: List and brief the various applications of MANETs. (May 2025, Dec 2025, 7 marks)  
> PYQ: What are the applications of MANET and challenges of MANET? (Dec 2023, 15 marks)  
> PYQ: Explain Applications of MANETs and Challenges of MANETs. (Jul 2022, 7.5×2=15 marks)  
> PYQ: Discuss the characteristics & applications of MANETs in detail. (May 2023, 15 marks)

### **3.1 Military / Battlefield Communication**

This is the **original motivation** for MANET research.

- Soldiers carry radio devices and need to communicate in the field.
- No time or resources to set up infrastructure (antennas, base stations).
- Commanders need real-time information about troop positions.
- MANETs allow **instant formation** of secure communication networks.

**Use Cases:**
- Battlefield coordination between soldiers
- Communication between tanks, drones, and command centers
- Surveillance data relay from unmanned vehicles

```
Soldier A ──► Soldier B ──► Command Center
   (relay)       (relay)
```

---

### **3.2 Emergency / Disaster Relief**

When natural disasters (earthquakes, floods, hurricanes) destroy existing infrastructure, MANETs provide communication where nothing else works.

- After an earthquake, cell towers and landlines may be destroyed.
- Rescue teams use MANET-capable devices to communicate.
- First responders can form a temporary network instantly.

**Use Cases:**
- Search and rescue coordination
- Hospital-to-hospital emergency communication
- Police and fire department coordination

---

### **3.3 Personal Area Networking (PAN)**

- Small-scale ad hoc networks among personal devices.
- Example: Connecting your phone, tablet, and laptop without a Wi-Fi router.
- Bluetooth-based PANs (piconets) are a form of ad hoc networking.
- Sharing files between nearby devices.

---

### **3.4 Vehicular Networks (VANET)**

- Vehicles on roads form a MANET — called **VANET (Vehicular Ad Hoc Network)**.
- Each car communicates with nearby cars (**V2V — Vehicle to Vehicle**) and with roadside infrastructure (**V2I — Vehicle to Infrastructure**).

**Use Cases:**
- Collision avoidance warnings ("car ahead braking hard!")
- Traffic congestion information sharing
- Automatic toll collection
- Emergency vehicle priority at intersections
- Internet access in tunnels via multi-hop relay

---

### **3.5 Commercial Applications**

- **Conference/Meeting Networks:** Attendees at a conference connect instantly without a Wi-Fi router.
- **Trade Shows:** Temporary networks for product demonstrations.
- **Stadium/Concert Networking:** Large crowds sharing data.
- **Retail:** Wireless inventory tracking in warehouses.

---

### **3.6 Education**

- In remote or rural areas without internet access, MANET can be used to share educational content.
- Students and teachers form a local ad hoc network.
- Example: **One Laptop per Child (OLPC)** project used mesh networking for schools.

---

### **3.7 Other Applications**

- **Healthcare:** Wireless monitoring of patients in hospitals. Sensor nodes on patients send data to nurses' devices.
- **Environmental Monitoring:** Deploying sensor nodes in forests, oceans, or disaster zones to monitor conditions.
- **Mining / Underground Operations:** Communication in areas where radio towers cannot be installed.
- **Space / Remote Exploration:** Communication between rover units on another planet.

---

### **3.8 Summary Table — MANET Applications**

| Application Area | Use Case | Why MANET? |
|-----------------|----------|------------|
| Military | Battlefield communication | No fixed infrastructure possible |
| Disaster Relief | Emergency coordination | Infrastructure destroyed |
| Personal Networks | Device-to-device file sharing | Convenience, no router needed |
| VANET | Traffic safety, navigation | Vehicles are moving nodes |
| Commercial | Conferences, warehouses | Temporary, quick setup |
| Education | Rural connectivity | No internet infrastructure |
| Healthcare | Patient monitoring | Mobility of patients |

---

## **Section 4: Challenges of MANETs**

> PYQ: Discuss the various issues in Adhoc Wireless sensor network. (Dec 2025, 8 marks)  
> PYQ: What are the applications of MANET and challenges of MANET? (Dec 2023, 15 marks)  
> PYQ: Challenges of MANETs. (Jul 2022, 7.5 marks)

### **4.1 Routing Challenges**

Routing is the most fundamental challenge in MANETs.

**Why routing is hard:**
- Topology changes due to node mobility — routes become invalid quickly.
- A route valid now may be broken in seconds.
- Routing tables must be updated constantly, consuming bandwidth and energy.
- Multi-hop routing introduces cumulative delays.

**Key problems:**
- **Route discovery overhead** — finding a new route takes time and bandwidth.
- **Stale routes** — old routes in tables lead to packet drops.
- **Loop formation** — routing loops waste bandwidth.
- **Route maintenance** — detecting broken links and finding alternates.

---

### **4.2 Security Challenges**

MANETs are inherently vulnerable due to the open wireless medium and lack of centralized control.

**Common Attacks:**

| Attack | Description |
|--------|-------------|
| **Blackhole Attack** | A malicious node claims shortest route to drop all packets |
| **Wormhole Attack** | Two colluding attackers create a fake fast tunnel to divert traffic |
| **Sybil Attack** | A node pretends to be multiple nodes to gain influence |
| **Flooding Attack (DoS)** | Attacker floods network with fake route requests to exhaust resources |
| **Eavesdropping** | Passively listening to wireless transmissions |
| **Man-in-the-Middle** | Intercepting and modifying packets between two nodes |
| **Replay Attack** | Re-sending old valid packets to confuse the network |

**Why security is harder in MANETs:**
- No central authentication server.
- Nodes may be captured by enemies (especially in military).
- Wireless medium is accessible to all.

---

### **4.3 QoS (Quality of Service) Challenges**

**QoS** refers to guaranteeing certain performance metrics (bandwidth, delay, jitter) for applications.

- In wired networks, QoS is managed by dedicated routers.
- In MANETs, the dynamic topology means QoS guarantees can collapse at any moment.
- Multimedia applications (voice, video) require **low and consistent delay (jitter)** — hard to guarantee in MANETs.
- Bandwidth reservation is difficult when the network topology keeps changing.

---

### **4.4 Power / Energy Constraints**

- Battery-powered devices have limited energy.
- Transmitting data is the **largest energy consumer** in a wireless node.
- Nodes that are relay points carry traffic for others — their batteries drain faster.
- A "selfish node" may refuse to relay to save its own battery.
- Energy-aware routing is needed to **balance the load** and **maximize network lifetime**.

**Energy Trade-off:**

```
More Hops = More Energy (each relay drains multiple batteries)
Fewer Hops = Higher transmission power per hop (also drains fast)
Optimal = balance between number of hops and power per hop
```

---

### **4.5 Scalability**

- A routing protocol may work perfectly for 10–20 nodes.
- With 100+ nodes, routing control traffic (HELLO messages, route requests) can consume most of the bandwidth.
- The problem worsens because: more nodes → more movement → more topology changes → more routing updates.
- **Flat routing** (where every node knows every other) doesn't scale.
- **Hierarchical routing** (zones, clusters) helps but adds complexity.

---

### **4.6 Bandwidth Limitations**

- Wireless medium has much lower capacity than fiber/copper.
- Shared medium: only one node in an area should transmit at a time to avoid collision.
- **MAC layer** must handle access control — adds overhead.
- Hidden node problem, exposed node problem (see below) reduce effective bandwidth.

---

### **4.7 Hidden Node Problem**

> PYQ: What is hidden terminal problem? (May 2025, 3 marks)

```
         A ──────────────► B ◄───────────── C
         |        range    |       range    |
         └── A cannot hear C ──────────────┘
```

- **Node A** and **Node C** are both in range of **Node B**, but **out of range of each other**.
- Both A and C sense the channel as idle (they cannot hear each other).
- Both transmit to B simultaneously → **collision at B**.
- This reduces throughput significantly.
- **Solution:** RTS/CTS (Request to Send / Clear to Send) mechanism.

---

### **4.8 Exposed Node Problem**

```
         A ◄──────────── B ────────────► C ────────────► D
              (B transmitting to A)        (C wants to send to D)
```

- **Node B** is transmitting to **Node A**.
- **Node C** senses the channel as busy (it hears B) and waits.
- But C could safely transmit to D without interfering with B→A (because D is out of B's range).
- C is unnecessarily blocked — this reduces throughput.
- This is the **exposed node problem**.

---

### **4.9 Summary Table — MANET Challenges**

| Challenge | Root Cause | Impact |
|-----------|-----------|--------|
| Routing | Dynamic topology | Broken routes, high overhead |
| Security | Open medium, no central authority | Attacks, data theft |
| QoS | Changing topology | Cannot guarantee delay/bandwidth |
| Energy | Battery-powered nodes | Network partitioning, node death |
| Scalability | Routing overhead grows with nodes | Performance collapse |
| Bandwidth | Shared wireless medium | Congestion, low throughput |
| Hidden node | Nodes cannot detect all transmissions | Collisions at receivers |
| Exposed node | Nodes overhear irrelevant transmissions | Unnecessary blocking |

---

## **Section 5: Routing in MANETs**

> PYQ: What do you mean by a routing table. (May 2025, 3 marks)  
> PYQ: Explain Routing Layer. (May 2023, 2.5 marks)  
> PYQ: Explain the challenges in designing routing algorithms. (Dec 2025, 8 marks)  
> PYQ: Discuss different routing algorithms of MANETs in detail. (Jul 2022, 15 marks)

### **5.1 Why Routing in MANETs is Different**

In wired networks (like the Internet), routing is done by dedicated **routers** with:
- Stable, known topology
- High-bandwidth links
- Unlimited power
- Centralized routing tables (BGP, OSPF)

In MANETs, routing must be done **by every mobile node** with:
- Unpredictable, frequently changing topology
- Low-bandwidth, lossy wireless links
- Limited battery power
- No centralized routing table authority

**Consequences:**
- Standard routing protocols (OSPF, RIP) cannot be used directly.
- MANET-specific protocols must handle link failures gracefully.
- Protocols must be lightweight (small overhead) to save battery and bandwidth.

---

### **5.2 Criteria for Classification of Routing Protocols**

MANET routing protocols can be classified based on several different criteria:

#### **Criterion 1: Timing / Reactivity**

| Type | Description |
|------|-------------|
| **Proactive (Table-driven)** | Routes are maintained at all times; updates sent periodically |
| **Reactive (On-demand)** | Routes are discovered only when needed |
| **Hybrid** | Proactive within a zone, reactive outside |

#### **Criterion 2: Route Initiator**

| Type | Description |
|------|-------------|
| **Source-initiated** | The source node starts route discovery (e.g., DSR) |
| **Destination-initiated** | The destination node responds with routes |

#### **Criterion 3: Routing Information Used**

| Type | Description |
|------|-------------|
| **Topology-based** | Uses knowledge of the network graph (links, nodes) |
| **Position-based (Geographic)** | Uses physical location (GPS coordinates) of nodes |
| **Energy-based** | Uses remaining battery level of nodes |
| **QoS-based** | Uses link quality metrics (delay, bandwidth) |

#### **Criterion 4: Number of Paths**

| Type | Description |
|------|-------------|
| **Single path** | Only one route is maintained at a time |
| **Multipath** | Multiple routes are maintained simultaneously for redundancy |

#### **Criterion 5: Network Structure**

| Type | Description |
|------|-------------|
| **Flat** | All nodes have equal role |
| **Hierarchical** | Nodes organized into clusters; cluster heads do routing |

---

### **5.3 Taxonomy of MANET Routing Algorithms**

> PYQ: Give the taxonomy of MANET routing algorithm. (May 2025, 8 marks)

```
                  ┌──────────────────────────────────┐
                  │     MANET Routing Algorithms      │
                  └───────────────┬──────────────────┘
                                  │
          ┌───────────────────────┼───────────────────────┐
          ▼                       ▼                       ▼
  ┌───────────────┐      ┌────────────────┐      ┌────────────────┐
  │ Topology-Based│      │ Position-Based │      │ Other          │
  │   Routing     │      │ (Geographic)   │      │ Algorithms     │
  └───────┬───────┘      └────────┬───────┘      └────────┬───────┘
          │                       │                       │
    ┌─────┼──────┐          GPS-based              ┌──────┼──────┐
    ▼     ▼      ▼          Greedy forward          ▼      ▼      ▼
Proactive Reactive Hybrid   GPSR               Power  Multipath  QoS
(DSDV,   (AODV,   (ZRP)                       Aware  Routing   Routing
 OLSR)    DSR)
```

---

## **Section 6: Topology-Based Routing Algorithms**

> PYQ: Explain and illustrate any one Topology-based Routing algorithm. (May 2025, 7 marks)  
> PYQ: How a reactive routing protocol is different from a proactive routing protocol? (May 2025, Dec 2025, Dec 2023, 2.5–3 marks)  
> PYQ: Explain Reactive Routing Protocol and Proactive Routing Protocol in detail. (May 2023, 2×7.5=15 marks)  
> PYQ: Discuss any four reactive routing protocols for Ad-hoc wireless networks. (Dec 2023, 15 marks)  
> PYQ: Illustrate the table driven routing algorithm — Cluster Head Gateway routing protocol. (Dec 2025, 8 marks)  
> PYQ: Differentiate DSDV and AODV. (May 2025, 8 marks)  
> PYQ: Give the significance of the principle involved in a demand routing protocol. (Dec 2025, 7 marks)

**Topology-based routing** uses information about the **network graph** (which nodes exist and which links connect them) to make routing decisions. There are three main sub-types:

### **6.1 Proactive (Table-Driven) Routing**

**Definition:**

**Proactive routing** protocols maintain **up-to-date routing tables** for every possible destination at all times. Nodes periodically exchange routing updates so that every node knows the full network topology.

**Working Principle:**

```
Every node maintains a routing table:
┌────────────┬──────────────┬──────────┐
│ Destination│  Next Hop    │  Cost    │
├────────────┼──────────────┼──────────┤
│  Node B    │   Node C     │   2      │
│  Node D    │   Node A     │   1      │
│  Node E    │   Node C     │   3      │
└────────────┴──────────────┴──────────┘

Nodes exchange updates periodically (e.g., every 5 seconds):
"Hello, my table has changed..."
```

**Advantages:**
✅ Routes are immediately available — no delay when data needs to be sent.  
✅ Good for applications requiring **low latency** route setup.  
✅ Simple to understand and implement.

**Disadvantages:**
❌ High **control overhead** — periodic updates consume bandwidth and energy even when no data is being sent.  
❌ Stale routing entries — in highly mobile networks, tables may be outdated before data arrives.  
❌ Does not scale well — overhead grows with number of nodes.

---

#### **6.1.1 DSDV (Destination Sequenced Distance Vector)**

**Full name:** Destination Sequenced Distance Vector

**Based on:** Bellman-Ford (Distance Vector) algorithm, with sequence numbers to prevent routing loops.

**How it works:**

1. Each node maintains a routing table with:
   - Destination
   - Next Hop
   - Number of hops (metric)
   - **Sequence number** (even = from destination, odd = route broken)
2. Nodes broadcast their routing tables periodically.
3. On receiving an update, a node updates its table if:
   - The received sequence number is **higher** (more recent info), OR
   - Same sequence number but **fewer hops** (better route).
4. Sequence numbers prevent **count-to-infinity** and loops.

**Routing Table Example:**

| Destination | Next Hop | Hops | Sequence No. |
|-------------|----------|------|--------------|
| B | C | 2 | B-12 |
| D | D | 1 | D-8 |
| E | C | 3 | E-6 |

**Two types of updates:**
- **Full dump:** Complete routing table (sent infrequently).
- **Incremental:** Only changed entries (sent when changes occur).

**Advantages:**
✅ Loop-free routing (guaranteed by sequence numbers).  
✅ Routes always ready.  
✅ Simple implementation.

**Disadvantages:**
❌ High overhead for large networks.  
❌ Slow convergence when topology changes rapidly.  
❌ Wasteful when little data is transmitted.

---

#### **6.1.2 OLSR (Optimized Link State Routing)**

**Full name:** Optimized Link State Routing

**Based on:** Link State routing (like OSPF), optimized using **Multipoint Relays (MPR)**.

**Key Concept — Multipoint Relay (MPR):**

- In standard flooding, every node re-broadcasts a message — huge overhead.
- OLSR selects a **small subset of neighbors** (MPRs) to forward control messages.
- Only MPR nodes re-broadcast, drastically reducing flooding overhead.

```
Without MPR (standard flooding):
A broadcasts → B, C, D, E, F all re-broadcast (5 re-broadcasts)

With MPR:
A selects B and D as MPRs → only B and D re-broadcast (2 re-broadcasts)
```

**How OLSR works:**

1. Each node selects a set of **MPR nodes** from its 1-hop neighbors that can reach all 2-hop neighbors.
2. Nodes broadcast **Hello messages** periodically to discover neighbors.
3. MPR nodes send **TC (Topology Control) messages** to propagate link-state info.
4. Each node builds a **topology map** and computes shortest paths using Dijkstra's algorithm.

**Advantages:**
✅ Significantly reduced flooding overhead vs standard link-state.  
✅ Efficient for **dense networks**.  
✅ Loop-free, routes always available.  
✅ Supports QoS extensions.

**Disadvantages:**
❌ Still maintains tables for all destinations (overhead for sparse networks).  
❌ MPR selection adds complexity.  
❌ TC messages can become outdated in high-mobility scenarios.

---

### **6.2 Reactive (On-Demand) Routing**

**Definition:**

**Reactive routing** protocols discover routes **only when a source node needs to send data** to a destination. No routing table is maintained when there is no data to send.

**Working Principle:**

```
1. Source wants to send to Destination.
2. Source floods a Route Request (RREQ) packet:
   RREQ: [Source=A, Dest=D, SeqNo=5, TTL=10]

3. Every intermediate node re-broadcasts RREQ.
4. Destination (or a node with a fresh route) sends a Route Reply (RREP):
   RREP: [Source=A, Dest=D, Route: A→B→C→D]

5. Source receives RREP and starts sending data.
6. If route breaks: Route Error (RERR) sent back.
```

**Advantages:**
✅ Zero routing overhead when no data is being sent.  
✅ Scales better for **sparse or low-traffic** networks.  
✅ Routes are always fresh (discovered just-in-time).

**Disadvantages:**
❌ **Route discovery latency** — data transmission is delayed until a route is found.  
❌ RREQ flooding creates temporary overhead when route is needed.  
❌ Poor for real-time applications that cannot tolerate setup delay.

---

#### **6.2.1 AODV (Ad hoc On-demand Distance Vector)**

**Full name:** Ad hoc On-demand Distance Vector

**Type:** Reactive, uses hop-count metric, maintains routing tables.

**Key Messages:**
- **RREQ** (Route Request) — broadcast by source to find a route.
- **RREP** (Route Reply) — unicast from destination (or intermediate node) back to source.
- **RERR** (Route Error) — sent when a link breaks.

**Detailed Working of AODV:**

**Step 1 — Route Discovery:**
```
Source (S) wants to send to Destination (D).
S broadcasts RREQ:
  RREQ = {Source=S, Dest=D, SrcSeqNo=5, DestSeqNo=last known, BroadcastID=42, TTL=10}

Intermediate nodes:
  - Set up a reverse route to S (for sending RREP back).
  - Re-broadcast RREQ (if not already seen).
  - Discard duplicate RREQs (identified by Source + BroadcastID).
```

**Step 2 — Route Reply:**
```
Destination D (or intermediate node with fresh route) sends RREP back:
  RREP = {Source=S, Dest=D, DestSeqNo=10, HopCount=3, Lifetime=T}

Intermediate nodes:
  - Forward RREP toward S using reverse route entries.
  - Set up a forward route to D while forwarding.
```

**Step 3 — Data Transmission:**
```
S now has route: S → A → B → D
Data packets are sent along this route.
```

**Step 4 — Route Maintenance:**
```
If a link breaks (e.g., A→B breaks):
  A sends RERR back to S.
  S can restart route discovery.
```

**ASCII Diagram — AODV Route Discovery:**

```
        S ──RREQ──► A ──RREQ──► B ──RREQ──► D
        │                                    │
        ◄─────────────RREP───────────────────┘
        (reverse path: D→B→A→S)

After RREP received:
  Routing table at S: Dest=D, NextHop=A
  Routing table at A: Dest=D, NextHop=B
  Routing table at B: Dest=D, NextHop=D
```

**Sequence Numbers in AODV:**
- Each node maintains a **sequence number** for itself.
- Sequence numbers ensure freshness — higher sequence number = more recent route.
- Prevents loops and stale routes.

**Advantages:**
✅ Loop-free (due to sequence numbers).  
✅ Supports both unicast and multicast.  
✅ Low overhead when network has low traffic.  
✅ Scales reasonably well.

**Disadvantages:**
❌ Route discovery adds latency before data can flow.  
❌ RREQ flooding can cause broadcast storm.  
❌ Route may break due to mobility (RERR cycle).

---

#### **6.2.2 DSR (Dynamic Source Routing)**

**Full name:** Dynamic Source Routing

**Type:** Reactive, uses **source routing** (the full path is embedded in each packet header).

**Key Concept — Source Routing:**
- Instead of each intermediate node looking up a routing table, the **source node specifies the complete path** in every packet header.
- Intermediate nodes simply forward the packet to the next node listed in the header.

**Key Messages:**
- **RREQ** (Route Request) — flooded, each node adds its ID to the RREQ.
- **RREP** (Route Reply) — sent back with the complete route.
- **RERR** (Route Error) — sent when a link breaks.

**Detailed Working of DSR:**

**Step 1 — Route Discovery:**
```
S wants to send to D.
S broadcasts RREQ with path so far: [S]

Intermediate node A receives RREQ:
  Appends itself: [S, A]
  Re-broadcasts RREQ.

Node B receives RREQ:
  Appends itself: [S, A, B]
  Re-broadcasts RREQ.

Destination D receives RREQ: [S, A, B, D]
  D now knows the full path: S → A → B → D
```

**Step 2 — Route Reply:**
```
D sends RREP back to S with the route:
  RREP = {Route: S→A→B→D}
S stores this in its Route Cache.
```

**Step 3 — Data Transmission:**
```
Packet header contains full route:
  [Data | Route: A, B, D]
A forwards to B; B forwards to D.
```

**Route Cache:**
- Nodes **overhear** route information in passing packets and cache it.
- Routes learned by overhearing can be used for future transmissions — reduces RREQ floods.

**ASCII Diagram — DSR vs AODV Headers:**

```
AODV packet header:
  [Data | Dest=D | NextHop=A]    ← Each node looks up its own table

DSR packet header:
  [Data | Route: A → B → D]     ← Full path carried in every packet
```

**Advantages:**
✅ Multiple routes cached — no need to rediscover immediately after failure.  
✅ Route caching reduces RREQ floods.  
✅ Does not require periodic updates — fully on-demand.  
✅ Nodes can passively learn routes from overheard packets.

**Disadvantages:**
❌ Packet header grows large with long routes (overhead proportional to path length).  
❌ Stale cache entries can cause packet drops.  
❌ Not suitable for large networks (header size becomes too big).  
❌ Promiscuous mode required for route caching (high power consumption).

---

### **6.3 Hybrid Routing: ZRP**

**Full name:** Zone Routing Protocol

**Type:** Hybrid — combines proactive and reactive strategies.

**Core Idea:**

ZRP divides the network into **zones** around each node. Within the zone, proactive routing is used. Between zones, reactive routing is used.

```
                 Zone of Node A (radius = 2 hops):
                 ┌────────────────────────┐
                 │   B ─── C              │
                 │   |     |              │
                 │   A ─── D ─── E ───── │── F (outside zone)
                 │                        │
                 └────────────────────────┘
                 (A knows routes to B,C,D,E proactively)
                 (To reach F: reactive discovery)
```

**Zone Radius (ρ):** The number of hops defining the zone boundary.

**Two Sub-protocols:**
- **IARP (Intrazone Routing Protocol):** Proactive — maintains routes within the zone.
- **IERP (Interzone Routing Protocol):** Reactive — discovers routes to nodes outside the zone.
- **BRP (Bordercast Resolution Protocol):** Helps forward RREQs efficiently between zones.

**How ZRP Works:**

1. Every node proactively knows all routes within its zone (radius ρ).
2. When A wants to reach F (outside zone):
   - A broadcasts RREQ to its **border nodes** (nodes at the edge of its zone).
   - Border nodes check their zones for F.
   - If F is in a border node's zone, RREP is sent back.
   - Otherwise, the border nodes forward RREQ to their border nodes.

**Advantages:**
✅ Reduces route discovery latency vs pure reactive (nearby nodes found proactively).  
✅ Reduces overhead vs pure proactive (only local topology maintained).  
✅ Tunable — zone radius (ρ) can be adjusted for network conditions.

**Disadvantages:**
❌ More complex to implement than either pure approach.  
❌ Zone maintenance overhead still exists (for intrazone routing).  
❌ Optimal zone radius is hard to determine dynamically.

---

### **6.4 Comparison Table — Proactive vs Reactive vs Hybrid**

| Feature | Proactive (DSDV, OLSR) | Reactive (AODV, DSR) | Hybrid (ZRP) |
|---------|----------------------|---------------------|--------------|
| **Route Availability** | Always ready | Discovered on demand | Partly ready (within zone) |
| **Latency to First Packet** | Very low | High (discovery delay) | Medium |
| **Control Overhead** | High (periodic updates) | Low (only on demand) | Medium |
| **Scalability** | Poor (large networks) | Better | Good |
| **Bandwidth Usage** | High (even idle) | Low (only when needed) | Medium |
| **Suitable For** | Low mobility, frequent traffic | High mobility, sparse traffic | General purpose |
| **Examples** | DSDV, OLSR | AODV, DSR | ZRP |
| **Loop-Free?** | Yes | Yes | Yes |
| **Stale Routes?** | Risk with high mobility | Less risk (fresh discovery) | Medium risk |

---

## **Section 7: Position-Based Routing Algorithms**

> PYQ: Explain position based routing algorithms. (Dec 2023, 15 marks)

### **7.1 Why Position-Based Routing?**

**Problem with topology-based routing:**
- Maintaining global topology (who is connected to whom) requires significant overhead.
- As network size and mobility increase, topology-based protocols struggle.

**Solution — Position-Based (Geographic) Routing:**
- Instead of knowing the **network topology**, each node only needs to know its own **geographic position** (GPS coordinates) and the position of its **immediate neighbors**.
- Each node also needs to know the position of the **destination** (obtained via a location service).
- Routing decision: "Forward this packet to whichever neighbor is **closest to the destination**."

**No routing tables needed. No global topology required.**

---

### **7.2 Greedy Forwarding**

**Definition:**

**Greedy forwarding** is the fundamental strategy in position-based routing. A node forwards a packet to the **neighbor that is closest to the destination** (in terms of Euclidean distance).

```
    Source (S)
       │
       │ neighbors of S: A, B, C
       │
       S ────────────────────────────────── Destination (D)
      /|\
     A B C
     |
     A is closest to D → forward to A

    A ────────────────────── D
   /|\
  E F G
     |
     F is closest to D → forward to F

    F ──────────── D  (direct neighbor!)
```

**Working:**

1. Each node knows:
   - Its own position (GPS).
   - Positions of all its **1-hop neighbors**.
   - Position of the **destination**.
2. The node selects the neighbor **closest to the destination** and forwards.
3. This repeats hop by hop until the packet reaches the destination.

**Problem — The Void (Local Maximum):**

Greedy forwarding can get stuck in a **void** — a situation where none of the current node's neighbors are closer to the destination than the current node itself.

```
     S ──► A ──► B
                  B is stuck! No neighbor closer to D.
                       ↕         D
                  ┌────┘         (D is in a void)
                  C (far from D)
```

**Solution:** When greedy forwarding fails, switch to **perimeter routing (face routing)**.

---

### **7.3 GPSR (Greedy Perimeter Stateless Routing)**

**Full name:** Greedy Perimeter Stateless Routing

**Proposed by:** Karp and Kung (2000).

**GPSR combines two modes:**
1. **Greedy mode** — used when possible (forward to closest neighbor to destination).
2. **Perimeter mode** — used when greedy fails (packet is stuck at a void).

**Perimeter Mode — Right-Hand Rule:**

When greedy fails (current node is a local maximum):
- Switch to perimeter mode.
- Use the **right-hand rule** to traverse the perimeter of the void.
- Eventually, the packet finds a node from which greedy forwarding can resume.

```
Right-Hand Rule:
  When you arrive at a node via edge (u, v):
  Choose the next edge that is the first counterclockwise from (u, v).
  This traces the face of the planar graph.

Diagram:
           ┌──A──┐
      S ───┤     ├─── D
           └──B──┘
                C (stuck — local max)

  C uses perimeter (right-hand rule) to go around the void:
  C → A → D (GPSR found a path!)
```

**Planarization:**
- GPSR first builds a **planar graph** (no crossing edges) using:
  - **GG (Gabriel Graph)** or
  - **RNG (Relative Neighborhood Graph)**
- The right-hand rule only works correctly on planar graphs.

**GPSR Modes Diagram:**

```
                         Greedy Mode:
S ───────────────────────────────────────► D
         (each hop gets closer to D)

                         Perimeter Mode (when void found):
S ─────► ... ─────► LocalMax ─────────────► D
                        │   (right-hand rule)
                        └──► A ──► B ──► D
```

**Advantages:**
✅ **Stateless** — no routing tables, no topology stored.  
✅ Scales to very large networks (no global state needed).  
✅ Guaranteed delivery in connected planar graphs.  
✅ Low overhead — only need neighbor position info.

**Disadvantages:**
❌ Requires **GPS hardware** on every node (may not always be available).  
❌ GPS may be inaccurate indoors or in dense urban environments.  
❌ Location service needed to map destination IDs to GPS coordinates.  
❌ Planarization may disconnect the graph, causing delivery failure.  
❌ Does not optimize for path length — greedy path may not be shortest.

---

### **7.4 Other Position-Based Protocols**

| Protocol | Description |
|----------|-------------|
| **LAR (Location Aided Routing)** | Uses GPS to restrict RREQ flooding to a **request zone** — reduces overhead of reactive protocols |
| **DREAM (Distance Routing Effect Algorithm for Mobility)** | Proactive position-based; update frequency proportional to node speed |
| **FACE Routing** | Pure perimeter routing using face traversal |
| **GFG (Greedy-Face-Greedy)** | Similar to GPSR — alternate between greedy and face routing |

---

### **7.5 Comparison — Topology-Based vs Position-Based**

| Feature | Topology-Based | Position-Based |
|---------|----------------|----------------|
| **Information needed** | Network topology (links, nodes) | GPS coordinates of nodes |
| **Routing tables** | Required | Not required |
| **Overhead** | High (topology updates) | Low (only neighbor positions) |
| **Scalability** | Limited | High |
| **GPS required?** | No | Yes |
| **Delivery guarantee** | Yes (if topology correct) | Yes (if network connected + planar) |
| **Examples** | DSDV, OLSR, AODV, DSR | GPSR, LAR, DREAM |

---

## **Section 8: Other Routing Algorithms**

### **8.1 Power-Aware Routing**

**Motivation:**

Standard routing protocols (AODV, DSR) use **hop count** or **path length** as the metric. They do not consider the remaining battery of intermediate nodes. This leads to:
- Heavily used relay nodes exhausting their batteries quickly.
- Network partitioning when critical relay nodes die.

**Goal:** Maximize overall **network lifetime** by balancing energy usage.

**Strategies:**

#### **Strategy 1: Minimize Total Transmission Power**
- Choose paths that minimize the **total power consumed** to deliver a packet.
- Not always the shortest hop path — may use longer paths with lower transmission power per hop.

#### **Strategy 2: Maximize Minimum Node Battery**
- Choose paths that avoid nodes with **low remaining battery**.
- Ensures no single node is drained prematurely.

#### **Strategy 3: Minimize Maximum Node Energy**
- Minimize the maximum energy consumed by any single node on the path.
- Prevents bottleneck nodes from dying quickly.

#### **Strategy 4: Minimize Energy × Delay**
- Trade-off between energy and delay.
- Suitable for delay-tolerant applications.

**Example Protocol — MTPR (Minimum Total Power Routing):**
- Selects the path with minimum sum of transmission powers.

**Example Protocol — MMBCR (Minimum Maximum Battery Cost Routing):**
- Routes through nodes with maximum battery to avoid draining the weakest nodes.

**Challenges:**
- Battery level is dynamic — a good route now may be bad in 5 minutes.
- Nodes may lie about their battery level to avoid being used as relays.

---

### **8.2 Multipath Routing**

**Motivation:**

Standard routing uses a **single path** between source and destination. If this path breaks, a new route must be discovered — causing delay. Multipath routing maintains **multiple routes simultaneously**.

**Benefits:**
- **Fault tolerance** — if one path fails, switch to another immediately.
- **Load balancing** — distribute traffic across multiple paths to avoid congestion.
- **Increased throughput** — send data simultaneously on multiple paths.
- **Security** — split a message across paths, making eavesdropping harder.

**Types of Multipath Routing:**

| Type | Description |
|------|-------------|
| **Node-disjoint** | Multiple paths share no intermediate nodes (highest redundancy) |
| **Link-disjoint** | Paths share no common links (but may share nodes) |
| **Braided paths** | Paths are not disjoint but are independent enough to provide redundancy |

**How Multipath Works (AOMDV — Ad hoc On-demand Multipath Distance Vector):**

```
Source (S) sends RREQ.
Multiple copies of RREQ reach Destination (D) via different paths.
D sends RREP along each distinct path.
S maintains all valid paths:
  Path 1: S → A → B → D
  Path 2: S → C → E → D
  Path 3: S → A → F → D

Data can be sent on all paths simultaneously (split) or
Path 1 used primarily; Path 2 as backup.
```

**Challenges:**
- Maintaining multiple routes increases overhead.
- Paths may become correlated (share nodes) in dense networks.
- Synchronization of packets on multiple paths.

---

### **8.3 QoS Routing**

**Motivation:**

Different applications have different network requirements:
- **Voice over IP (VoIP):** Needs low delay (< 150 ms) and low jitter.
- **Video streaming:** Needs high bandwidth (> 1 Mbps) and low jitter.
- **File transfer:** Tolerates delay, needs reliable delivery.
- **Sensor data:** May need very low energy, not concerned with delay.

**Standard routing (shortest path) does not consider these requirements.** QoS routing selects paths that **satisfy specific quality constraints**.

**QoS Parameters:**

| Parameter | Description |
|-----------|-------------|
| **Bandwidth** | Minimum link capacity required |
| **Delay** | Maximum end-to-end delay allowed |
| **Jitter** | Maximum variation in delay |
| **Packet Loss Rate** | Maximum fraction of packets that can be dropped |
| **Reliability** | Probability of successful delivery |

**QoS Routing Approaches:**

#### **1. Ticket-Based QoS Routing**
- Source issues "tickets" — each ticket allows searching one path.
- More tickets = more paths explored = higher chance of finding QoS path.
- Trade-off between overhead and success rate.

#### **2. Imprecise State Information QoS Routing**
- QoS routing typically needs global state (link bandwidth, delay) — expensive in MANETs.
- Use **approximate/imprecise** state information to make routing decisions.
- Good enough in practice without the full overhead.

#### **3. CEDAR (Core Extraction Distributed Ad hoc Routing)**
- Builds a **core** (connected dominating set of nodes).
- Core nodes propagate QoS state information.
- Source initiates QoS path discovery through the core.

**Challenges in QoS Routing for MANETs:**
- QoS guarantees collapse when routes change due to mobility.
- Resource reservation (RSVP-style) is hard in dynamic networks.
- Gathering accurate link state information costs energy and bandwidth.

---

### **8.4 Summary — Other Routing Algorithms**

| Algorithm Type | Goal | Metric Used | Key Challenge |
|---------------|------|-------------|---------------|
| Power-aware | Maximize network lifetime | Remaining battery, transmission power | Dynamic battery levels, selfish nodes |
| Multipath | Fault tolerance, load balancing | Multiple path metrics | Overhead, path correlation |
| QoS | Meet application requirements | Delay, bandwidth, jitter, loss | Dynamic topology breaks guarantees |

---

## **Quick Revision Points**

### **Ad Hoc Networks:**
- No fixed infrastructure, self-organizing, multi-hop.
- Types: MANET (mobile), VANET (vehicles), WSN (sensors).

### **MANET Characteristics (remember with "DMBESS"):**
- **D**ynamic topology
- **M**ulti-hop routing
- **B**andwidth constrained
- **E**nergy constrained
- **S**ecurity limited
- **S**elf-organizing, **S**calability challenges

### **MANET Applications:**
- Military, disaster relief, PAN, VANET, commercial, education, healthcare.

### **MANET Challenges:**
- Routing, security (blackhole, wormhole, Sybil), QoS, energy, scalability, hidden/exposed node.

### **Hidden Node vs Exposed Node:**
```
Hidden:  A and C both transmit to B → collision (A and C cannot hear each other)
Exposed: C delays transmission because it hears B→A, but C's transmission to D is safe
```

### **Routing Protocol Classification Criteria:**
- Timing (proactive / reactive / hybrid)
- Initiator (source / destination)
- Info used (topology / position / energy)
- Number of paths (single / multipath)
- Structure (flat / hierarchical)

### **Taxonomy:**
```
MANET Routing
├── Topology-Based
│   ├── Proactive: DSDV, OLSR
│   ├── Reactive: AODV, DSR
│   └── Hybrid: ZRP
├── Position-Based: GPSR, LAR
└── Other: Power-aware, Multipath, QoS
```

### **Proactive vs Reactive — Key Difference:**

| | Proactive | Reactive |
|--|-----------|----------|
| Route ready? | Always | Only after discovery |
| Overhead | Constant (periodic) | Burst (on demand) |
| Latency | Low | High (first packet) |
| Examples | DSDV, OLSR | AODV, DSR |

### **AODV Key Points:**
- RREQ (flood) → RREP (unicast back) → Data → RERR (on failure).
- Sequence numbers prevent loops and stale routes.
- Routing table per node (unlike DSR which embeds full route in header).

### **DSR Key Points:**
- Source routing — full path in every packet header.
- Route cache — nodes store overheard routes.
- Header overhead grows with path length.

### **GPSR Key Points:**
- Greedy mode: forward to neighbor closest to destination.
- Perimeter mode: right-hand rule when greedy fails (void).
- Stateless — no routing tables.
- Requires GPS on every node.

### **Power-Aware Routing Goals:**
- Minimize total power, maximize minimum battery, balance energy load.

### **Multipath Routing Benefits:**
- Fault tolerance, load balancing, throughput, security.

### **QoS Parameters:**
- Bandwidth, delay, jitter, packet loss, reliability.

---

## **Expected Exam Questions**

### **15-mark Questions**

1. Discuss the characteristics & applications of MANETs in detail. *(May 2023)*
2. Discuss the characteristics of wireless channel. *(Dec 2023)*
3. What are the applications of MANET and challenges of MANET? *(Dec 2023)*
4. Explain Applications of MANETs and Challenges of MANETs. *(Jul 2022)*
5. Discuss different routing algorithms of MANETs in detail. *(Jul 2022)*
6. Explain position based routing algorithms. *(Dec 2023)*
7. Explain Reactive Routing Protocol and Proactive Routing Protocol in detail. *(May 2023)*
8. Discuss any four reactive routing protocols for Ad-hoc wireless networks. *(Dec 2023)*

### **7–8 mark Questions**

1. Explain the characteristics of Mobile Ad hoc Networks (MANETs). *(May 2025)*
2. List and brief the various applications of MANETs. *(May 2025, Dec 2025)*
3. Discuss the various issues in Adhoc Wireless sensor network. *(Dec 2025)*
4. Give the taxonomy of MANET routing algorithm. *(May 2025)*
5. Explain and illustrate any one Topology-based Routing algorithm. *(May 2025)*
6. Explain the challenges in designing routing algorithms. *(Dec 2025)*
7. Give the significance of the principle involved in a demand routing protocol. *(Dec 2025)*
8. Illustrate the table driven routing algorithm — Cluster Head Gateway routing protocol. *(Dec 2025)*
9. Differentiate DSDV and AODV. *(May 2025)*

### **Short Answer (2.5–3 marks)**

1. What are the characteristics of MANET? *(Dec 2025)*
2. How a reactive routing protocol is different from a proactive routing protocol? *(May 2025, Dec 2025, Dec 2023)*
3. What is hidden terminal problem? *(May 2025)*
4. What do you mean by a routing table. *(May 2025)*
5. Explain Routing Layer. *(May 2023)*
6. What is MANET? *(May 2023, Jul 2022)*

---

_These notes were compiled by [Deepak Modi](https://deepakmodi.dev)_  
_Last updated: May 2026_
