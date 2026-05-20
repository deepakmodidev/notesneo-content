---
title: "Unit 3: Basics of Wireless, Sensors and Applications"
description: "Sensor Network Classification, Architecture, Physical, MAC, and Link layers"
author: "Deepak Modi"
date: "2026-05-10"
pdfUrl: ""
---

## Syllabus:

Basics of Wireless, Sensors and Applications: Applications, Classification of sensor networks, Architecture of sensor network, Physical layer, MAC layer, Link layer.

---

## 🎯 PYQ Analysis for Unit 3

### **High Priority Topics** (15 marks questions)

1. **Architecture of Wireless Sensor Network (with diagram)** — (Dec 2023: 15, Jul 2022: 15)
2. **Classification of Wireless Sensor Networks + Applications** — (May 2023: 15)
3. **Physical and MAC Layer of WSN** — (May 2023: 15, Jul 2022: 15 — incl. Link Layer)
4. **MAC Protocols for WSN** — (Dec 2023: 15)
5. **Design Goals of MAC Protocol for Ad-Hoc Networks** — (May 2025: 15)
6. **Components of a Sensor Node (role & limitations)** — (Dec 2025: 15)

### **Medium Priority Topics** (Short answers)

1. **Wireless Sensor Network** — Dec 2023 (2.5 marks)
2. **Cellular vs Ad-hoc wireless network** — Dec 2023 (2.5 marks)
3. **MAC Layer** — Dec 2023 (2.5 marks)
4. **Link Layer** — Jul 2022 (2.5 marks)
5. **Sensors / Active vs Passive sensors** — May 2023, May 2025 (2.5–3 marks)
6. **WSN** — Jul 2022 (2.5 marks)
7. **Data relaying in wireless sensor network** — Dec 2023 (2.5 marks)
8. **MAC Protocols for WSN / Issues in MAC for Ad-hoc** — May 2025, Dec 2025 (8 marks)
9. **Sensor Network Architecture (with diagram)** — May 2025, Dec 2025 (7 marks)

---

## **Section 1: Introduction to Wireless Sensor Networks (WSN)**

> PYQ: What is a Wireless sensor network? (Dec 2023, 2.5 marks)  
> PYQ: What is WSN? (Jul 2022, 2.5 marks)  
> PYQ: Explain Sensors. (May 2023, 2.5 marks)  
> PYQ: Differentiate between active and passive sensors. (May 2025, 3 marks)  
> PYQ: What is data relaying in wireless sensor network? (Dec 2023, 2.5 marks)

### **1.1 What is a WSN?**

A **Wireless Sensor Network (WSN)** is a distributed network of small, low-power devices called **sensor nodes** (or **motes**) that collaboratively sense, process, and transmit data about physical or environmental conditions to a central location called the **base station** or **sink**.

Each sensor node is capable of:
- Sensing physical phenomena (temperature, humidity, pressure, motion, etc.)
- Local data processing
- Wireless communication with neighboring nodes or the base station

WSNs operate without fixed infrastructure and are often deployed in harsh, inaccessible, or remote environments.

**Key characteristics of WSN:**
- **Large scale** — hundreds to thousands of nodes
- **Resource constrained** — limited battery, memory, and processing power
- **Self-organizing** — nodes form network autonomously
- **Data-centric** — users query data, not specific nodes
- **Application-specific** — design varies by application

---

### **1.2 WSN vs MANET — Key Differences**

> PYQ: Difference between cellular network and ad-hoc wireless network. (Dec 2023, 2.5 marks)

| Feature | WSN | MANET |
|---|---|---|
| **Primary goal** | Data collection from environment | Communication between mobile users |
| **Node count** | Hundreds to thousands | Tens to hundreds |
| **Node mobility** | Mostly static | Highly mobile |
| **Energy** | Very limited (battery-powered, often not replaceable) | Limited but usually rechargeable |
| **Processing power** | Very low | Moderate to high |
| **Communication** | Many-to-one (convergecast to sink) | Peer-to-peer |
| **Topology** | Semi-static | Highly dynamic |
| **Data model** | Data-centric (event-driven or periodic) | Address-centric (node IDs) |
| **Node identity** | Usually not important | Important (routing by address) |
| **Deployment** | Random/planned in hostile areas | Random in open environments |
| **Failure tolerance** | Must tolerate node failures | Less tolerance expected |
| **Traffic pattern** | Periodic or event-driven small packets | Bursty, varied traffic |
| **Security** | Hard to secure (physical access) | Easier to secure |

---

### **1.3 Key Constraints of Sensor Nodes**

#### **Energy**
- Sensor nodes are battery-powered with **no or limited recharging** capability.
- Energy is the **most critical constraint** — determines network lifetime.
- Energy consumption breakdown:
  - Communication (radio) — **dominant** (~70–80%)
  - Sensing — moderate
  - Processing — relatively low
- Nodes must minimize idle listening, overhearing, and collisions.

#### **Memory**
- Typical sensor nodes have very limited RAM (**4–256 KB**) and Flash memory (**32 KB–1 MB**).
- Limits the complexity of algorithms that can run on the node.
- Protocols must be lightweight and compact.

#### **Processing Power**
- Microcontrollers like **ATmega128**, **MSP430**, or **ARM Cortex-M** are used.
- Clock speeds in the range of **4–16 MHz** — far less than general-purpose CPUs.
- Complex computations (encryption, compression) must be carefully designed.

#### **Communication Range**
- Typical range: **10 m to 100 m** (depends on power and environment).
- Long-range transmission is costly in energy — **multi-hop routing** is used instead.
- Radio transceivers operate in the **ISM (Industrial, Scientific, Medical)** bands.

---

## **Section 2: Applications of Sensor Networks**

> PYQ: Discuss the classification of wireless sensor networks and its applications in detail. (May 2023, 15 marks)

WSNs are deployed across a wide range of domains. The key driving factor is the ability to place sensors in locations that are **inaccessible, hazardous, or impractical** for wired sensing.

---

### **2.1 Military Applications**

Military applications were among the **first motivators** for WSN research.

- **Battlefield surveillance** — monitor troop movements, detect enemy activity
- **Enemy tracking** — track vehicles, equipment, and personnel positions
- **Nuclear, biological, chemical (NBC) detection** — sense hazardous agents
- **Damage assessment** — evaluate post-attack damage in real time
- **Smart weapons guidance** — sensors embedded in munitions

> Example: DARPA-funded programs like SensIT and Smart Dust were early WSN research initiatives for military use.

---

### **2.2 Environmental Monitoring**

- **Forest fire detection** — deploy nodes across forests; detect temperature/smoke anomalies before fires spread
- **Flood monitoring** — measure water levels in rivers and trigger alerts
- **Weather monitoring** — distributed sensing of temperature, humidity, wind, precipitation
- **Landslide detection** — detect ground movement patterns
- **Volcanic activity monitoring** — deploy sensors near volcanoes to detect seismic activity
- **Ecosystem monitoring** — track wildlife behavior, habitat conditions (e.g., Great Duck Island project)

---

### **2.3 Healthcare Applications**

- **Patient monitoring** — continuous monitoring of heart rate, blood pressure, SpO2, temperature
- **Hospital asset tracking** — track wheelchairs, IV pumps, defibrillators using RFID + sensors
- **Elderly care** — detect falls, monitor vital signs, alert caregivers
- **Drug administration** — ensure correct dosage and timing
- **Post-operative monitoring** — track recovery outside ICU
- **Epidemic detection** — monitor spread of infectious diseases

---

### **2.4 Industrial Applications**

- **Machine health monitoring** — detect vibration, temperature anomalies in motors/turbines
- **Process control** — monitor chemical, pressure, flow in industrial pipelines
- **Structural health monitoring** — monitor bridges, dams, buildings for cracks, stress
- **Supply chain management** — track goods in warehouses and during transit
- **Worker safety** — detect toxic gas levels in mines or chemical plants

---

### **2.5 Smart Home Applications**

- **Automation** — automatic control of lighting, HVAC, appliances based on occupancy
- **Security** — motion detectors, door/window sensors, surveillance
- **Energy management** — monitor and optimize power usage
- **Smart meters** — real-time electricity/water/gas consumption tracking
- **Elderly/children monitoring** — detect unusual activity patterns

---

### **2.6 Agriculture (Precision Farming)**

- **Soil monitoring** — soil moisture, pH, nitrogen levels for optimal irrigation and fertilization
- **Crop monitoring** — detect crop diseases, pest activity
- **Microclimate sensing** — temperature and humidity inside greenhouses
- **Livestock tracking** — GPS + sensors to track animal health and location
- **Irrigation automation** — activate/deactivate irrigation based on soil moisture thresholds

---

### **2.7 Disaster Management**

- **Earthquake early warning** — detect seismic activity, estimate magnitude
- **Tsunami detection** — underwater pressure sensors detect wave patterns
- **Flood early warning** — river/reservoir level monitoring
- **Post-disaster search and rescue** — deploy sensors in rubble to detect survivors
- **Infrastructure assessment** — monitor buildings after disasters

---

### **2.8 Transportation**

- **Traffic monitoring** — measure vehicle flow, detect congestion, control traffic lights
- **Vehicle tracking** — fleet management, cargo tracking
- **Parking management** — detect occupancy of parking spots
- **Road condition monitoring** — ice detection, pothole detection
- **Railway safety** — track status of rail lines, bridge loads

---

## **Section 3: Classification of Sensor Networks**

> PYQ: Discuss the classification of wireless sensor networks and its applications in detail. (May 2023, 15 marks)

Sensor networks can be classified along multiple dimensions based on deployment, mobility, communication model, and other factors.

---

### **3.1 By Deployment Strategy**

| Type | Description | Pros | Cons |
|---|---|---|---|
| **Random/Unplanned** | Nodes dropped from aircraft or scattered randomly | Fast deployment, suitable for hazardous areas | Coverage gaps, redundancy needed |
| **Deterministic/Planned** | Nodes placed at specific locations by hand | Optimal coverage, known topology | Time-consuming, not feasible in hostile areas |

---

### **3.2 By Mobility**

| Type | Description | Use Case |
|---|---|---|
| **Static** | Nodes remain fixed after deployment | Environment monitoring, structural monitoring |
| **Mobile** | Nodes (or some nodes) move during operation | Animal tracking, robot-assisted sensing |
| **Hybrid** | Some nodes static, some mobile (mobile sinks) | Data mule-based collection |

---

### **3.3 By Communication Model**

| Type | Description |
|---|---|
| **Single-hop** | Each sensor node communicates directly with the base station |
| **Multi-hop** | Data is relayed through intermediate nodes to reach the base station |

Multi-hop is preferred when nodes are far from the base station, as it **saves transmit energy**.

```
Single-hop:                     Multi-hop:
  [S1] ----\                    [S1] -> [S2] -> [S3] -> [BS]
  [S2] ----- [BS]              [S4] -> [S5] ---------> [BS]
  [S3] ----/
```

---

### **3.4 By Data Aggregation**

| Type | Description |
|---|---|
| **With Aggregation** | Intermediate nodes (cluster heads) combine/summarize data before forwarding — reduces traffic |
| **Without Aggregation** | Raw data forwarded directly to base station — higher accuracy but more energy consumption |

---

### **3.5 By Power Source**

| Type | Description |
|---|---|
| **Battery-powered** | Fixed energy budget; node dies when battery depletes |
| **Energy harvesting** | Solar, vibration, thermal energy used to recharge — potentially infinite lifetime |
| **Hybrid** | Battery + energy harvesting backup |

---

### **3.6 By Sensing Type**

| Type | Sensors Used | Examples |
|---|---|---|
| **Scalar** | Single value per reading | Temperature, pressure, humidity sensors |
| **Multimedia** | High bandwidth, stream data | Camera (image/video), microphone (audio) |

**Multimedia WSNs** (MWSNs) have additional challenges: higher data rates, more processing, and much more energy consumption.

---

### **3.7 Active vs Passive Sensors**

Sensors are also classified by how they **acquire** the physical signal:

| Aspect | **Active Sensors** | **Passive Sensors** |
|--------|--------------------|---------------------|
| **Definition** | Emit their own signal/energy and measure what is reflected/returned | Only detect/receive energy that is naturally emitted by the environment |
| **Energy use** | High — must power the emitter | Low — no emission, only sensing |
| **Examples** | Radar, LIDAR, ultrasonic range finder, active IR (motion), sonar | Thermometer, photodiode, microphone, humidity sensor, passive IR (PIR) |
| **Operating principle** | Transmit signal → wait for echo / reflection → measure delay or intensity | Capture ambient signal (light, heat, sound, vibration) directly |
| **Independence** | Works in darkness / no ambient signal needed | Depends on natural source (sunlight, body heat, ambient sound) |
| **Range** | Controllable (depends on emitter power) | Bounded by ambient signal strength |
| **Stealth** | Detectable (emissions can be sensed by others) | Undetectable (no emission) |
| **Use case in WSN** | Object detection, distance measurement, intrusion | Temperature monitoring, light sensing, audio surveillance |

**Quick recall:** *Active = emits + measures echo. Passive = listens only.*

---

## **Section 4: Architecture of Sensor Network**

> PYQ: Elaborate the sensor network architecture with a diagram. (May 2025, Dec 2025, 7 marks)  
> PYQ: Explain the architecture of wireless sensor network in detail. (Jul 2022, 15 marks)  
> PYQ: Discuss architecture of wireless sensor network with diagrammatic illustration. (Dec 2023, 15 marks)  
> PYQ: What are the main components of a sensor node? Discuss its role and limitations. (Dec 2025, 15 marks)

### **4.1 Sensor Node — Block Diagram**

A sensor node (mote) typically consists of four main subsystems:

```
+-------------------------------------------------------+
|                   SENSOR NODE                         |
|                                                       |
|  +------------------+    +------------------------+  |
|  |  SENSING UNIT    |    |   PROCESSING UNIT      |  |
|  |                  |    |                        |  |
|  | [Sensors]        |    | [Microcontroller]      |  |
|  |    |             |    |    |                   |  |
|  | [ADC]            |    | [Memory]               |  |
|  |  (Analog to      |    |  (Flash + SRAM)        |  |
|  |   Digital)       |    |                        |  |
|  +--------+---------+    +-----------+------------+  |
|           |                          |               |
|           +---------+  +-------------+               |
|                     |  |                             |
|              +------v--v-------+                     |
|              | COMMUNICATION   |                     |
|              |     UNIT        |                     |
|              | [Radio          |                     |
|              |  Transceiver]   |                     |
|              |  (TX + RX)      |                     |
|              +-----------------+                     |
|                                                       |
|  +---------------------------------------------------+|
|  |              POWER UNIT                           ||
|  |  [Battery] + [Energy Harvesting (optional)]       ||
|  |  [Power Management Circuit]                       ||
|  +---------------------------------------------------+|
+-------------------------------------------------------+
```

**Sensing Unit:**
- **Sensors** — transduce physical quantity into analog electrical signal
- **ADC (Analog-to-Digital Converter)** — converts analog signal to digital for processing

**Processing Unit:**
- **Microcontroller** — executes sensing, processing, MAC, routing protocols
- **Memory** — Flash (program storage) and SRAM (data/stack)

**Communication Unit:**
- **Radio Transceiver** — handles wireless transmission and reception
- Typically a short-range low-power radio (e.g., CC2420, nRF24L01)

**Power Unit:**
- **Battery** — primary energy source (AA, coin cell, or custom)
- **Energy harvesting** — solar panel, piezoelectric, thermoelectric (optional)
- **Power regulation circuit** — converts and regulates voltage

---

### **4.2 Network Architecture**

A WSN follows a layered network architecture:

```
+------------------+
|   User / Cloud   |   <-- Applications, dashboards, data analytics
+--------+---------+
         |
     (Internet)
         |
+--------+---------+
|   Base Station   |   <-- Sink node; collects all data, high-power device
|      (Sink)      |       connected to the internet
+--------+---------+
         |
    (Multi-hop
     wireless)
         |
+--------+---------+
|  Cluster Heads   |   <-- Aggregator nodes; collect data from member nodes
+--------+---------+
         |
+--------+---------+
|  Sensor Nodes    |   <-- Leaf nodes; sense and transmit data
+------------------+
```

**Sensor Nodes:** Smallest, most numerous, most resource-constrained. Sense the environment and send data to cluster heads or directly to the base station.

**Cluster Heads (CHs):** Elected periodically; aggregate data from cluster members. Have higher energy or are rotated among nodes. Reduce total traffic.

**Base Station (Sink):** Powerful node (often connected to mains power) that receives data from the entire network. Acts as a gateway to the internet.

**Internet / User:** End user accesses data via web/mobile applications.

---

### **4.3 Data Flow Diagram**

```
Physical World
     |
     | (Physical phenomenon)
     v
[Sensor Node]
     |  Sense -> ADC -> Process -> Compress/Encrypt
     |
     v (Radio transmission)
[Neighboring Node / Cluster Head]
     |  Aggregate / Forward
     v
[Base Station / Sink]
     |  Protocol conversion, store data
     v
[Internet]
     |
     v
[User Application]
     (Query, visualization, alerts)
```

#### **Data Relaying in WSN**

**Data relaying** is the process by which an intermediate sensor node forwards a packet — that it did not originate — toward the sink (base station) on behalf of another node. Because individual sensor nodes have **limited transmission range** and the sink is usually far away, packets must traverse the network in a **multi-hop** fashion: each node along the path *relays* the data for its neighbors.

```
[Source Node] --hop1--> [Relay 1] --hop2--> [Relay 2] --hop3--> [Sink]
                            ^                   ^
                            |                   |
                        forwards            forwards
                       other nodes'        other nodes'
                          data                data
```

**Why data relaying is needed:**
- **Range limitation** — direct sensor-to-sink communication would require high transmit power that drains batteries.
- **Energy efficiency** — short multi-hop transmissions cost less total energy than one long single-hop transmission.
- **Coverage** — extends the reachable area beyond any single node's radio range.

**Key concerns:**
- **Energy hole problem** — nodes nearest the sink relay everyone's data and die first.
- **Load balancing** — routing protocols rotate relay duty to extend network lifetime.
- **Reliability** — relay node failure breaks the path; multipath/redundant routing helps.

---

### **4.4 Network Topology Types**

#### **Flat Architecture**

All sensor nodes are peers. Each node communicates directly or via multi-hop to the base station. No special roles.

```
[S1] - [S2] - [S3]
  \             |
   [S4] - [S5]-[BS]
```

✅ Simple, robust, decentralized  
❌ Poor scalability, high energy cost for nodes far from BS

---

#### **Hierarchical / Cluster-based Architecture**

Nodes organized into clusters. Each cluster has a **Cluster Head (CH)** that aggregates data.

```
Cluster 1:          Cluster 2:
[S1][S2][S3]        [S6][S7][S8]
      |                   |
    [CH1]               [CH2]
       \                 /
        ----> [BS] <----
```

✅ Scalable, energy-efficient (data aggregation), extends lifetime  
❌ CH may become energy bottleneck; requires CH election protocol (e.g., LEACH)

---

#### **Tree-based Architecture**

Hierarchical tree rooted at the base station.

```
              [BS]
             /    \
          [CH1]  [CH2]
          / \      / \
        [S1][S2] [S3][S4]
```

✅ Structured, easy routing  
❌ Vulnerable to node failure (single point)

---

## **Section 5: Physical Layer**

> PYQ: Explain the physical and MAC layer of Wireless sensor network in detail. (May 2023, 15 marks)  
> PYQ: Explain the Physical Layer of WSN. (Jul 2022, part of 5×3=15 marks)

The **Physical (PHY) layer** is responsible for the actual transmission and reception of raw bits over the wireless channel.

---

### **5.1 Wireless Transmission Basics**

- Data is transmitted as **electromagnetic waves** through the air.
- Key parameters: **frequency**, **bandwidth**, **modulation**, **transmit power**, **antenna gain**
- Wireless channel introduces **path loss**, **shadowing**, **multipath fading**, and **interference**

---

### **5.2 Frequency Bands Used in WSN (ISM Bands)**

WSNs primarily use **ISM (Industrial, Scientific, Medical)** bands — unlicensed spectrum:

| Band | Frequency | Standard | Notes |
|---|---|---|---|
| **Low** | **868 MHz** | IEEE 802.15.4 | Europe; 1 channel; better range |
| **Medium** | **915 MHz** | IEEE 802.15.4 | Americas; 10 channels |
| **High** | **2.4 GHz** | IEEE 802.15.4 / WiFi / Bluetooth | Global; 16 channels; most common |

**Trade-offs:**
- Lower frequency → better range, less path loss, but narrower bandwidth
- Higher frequency → more channels available, but more path loss

---

### **5.3 Modulation Techniques**

**Modulation** converts digital data into analog signals suitable for wireless transmission.

#### **BPSK — Binary Phase Shift Keying**
- Two phase states: 0° and 180°
- 1 bit per symbol
- Simple, robust, used in low-data-rate WSN
- Used in 868/915 MHz band of IEEE 802.15.4

```
Bit:  0     1     0     1
      |     |     |     |
Phase: 0°   180°  0°   180°
```

#### **QPSK — Quadrature Phase Shift Keying**
- Four phase states: 0°, 90°, 180°, 270°
- 2 bits per symbol → higher spectral efficiency
- Used in 2.4 GHz band of IEEE 802.15.4 (O-QPSK variant)

```
Dibits: 00=0°, 01=90°, 10=180°, 11=270°
```

#### **FSK — Frequency Shift Keying**
- Different frequencies represent different bits
- More immune to amplitude noise
- Used in Bluetooth and some proprietary WSN radios

---

### **5.4 IEEE 802.15.4 Standard (Zigbee Physical Layer)**

**IEEE 802.15.4** is the foundational standard for low-rate wireless personal area networks (LR-WPAN), used by **Zigbee**, 6LoWPAN, and WirelessHART.

| Parameter | Value |
|---|---|
| **Standard** | IEEE 802.15.4-2003/2006/2011 |
| **Frequency bands** | 868 MHz, 915 MHz, 2.4 GHz |
| **Data rate** | 20/40/250 kbps |
| **Modulation** | BPSK (868/915 MHz), O-QPSK (2.4 GHz) |
| **Spreading** | DSSS (Direct Sequence Spread Spectrum) |
| **Range** | 10–100 m |
| **Channels** | 1 + 10 + 16 = 27 total |
| **TX power** | 1–100 mW |

**PHY Frame Structure (IEEE 802.15.4):**

```
+----------+----------+----------+----------+----------+
| Preamble | SFD      | PHR      |  PHY     | Payload  |
| (4 bytes)|(1 byte)  |(1 byte)  | Payload  | (PSDU)   |
|          |          |          | Length   | 0-127 B  |
+----------+----------+----------+----------+----------+
```

- **Preamble**: synchronization
- **SFD (Start Frame Delimiter)**: marks start of data
- **PHR (PHY Header)**: contains payload length
- **PSDU**: actual data payload

---

### **5.5 Propagation Models**

Propagation models describe how signal strength drops as distance increases.

#### **Free Space Model**

> **Analogy**: Like a light bulb in an empty room — the further you go, the dimmer it gets, and it drops off with the square of the distance.

- Signal power decreases with **d²** (double the distance → 4× weaker signal)
- Assumes **clear line-of-sight**, no obstacles or reflections
- Optimistic model — real environments are messier

#### **Two-Ray Ground Reflection Model**

> **Analogy**: Like shouting across an empty field — your voice travels directly to the listener, but also bounces off the ground and arrives slightly later, partially cancelling your direct signal.

- More realistic — signal travels via **two paths**: direct path + ground-reflected path
- Signal power decreases with **d⁴** — drops off much faster than free space
- Used for longer distances over flat terrain (outdoor fields, farmland)

| Model | Power drop | When to use |
|-------|-----------|-------------|
| **Free Space** | d² | Short range, clear line-of-sight |
| **Two-Ray** | d⁴ | Longer outdoor distances, flat terrain |

---

### **5.6 Energy Consumption at Physical Layer**

The PHY layer is the **dominant energy consumer** in a sensor node.

| Operation | Energy Cost |
|---|---|
| Transmitting | Highest |
| Receiving | High (similar to TX) |
| Idle listening | Significant (radio ON but not receiving) |
| Sleep mode | Very low |

Key insight: **Idle listening wastes almost as much energy as active receiving**. MAC protocols exploit sleep scheduling to minimize idle listening.

---

## **Section 6: MAC Layer**

> PYQ: What is MAC Layer? (Dec 2023, 2.5 marks)  
> PYQ: Explain MAC protocols for wireless sensor Networks. (May 2025, 8 marks)  
> PYQ: Present an overview of MAC protocols for wireless sensor networks. (Dec 2023, 15 marks)  
> PYQ: List the design goals of MAC protocol for ad-hoc networks. (May 2025, 15 marks)  
> PYQ: List the issues of designing a MAC protocol for ad hoc networks. (Dec 2025, 8 marks)  
> PYQ: Explain the physical and MAC layer of Wireless sensor network in detail. (May 2023, 15 marks)  
> PYQ: Explain the MAC Layer of WSN. (Jul 2022, part of 5×3=15 marks)

The **Medium Access Control (MAC) layer** controls how sensor nodes share the wireless channel. In WSN, MAC design is **energy-centric**, unlike traditional MACs that focus on throughput and fairness.

---

### **6.1 Role of MAC in WSN**

- **Coordinate channel access** — prevent collisions among nodes
- **Energy efficiency** — minimize idle listening, overhearing, collisions
- **Latency** — acceptable delay for data delivery
- **Scalability** — support varying network sizes
- **Adaptability** — handle changes in network topology

---

### **6.1.1 Design Goals of MAC Protocol for Ad-Hoc Networks**

A MAC protocol for an ad-hoc / sensor network must satisfy the following **design goals**:

1. **Distributed operation** — no central coordinator (no AP / base station); every node decides on its own.
2. **Energy efficiency** — minimize power-hungry states (idle listening, overhearing, control overhead).
3. **Fair channel access** — give every node a reasonable share of bandwidth without starvation.
4. **High throughput & low latency** — maximize successful transmissions and minimize delivery delay.
5. **Support for QoS** — provide differentiated service for real-time vs best-effort traffic.
6. **Scalability** — performance must not degrade sharply as node density or network size grows.
7. **Adaptability to mobility** — handle topology changes from node movement, joins, and failures.
8. **Hidden / exposed terminal handling** — coordinate transmissions to avoid collisions at the receiver and to avoid unnecessary backoff.
9. **Synchronization tolerance** — operate with minimal or no global clock synchronization.
10. **Time-bounded delivery (where required)** — for real-time data such as alerts.

---

### **6.1.2 Issues / Challenges in Designing MAC for Ad-Hoc Networks**

The above goals are difficult because of the following **design issues** unique to ad-hoc networks:

| Issue | Why it matters |
|------|----------------|
| **Shared, error-prone wireless medium** | Multipath fading, interference cause packet loss not seen in wired MACs |
| **Hidden terminal problem** | Two senders out of each other's range collide at the common receiver |
| **Exposed terminal problem** | Sender unnecessarily defers because it overhears an unrelated transmission |
| **Lack of central coordinator** | Cannot rely on AP scheduling — every node must negotiate access |
| **Mobility-induced topology changes** | Neighbor lists keep changing; static schedules go stale |
| **Energy constraint** | Battery-powered nodes — cannot use power-hungry MACs like full-duplex carrier sense |
| **Time synchronization difficulty** | TDMA-style slotting needs synchronization that is expensive in ad-hoc settings |
| **Half-duplex radio** | Most radios cannot transmit and receive simultaneously — collision detection is impossible (CSMA/CD doesn't work) |
| **Bandwidth limitation** | Wireless capacity is far below wired; control overhead becomes significant |
| **QoS support** | Hard to guarantee delay/jitter bounds on a shared, unreliable channel |

These constraints rule out classical Ethernet-style CSMA/CD and force MAC designs to use **CSMA/CA**, **RTS/CTS**, **scheduled (TDMA)**, **hybrid** (Z-MAC), or **duty-cycled** (S-MAC, B-MAC) approaches.

---

### **6.2 Sources of Energy Waste at MAC Layer**

These are the four primary causes of energy wastage:

| Source | Description |
|---|---|
| **Idle Listening** | Radio ON and listening when no data is arriving — wasted energy |
| **Overhearing** | Receiving packets addressed to other nodes — wasted reception |
| **Collision** | Two nodes transmit simultaneously → packet corrupted → retransmit |
| **Control Overhead** | Transmission of control packets (RTS, CTS, ACK) consumes energy |

```
Energy Waste Sources:
┌─────────────────────┐
│  Idle Listening     │  ← Most common waste
│  Overhearing        │  ← Dense networks
│  Collision          │  ← Contention-based MACs
│  Control Overhead   │  ← Excessive handshaking
└─────────────────────┘
```

---

### **6.3 Types of MAC Protocols**

WSN MAC protocols fall into three categories:

#### **Schedule-Based (TDMA)**

- Time is divided into slots; each node is assigned specific slots to transmit.
- No collisions, no idle listening during off-slots.
- Examples: **TDMA, TRAMA, S-MAC (partial)**

✅ No collisions  
✅ Predictable latency  
✅ Energy-efficient  
❌ Requires time synchronization  
❌ Less adaptive to dynamic traffic  

---

#### **Contention-Based (CSMA)**

- Nodes compete for the channel; listen before transmitting.
- Examples: **CSMA/CA (IEEE 802.15.4), ALOHA**

✅ No synchronization needed  
✅ Adapts to traffic load  
❌ Collisions possible  
❌ Idle listening waste  

---

#### **Hybrid**

- Combines TDMA and CSMA features.
- Examples: **Z-MAC, TDMA+CSMA hybrid**

✅ Flexibility of CSMA + efficiency of TDMA  
❌ More complex design  

---

### **6.4 S-MAC Protocol (Sensor MAC)**

**S-MAC** is one of the most important energy-efficient MAC protocols for WSN.

**Key Idea:** Nodes follow a **periodic sleep/listen cycle**. During the listen period, they can send/receive. During sleep, the radio is OFF.

#### **Operation:**

1. Each node follows a **duty cycle**: Listen for a short period, then sleep.
2. Nodes exchange **SYNC** packets to synchronize their schedules.
3. Neighboring nodes form **virtual clusters** — nodes with the same schedule.
4. Nodes on different schedules have **border nodes** that follow both schedules.

**Duty Cycle:**

```
|<--------- Period T -------->|
|  Listen  |     Sleep        |  Listen  |     Sleep        |
|<--Tl--->|<-------Ts------->|<--Tl--->|<-------Ts------->|

Duty cycle = Tl / T  (typically 10%)
```

**Frame Structure during Listen:**

```
|  SYNC  |  DATA   |
|  slot  |  slot   |
```

- **SYNC slot**: Nodes exchange synchronization information
- **DATA slot**: Actual data transmission using RTS/CTS/DATA/ACK

#### **Virtual Clusters:**

```
+--Group A (same schedule)--+    +--Group B--+
| [S1] [S2] [S3]            |    | [S4] [S5] |
|        |                  |    |    |       |
|      [S3]=border node=====+====+=[S4]       |
+---------------------------+    +-----------+
```

Border nodes follow both Group A and Group B schedules.

#### **Message Passing (RTS/CTS):**

```
Sender:   |--RTS-->|         |--DATA-->|
Receiver: |        |<--CTS---|         |--ACK-->|
```

Nodes that overhear RTS or CTS go to sleep for the duration of the transmission (reduces overhearing).

✅ Reduces idle listening dramatically  
✅ Good for low-traffic WSN  
❌ Latency increases with more hops (adaptive listening reduces this)  
❌ Border nodes wake up more, consuming extra energy  

---

### **6.5 IEEE 802.15.4 MAC**

The IEEE 802.15.4 MAC supports two modes:

#### **Beacon-Enabled Mode (Superframe Structure)**

A **coordinator** (e.g., cluster head or PAN coordinator) sends periodic **beacons** to synchronize the network.

```
|<---------------------- Superframe ---------------------------->|
|  Beacon | CAP (Contention Access Period) | CFP (TDMA slots)  |
|         | CSMA-CA based                  | GTS (Guaranteed   |
|         |                                | Time Slots)       |

Active: |<-------Active portion-------->|<----Inactive------->|
                                         (nodes sleep here)
```

- **CAP**: Contention-based (CSMA-CA) for general data
- **CFP**: TDMA-like guaranteed time slots (GTS) for time-critical data

#### **Non-Beacon Mode**

No synchronization. Nodes use **unslotted CSMA-CA**:

1. Node wants to transmit → Backs off random number of slots
2. Perform **CCA (Clear Channel Assessment)** — check if channel is idle
3. If idle → transmit; If busy → wait and retry
4. After fixed retries, declare failure

**Slotted CSMA-CA (Beacon mode):**

```
CW=2 (initial contention window)
BE=macMinBE (initial backoff exponent)

1. Set NB=0, CW=2, BE=macMinBE
2. Delay random(0, 2^BE - 1) backoff periods
3. Perform CCA
4. If idle: decrement CW; if CW=0, transmit
5. If busy: NB++, BE=min(BE+1, macMaxBE), CW=2
6. If NB > macMaxCSMABackoffs: declare failure
```

---

### **6.6 Z-MAC (Zebra MAC)**

**Z-MAC** is a hybrid MAC protocol that uses:
- **CSMA** under low traffic (flexible, low latency)
- **TDMA** under high traffic (efficient, collision-free)

Each node is assigned a TDMA slot but can also use others' slots when idle. Switches between modes based on detected contention.

---

### **6.7 Comparison: TDMA vs CSMA/CA for WSN**

| Feature | TDMA | CSMA/CA |
|---|---|---|
| **Collisions** | None | Possible |
| **Idle listening** | Minimal (sleep in off-slots) | Can be significant |
| **Synchronization** | Required | Not required |
| **Latency** | Predictable | Variable |
| **Overhead** | Slot assignment overhead | Backoff overhead |
| **Scalability** | Poor (fixed slot assignment) | Better |
| **Adaptability** | Low | High |
| **Energy efficiency** | Very high | Moderate |
| **Suitable for** | Periodic data, time-critical | Bursty traffic, simple deployment |

---

## **Section 7: Link Layer**

> PYQ: What is a Link Layer? (Jul 2022, 2.5 marks)  
> PYQ: Explain the Link Layer of WSN. (Jul 2022, part of 5×3=15 marks)

The **Link Layer** (Data Link Layer) ensures reliable frame delivery between directly connected nodes. In WSN, links are often **lossy** due to interference, fading, and node mobility, making link-layer reliability critical.

---

### **7.1 Role of Link Layer in WSN**

- **Framing**: Package data into frames with headers and trailers
- **Error detection**: Detect bit errors introduced by the channel
- **Error correction**: Recover from errors without retransmission (FEC)
- **Retransmission**: Request retransmission of lost/corrupted frames (ARQ)
- **Link quality estimation**: Measure channel quality for routing decisions

---

### **7.2 Error Detection: CRC**

**CRC (Cyclic Redundancy Check)** is the standard error detection method in WSN.

**How it works:**

1. Sender divides the message polynomial by a **generator polynomial G(x)**
2. The **remainder** is appended to the frame as the CRC field
3. Receiver divides the received frame by G(x)
4. If remainder is 0 → no error; else → error detected

```
Sender:
  Message M:   1101011011
  Generator G: 10011 (CRC-4)
  
  Append zeros: 11010110110000
  Divide by G:  compute remainder R
  Transmitted:  Message + R

Receiver:
  Divide (Message + R) by G
  Remainder = 0 → no error
  Remainder ≠ 0 → error detected → discard frame
```

**Common CRC variants:**
- **CRC-8**: 8-bit check (simple, lightweight for WSN)
- **CRC-16**: 16-bit check (used in many protocols)
- **CRC-32**: 32-bit check (stronger, used in Ethernet)

IEEE 802.15.4 uses **CRC-16** (ITU-T polynomial: 0x1021)

✅ Can detect all single-bit errors, burst errors  
❌ Cannot correct errors — only detection  

---

### **7.3 Error Correction: FEC**

**FEC (Forward Error Correction)** allows the receiver to **correct** errors without requesting retransmission.

**How it works:**
- Sender adds **redundant bits** (parity/coding bits) to the data
- Receiver uses the redundancy to detect AND correct errors

**Common FEC codes:**

| Code | Type | Capability |
|---|---|---|
| **Hamming Code** | Block code | Correct 1-bit, detect 2-bit errors |
| **Reed-Solomon** | Block code | Correct burst errors |
| **Convolutional Code** | Stream code | Flexible error correction |
| **Turbo Codes** | Block + iterative | Near Shannon limit |
| **LDPC** | Block code | Very high performance |

**In WSN:** Simple FEC like Hamming code is preferred due to low computational overhead.

**Trade-off:**
- FEC adds overhead (larger frames → more energy to transmit)
- FEC saves retransmission energy in high-error environments
- **FEC is preferred when link error rate is high and retransmission cost is high**

---

### **7.4 ARQ — Automatic Repeat Request**

**ARQ** relies on the receiver to detect errors (using CRC) and request retransmission.

Three main ARQ protocols:

#### **Stop-and-Wait ARQ**

Sender transmits **one frame** and waits for ACK before sending next.

```
Sender:   [Frame 0] ---------> 
Receiver:           <--------- [ACK 0]
Sender:   [Frame 1] ---------> 
Receiver:           <--------- [ACK 1]
          ...
```

If no ACK within timeout → retransmit same frame.

✅ Simple to implement  
❌ Low efficiency — channel idle while waiting for ACK  
❌ High latency  

---

#### **Go-Back-N ARQ**

Sender can transmit **N frames** (window size N) without waiting for ACK.

```
Window size N=4:
Sender:   [0][1][2][3][4] ...
                  ^-- Error at frame 2
Receiver:          NACK-2
Sender:   [2][3][4][5] ...   (go back to frame 2, resend all)
```

If frame i is corrupted → receiver **rejects all subsequent frames** → sender **retransmits from frame i**.

✅ Better channel utilization than stop-and-wait  
❌ Retransmits correctly received frames — wasteful  

---

#### **Selective Repeat ARQ**

Sender transmits up to N frames; receiver **buffers** out-of-order frames.

```
Window size N=4:
Sender:   [0][1][2][3][4] ...
                  ^-- Error at frame 2
Receiver: Accepts 0,1,3,4 (buffers out-of-order)
          NACK-2
Sender:   [2] only (selective retransmit)
```

✅ Most efficient — only lost frames are retransmitted  
❌ More complex — requires receiver buffering  

---

#### **ARQ in WSN Context**

| Protocol | WSN Suitability |
|---|---|
| Stop-and-Wait | ✅ Simple, low memory, used in simple WSN links |
| Go-Back-N | Moderate — moderate buffer needed |
| Selective Repeat | Best efficiency but needs buffer memory (limited in WSN) |

In WSN, **Stop-and-Wait or simple link-layer retransmission** is often used due to memory constraints. Higher-layer protocols may handle end-to-end reliability.

---

### **7.5 Link Quality Indicators**

#### **RSSI — Received Signal Strength Indicator**

- Measures the **power level** of the received signal in dBm
- Higher RSSI → stronger signal → better link quality
- Affected by distance, obstacles, interference

```
RSSI Range (typical):
  -40 dBm : Excellent
  -70 dBm : Good
  -85 dBm : Fair
  -100 dBm: Very poor / packet loss likely
```

#### **LQI — Link Quality Indicator**

- A composite metric measuring the **quality of the received signal** at the PHY layer
- In IEEE 802.15.4: LQI is computed from the **energy of received symbols** and **correlation** with ideal symbols
- Range: 0–255 (higher = better)
- Used by routing protocols to select reliable paths

#### **PRR — Packet Reception Rate**

- Fraction of successfully received packets over a period
- More accurate than RSSI/LQI as it measures actual link performance

```
PRR = (Packets received) / (Packets sent)
```

---

### **7.6 Why Link-Layer Reliability Matters in WSN**

WSN links are inherently **lossy**:
- **Multipath fading** — reflections cause constructive/destructive interference
- **Interference** — other devices using the same ISM band (WiFi, Bluetooth, microwaves)
- **Node mobility** — changing topology in mobile WSNs
- **Environmental dynamics** — moving objects, weather changes

**Consequences of lossy links:**
- Increased retransmissions → more energy consumption
- Reduced throughput
- Higher end-to-end latency

**Link-layer mechanisms to address lossy links:**
- CRC for error detection
- FEC for error correction without retransmission
- ARQ for reliable delivery
- Link quality estimation (RSSI, LQI) to select better routes
- **Adaptive modulation** — switch to lower-rate, more robust modulation on bad links

---

## **Quick Revision Points**

### WSN Fundamentals
- WSN = distributed network of sensor nodes sensing physical phenomena and reporting to a base station
- Key constraints: **energy (dominant), memory, processing, communication range**
- WSN differs from MANET in: data-centric, mostly static, many-to-one traffic, thousands of nodes

### Applications
- Military, environmental monitoring, healthcare, industrial, smart home, agriculture, disaster management, transportation
- Motivating factor: sensing in **inaccessible, hazardous, or large-scale** environments

### Classification
- Deployment: random vs deterministic
- Mobility: static vs mobile vs hybrid
- Communication: single-hop vs multi-hop
- Data: with/without aggregation
- Power: battery vs energy harvesting
- Sensing: scalar vs multimedia

### Architecture
- Sensor node = **Sensing unit + Processing unit + Communication unit + Power unit**
- Network layers: **Sensor nodes → Cluster Heads → Base Station → Internet → User**
- Topologies: Flat, Hierarchical/Cluster-based, Tree-based
- LEACH is a classic cluster-based protocol with random CH rotation

### Physical Layer
- ISM bands: **868 MHz (Europe), 915 MHz (Americas), 2.4 GHz (Global)**
- Modulation: **BPSK** (868/915 MHz), **O-QPSK** (2.4 GHz) in IEEE 802.15.4
- IEEE 802.15.4: data rate **250 kbps** at 2.4 GHz, uses DSSS
- Propagation: free space (d²), two-ray (d⁴)
- Energy: **TX dominant; idle listening nearly as costly as RX**

### MAC Layer
- Energy waste: **idle listening, overhearing, collision, control overhead**
- TDMA: no collision, needs sync, energy-efficient
- CSMA/CA: no sync needed, flexible, collisions possible
- **S-MAC**: periodic sleep/listen, virtual clusters, RTS/CTS during listen
- IEEE 802.15.4 MAC: **beacon-enabled** (superframe, CAP+CFP) and **non-beacon** (unslotted CSMA-CA)
- Z-MAC: hybrid CSMA+TDMA

### Link Layer
- CRC: error **detection** (IEEE 802.15.4 uses CRC-16)
- FEC: error **correction** (Hamming, Reed-Solomon) — no retransmission needed
- ARQ: Stop-and-Wait (simple, low memory), Go-Back-N, Selective Repeat (most efficient)
- RSSI: received power level; LQI: link quality (0–255); PRR: packet reception rate
- WSN links are lossy → link-layer reliability is critical

---

## **Expected Exam Questions**

### **15-mark Questions**

1. Explain the architecture of wireless sensor network in detail. *(Jul 2022)*
2. Discuss architecture of wireless sensor network with diagrammatic illustration. *(Dec 2023)*
3. Discuss the classification of wireless sensor networks and its applications in detail. *(May 2023)*
4. Explain the physical and MAC layer of Wireless sensor network in detail. *(May 2023)*
5. Explain the following layers of WSN: Physical, MAC, Link. *(Jul 2022)*
6. Present an overview of MAC protocols for wireless sensor networks. *(Dec 2023)*
7. List the design goals of MAC protocol for ad-hoc networks. *(May 2025)*
8. What are the main components of a sensor node? Discuss its role and limitations. *(Dec 2025)*

### **7–8 mark Questions**

1. Elaborate the sensor network architecture with a diagram. *(May 2025, Dec 2025)*
2. Explain MAC protocols for wireless sensor Networks. *(May 2025)*
3. List the issues of designing a MAC protocol for ad hoc networks. *(Dec 2025)*

### **Short Answer (2.5–3 marks)**

1. What is a Wireless sensor network? *(Dec 2023)*
2. What is WSN? *(Jul 2022)*
3. What is MAC Layer? *(Dec 2023)*
4. What is a Link Layer? *(Jul 2022)*
5. Explain Sensors. *(May 2023)*
6. Differentiate between active and passive sensors. *(May 2025)*
7. Difference between cellular network and ad-hoc wireless network. *(Dec 2023)*
8. What is data relaying in wireless sensor network? *(Dec 2023)*

---

_These notes were compiled by [Deepak Modi](https://deepakmodi.dev)_  
_Last updated: May 2026_
