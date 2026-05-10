---
title: "Unit 1: Introduction to Big Data"
description: "Why and Where Big Data, Applications and Challenges, Characteristics (6 V's), Dimensions of Scalability, Data Science process, Foundations of Big Data Systems, and Distributed File Systems."
author: "Deepak Modi"
date: "2026-05-10"
pdfUrl: ""
---

## Syllabus:

**Introduction to Big Data:** Big Data: Why and Where, Application and Challenges, Characteristics of Big Data and Dimensions of Scalability, The Six V, Data Science: Getting Value out of Big Data, Steps in the Data science process, Foundations for Big Data Systems and Programming, Distributed file systems.

---

## 🎯 PYQ Analysis for Unit 1

> PYQs will be added after analysis — check back soon.

---

## **Section 1: Big Data — Why and Where**

### **1.1 What is Big Data?**

**Definition:**

**Big Data** refers to extremely **large and complex datasets** that cannot be processed, stored, or analyzed using **traditional data management tools** (like regular databases or spreadsheets) within a reasonable time.

The term "Big Data" describes data that is:
- Too large to fit on one machine.
- Generated too fast to process in real time with traditional systems.
- Too varied in format to fit in a single table.

> **Simple Definition:** Big Data is data that is so big, fast, or complex that traditional methods can't handle it.

**Real-Life Scale:**

```
Every day:
  Google processes  → 8.5 billion searches
  YouTube receives  → 500 hours of video per minute uploaded
  Facebook generates→ 4 petabytes of data
  Twitter sees      → 500 million tweets
  WhatsApp sends    → 100 billion messages
```

---

### **1.2 Why Big Data? (The Need)**

Data has always existed, but several forces have **exploded the volume** beyond what old tools can handle:

**1. Digitization of Everything:**
- Everything is now recorded digitally — transactions, clicks, GPS location, health sensors.
- Every smartphone is a data generator.

**2. Internet and Social Media:**
- Billions of people use the internet every day.
- Each like, comment, post, search, and purchase generates data.

**3. IoT (Internet of Things):**
- Smart devices (sensors, wearables, smart appliances) continuously stream data.
- Example: A smart factory has thousands of sensors generating data every second.

**4. E-commerce and Digital Transactions:**
- Every purchase, product view, and abandoned cart is recorded.
- Amazon processes millions of transactions per day.

**5. Healthcare and Science:**
- Genomics, medical imaging, clinical trials generate enormous datasets.
- A single human genome = ~3 GB of data.

**6. Cheaper Storage and Computing:**
- Cost of storing 1 GB dropped from thousands of dollars (1980) to fractions of a cent (now).
- Cloud computing made large-scale processing affordable.

---

### **1.3 Where Does Big Data Come From? (Sources)**

**Data Sources:**

```
                    ┌──────────────────────────┐
                    │       Big Data Sources   │
                    └────────────┬─────────────┘
         ┌──────────────┬────────┴────────┬──────────────┐
         ▼              ▼                 ▼              ▼
   Social Media    Machine / IoT    Transactional    Web / Logs
   ───────────    ─────────────    ─────────────    ──────────
   Facebook       Sensors          Bank records     Clickstreams
   Twitter        GPS devices      E-commerce       Server logs
   Instagram      Smart meters     Healthcare       Search queries
   LinkedIn       RFID tags        Insurance        App usage
```

**Categories of Data Sources:**

| Source Type | Examples | Data Type |
|-------------|----------|-----------|
| **Social Media** | Facebook, Twitter, YouTube | Text, images, video |
| **Machine / Sensor** | IoT devices, GPS, RFID | Numeric streams |
| **Transaction** | Banks, e-commerce, hospitals | Structured records |
| **Web** | Logs, click-streams, search | Semi-structured |
| **Scientific** | Genomics, astronomy, climate | Numeric, images |
| **Enterprise** | ERP, CRM, supply chain | Structured |

---

## **Section 2: Applications and Challenges**

### **2.1 Applications of Big Data**

**1. Healthcare:**
- **Disease prediction** — analyzing patient history to predict illness.
- **Drug discovery** — finding drug interactions using genetic data.
- **Epidemic tracking** — monitoring disease spread (COVID-19 dashboards).
- **Personalized medicine** — treatment based on individual genome.

**2. Finance and Banking:**
- **Fraud detection** — real-time anomaly detection on credit card transactions.
- **Risk assessment** — evaluating loan default probability.
- **Algorithmic trading** — high-frequency trading decisions from market data.
- **Customer 360** — full customer profile from all touchpoints.

**3. Retail and E-commerce:**
- **Recommendation engines** — Amazon/Netflix "you may also like".
- **Demand forecasting** — predicting inventory needs.
- **Price optimization** — dynamic pricing based on demand.
- **Customer sentiment** — analyzing reviews and social media.

**4. Transportation:**
- **Traffic management** — real-time rerouting (Google Maps).
- **Predictive maintenance** — airlines predicting engine failures before they happen.
- **Ride-sharing optimization** — Uber/Ola surge pricing and driver allocation.
- **Self-driving cars** — processing sensor data in real time.

**5. Government and Smart Cities:**
- **Public safety** — crime hotspot prediction.
- **Energy management** — smart grid optimization.
- **Citizen services** — tax fraud detection, welfare eligibility.
- **Disaster response** — resource allocation using real-time data.

**6. Telecommunications:**
- **Churn prediction** — identify customers likely to switch providers.
- **Network optimization** — identifying bottlenecks using call data records.
- **Personalized plans** — usage-based plan recommendations.

**7. Manufacturing:**
- **Predictive maintenance** — prevent machine breakdowns using sensor data.
- **Quality control** — defect detection using computer vision.
- **Supply chain optimization** — reducing delays and wastage.

**8. Agriculture:**
- **Crop yield prediction** using satellite + weather data.
- **Precision farming** — targeted irrigation and fertilization.
- **Disease detection** — identifying crop disease from drone imagery.

---

### **2.2 Challenges of Big Data**

Despite its potential, Big Data comes with significant challenges:

**1. Storage:**
- Petabytes and exabytes of data need massive, scalable storage.
- Traditional RDBMS cannot store semi-structured or unstructured data.

**2. Processing Speed:**
- Data arrives faster than it can be processed (streaming data).
- Batch processing too slow for real-time use cases.

**3. Data Variety:**
- Data comes in structured, semi-structured, and unstructured formats.
- Integrating text, images, video, JSON, XML, CSV is complex.

**4. Data Quality:**
- Raw big data is often dirty — missing values, duplicates, inconsistencies.
- "Garbage In, Garbage Out" — poor quality input = poor insights.

**5. Privacy and Security:**
- Handling sensitive data (medical, financial) requires strict compliance.
- Risk of data breaches at scale.
- GDPR, HIPAA, and other regulations must be followed.

**6. Talent Gap:**
- Shortage of skilled data engineers, data scientists, and architects.

**7. Cost:**
- Infrastructure (servers, cloud, bandwidth) is expensive.
- ROI must justify the investment.

**8. Data Governance:**
- Deciding who owns data, who can access it, and how long to keep it.

---

## **Section 3: Characteristics of Big Data — The 6 V's**

### **3.1 What are the V's of Big Data?**

The characteristics of Big Data are described using **V's**. Originally there were **3 V's** (Gartner, 2001), which expanded to **6 V's** over time.

```
                     ┌─────────────┐
                     │  BIG DATA   │
                     └──────┬──────┘
         ┌──────────────────┼──────────────────┐
         ▼          ▼       ▼      ▼     ▼     ▼
      Volume    Velocity  Variety Veracity Value Variability
```

---

### **3.2 The 6 V's — Detailed**

#### **V1 — Volume**

**Definition:** The **amount / size** of data being generated and stored.

- We have moved from **gigabytes → terabytes → petabytes → exabytes**.
- Traditional systems crash under this load.

**Scale Reference:**

```
1 KB  = 1,000 bytes
1 MB  = 1,000 KB     (one song)
1 GB  = 1,000 MB     (a movie)
1 TB  = 1,000 GB     (a library of books)
1 PB  = 1,000 TB     (Facebook stores ~100 PB)
1 EB  = 1,000 PB     (all internet traffic per month)
1 ZB  = 1,000 EB     (total global data in 2020 ≈ 40 ZB)
```

**Challenge:** Where to store this? → **Distributed File Systems (HDFS)**

---

#### **V2 — Velocity**

**Definition:** The **speed** at which data is generated and must be processed.

- Twitter generates ~6,000 tweets per second.
- Stock exchange processes millions of trades per second.
- IoT devices stream data continuously.

**Types of Processing:**

```
Batch Processing:   Collect data → Process later (hours/days)
                    Example: Monthly billing reports

Stream Processing:  Process data as it arrives (milliseconds)
                    Example: Fraud detection, live traffic
```

**Challenge:** How to process fast enough? → **Apache Kafka, Apache Storm, Spark Streaming**

---

#### **V3 — Variety**

**Definition:** The **diversity of data types and formats** in Big Data.

**Three Types of Data:**

```
┌──────────────────┬──────────────────┬─────────────────────┐
│   Structured     │ Semi-Structured   │   Unstructured      │
├──────────────────┼──────────────────┼─────────────────────┤
│ Fixed schema     │ Flexible schema   │ No fixed schema     │
│ Rows & columns   │ Tags / key-value  │ Free-form           │
│ SQL databases    │ JSON, XML, CSV    │ Text, images, video │
│ Example:         │ Example:          │ Example:            │
│ Bank records     │ Twitter API data  │ Medical images      │
└──────────────────┴──────────────────┴─────────────────────┘
```

**Challenge:** How to store and query all formats? → **NoSQL databases, Data Lakes**

---

#### **V4 — Veracity**

**Definition:** The **quality, accuracy, and trustworthiness** of the data.

- Big Data is often noisy, incomplete, biased, or inconsistent.
- Wrong data leads to wrong conclusions → dangerous in healthcare or finance.

**Sources of bad veracity:**
- Sensor malfunction → wrong readings.
- User input errors → misspelled names, wrong dates.
- Social media noise → sarcasm, fake news, bots.
- Missing values → incomplete records.

**Challenge:** How to ensure data quality? → **Data cleaning, validation pipelines, data governance**

---

#### **V5 — Value**

**Definition:** The **usefulness or business benefit** derived from analyzing the data.

- Not all big data is valuable. Most raw data has low value density.
- The goal is to extract **high-value insights** from low-value-density data.

**Value Chain:**
```
Raw Data → Processed Data → Information → Knowledge → Wisdom → Business Value
```

**Example:** A billion web clicks have low individual value, but analyzed together they reveal purchasing patterns worth millions in targeted ads.

**Challenge:** How to extract value efficiently? → **ML models, analytics platforms, BI tools**

---

#### **V6 — Variability**

**Definition:** The **inconsistency in data** — same data meaning different things at different times or contexts.

- A word like "bank" can mean a financial institution or a river bank.
- Sentiment of a tweet depends on context and time.
- Data formats change over time.

**Difference from Variety:**
- **Variety** = different types of data (text vs video).
- **Variability** = the same type of data having inconsistent meaning or format.

**Challenge:** Context-aware processing, NLP, semantic analysis.

---

### **3.3 Summary Table — The 6 V's**

| V | Name | Question it Answers | Challenge |
|---|------|---------------------|-----------|
| **V1** | Volume | How much? | Storage, scalability |
| **V2** | Velocity | How fast? | Real-time processing |
| **V3** | Variety | What types? | Integration, NoSQL |
| **V4** | Veracity | How accurate? | Data quality, cleaning |
| **V5** | Value | How useful? | Insight extraction |
| **V6** | Variability | How consistent? | Context, semantics |

---

## **Section 4: Dimensions of Scalability**

### **4.1 What is Scalability?**

**Scalability** is the ability of a system to handle **growing amounts of work** (more data, more users, more requests) by adding resources.

### **4.2 Two Types of Scaling**

#### **Vertical Scaling (Scale Up)**

```
Before:           After:
┌─────────┐       ┌──────────────┐
│ Server  │  ──►  │ Bigger Server│
│ 8 GB    │       │ 64 GB RAM    │
│ 4 cores │       │ 32 cores     │
└─────────┘       └──────────────┘
```

- Add more CPU, RAM, or disk to a **single machine**.
- Simple but has physical limits.
- Expensive at high end.
- Single point of failure.

#### **Horizontal Scaling (Scale Out)**

```
Before:          After:
┌─────────┐      ┌─────┐ ┌─────┐ ┌─────┐
│ Server  │ ──►  │ S1  │ │ S2  │ │ S3  │
└─────────┘      └─────┘ └─────┘ └─────┘
```

- Add **more machines** (nodes) to a cluster.
- Big Data systems use horizontal scaling (commodity hardware).
- Basis of Hadoop, Spark, NoSQL.

| | Vertical | Horizontal |
|--|---------|------------|
| How | Bigger machine | More machines |
| Cost | High per unit | Low (commodity) |
| Limit | Physical hardware limit | Virtually unlimited |
| Failure | Single point of failure | Fault tolerant |
| Big Data fit | Poor | Excellent |

### **4.3 Dimensions of Scalability in Big Data**

| Dimension | What scales? | Example |
|-----------|-------------|---------|
| **Data Volume** | Amount of stored data | Adding more HDFS nodes |
| **Throughput** | Data processed per second | More Spark workers |
| **Query Speed** | Response time for queries | Partitioning, indexing |
| **Concurrency** | Simultaneous users/jobs | Load balancing |
| **Geographic** | Multiple data centers | Cloud regions (AWS) |

---

## **Section 5: Data Science — Getting Value out of Big Data**

### **5.1 What is Data Science?**

**Definition:**

**Data Science** is an interdisciplinary field that uses **scientific methods, algorithms, and systems** to extract **knowledge and insights** from structured and unstructured data.

It combines:
- **Statistics** — mathematical analysis
- **Computer Science** — programming and algorithms
- **Domain Knowledge** — understanding of the specific field

**Data Science vs Big Data:**

| | Big Data | Data Science |
|--|---------|-------------|
| **Focus** | Infrastructure to store and process large data | Methods to extract insights from data |
| **Tools** | Hadoop, Spark, HDFS | Python, R, ML, Statistics |
| **Role** | Data Engineer | Data Scientist |
| **Output** | Scalable pipelines | Actionable insights |

---

### **5.2 Steps in the Data Science Process**

The data science process is a structured workflow for turning raw data into valuable insights.

**Overview:**

```
  ┌─────────────────┐
  │ 1. Problem      │
  │    Definition   │
  └────────┬────────┘
           ▼
  ┌─────────────────┐
  │ 2. Data         │
  │    Collection   │
  └────────┬────────┘
           ▼
  ┌─────────────────┐
  │ 3. Data         │
  │    Preparation  │
  └────────┬────────┘
           ▼
  ┌─────────────────┐
  │ 4. Exploratory  │
  │    Analysis     │
  └────────┬────────┘
           ▼
  ┌─────────────────┐
  │ 5. Model        │
  │    Building     │
  └────────┬────────┘
           ▼
  ┌─────────────────┐
  │ 6. Evaluation   │
  └────────┬────────┘
           ▼
  ┌─────────────────┐
  │ 7. Deployment   │
  │  & Storytelling │
  └─────────────────┘
```

---

### **5.3 Each Step Explained**

#### **Step 1: Problem Definition**
- Clearly define the **business question** to answer.
- Example: "Which customers are most likely to churn next month?"
- Bad-defined problems = wasted effort.

#### **Step 2: Data Collection**
- Identify and gather data from relevant sources.
- Sources: databases, APIs, web scraping, sensors, surveys.
- Key question: Is there **enough data** to answer the question?

#### **Step 3: Data Preparation (Wrangling / Cleaning)**
- Real data is messy. This is the **most time-consuming step** (60–80% of effort).
- Tasks:
  - Handle missing values.
  - Remove duplicates.
  - Fix format inconsistencies.
  - Encode categorical variables.
  - Normalize / scale features.

#### **Step 4: Exploratory Data Analysis (EDA)**
- Understand the data **before** building models.
- Tasks:
  - Summary statistics (mean, median, std).
  - Data visualization (histograms, scatter plots, heatmaps).
  - Find correlations and outliers.
  - Choose appropriate ML techniques.

#### **Step 5: Model Building**
- Apply ML or statistical algorithms to the prepared data.
- Split data: training set + test set.
- Try multiple models, tune hyperparameters.
- Example: Decision tree, regression, clustering.

#### **Step 6: Evaluation**
- Measure how well the model performs on unseen data.
- Metrics: Accuracy, F1-score, RMSE, AUC (covered in ML Unit 4).
- If performance is poor → go back to Step 3 or 5.

#### **Step 7: Deployment and Communication**
- Deploy the model in a production system (web API, dashboard, app).
- Communicate findings to stakeholders using **visualizations and storytelling**.
- Monitor model over time for degradation.

---

## **Section 6: Foundations for Big Data Systems and Programming**

### **6.1 What Makes a Big Data System?**

A Big Data system must handle the 6 V's. The **foundation** consists of:

```
┌─────────────────────────────────────┐
│        Big Data System Stack        │
├─────────────────────────────────────┤
│  Analytics / ML Layer               │  (Spark MLlib, Hive, Pig)
├─────────────────────────────────────┤
│  Processing Layer                   │  (MapReduce, Spark, Flink)
├─────────────────────────────────────┤
│  Storage Layer                      │  (HDFS, S3, HBase, Cassandra)
├─────────────────────────────────────┤
│  Resource Management                │  (YARN, Kubernetes)
├─────────────────────────────────────┤
│  Hardware Layer                     │  (Commodity servers, cloud)
└─────────────────────────────────────┘
```

---

### **6.2 Key Concepts**

#### **Cluster Computing**

A **cluster** is a group of connected computers (nodes) that work together as one system.

```
       ┌──────────────────────┐
       │     Master Node      │  ← manages and coordinates
       └──────────┬───────────┘
        ┌─────────┼─────────┐
        ▼         ▼         ▼
   ┌────────┐ ┌────────┐ ┌────────┐
   │Worker 1│ │Worker 2│ │Worker 3│  ← do the actual work
   └────────┘ └────────┘ └────────┘
```

- Each worker stores and processes a portion of the data.
- Master node coordinates task assignment.

---

#### **MapReduce Programming Model**

**MapReduce** is the fundamental programming model for processing Big Data in parallel across a cluster.

**Two phases:**

```
MAP Phase:
  Input Data → Split into chunks → Each chunk processed in parallel
  → Produces key-value pairs (intermediate output)

REDUCE Phase:
  Group all values by key → Aggregate / combine values
  → Final output
```

**Example — Word Count:**

```
Input: "cat dog cat bird dog cat"

MAP output (key-value pairs):
  (cat,1) (dog,1) (cat,1) (bird,1) (dog,1) (cat,1)

REDUCE (group by key, sum values):
  cat  → 3
  dog  → 2
  bird → 1

Final Output:
  cat:3, dog:2, bird:1
```

---

#### **Data Replication**

- Each piece of data is stored on **multiple nodes** (default: 3 copies in HDFS).
- If one node fails, data is still available from another.
- Provides **fault tolerance**.

```
  Data Block A
  ┌──────────────────────────────────────┐
  │  Copy 1 → Node 1                    │
  │  Copy 2 → Node 3    (different rack)│
  │  Copy 3 → Node 5                    │
  └──────────────────────────────────────┘
```

---

### **6.3 Big Data Programming Tools**

| Tool | Type | Purpose |
|------|------|---------|
| **Hadoop** | Framework | Distributed storage + MapReduce processing |
| **Apache Spark** | Processing engine | Fast in-memory distributed processing |
| **Apache Kafka** | Messaging | Real-time data streaming |
| **Apache Hive** | Query tool | SQL-like queries on HDFS data |
| **Apache HBase** | NoSQL DB | Real-time read/write on HDFS |
| **Apache Pig** | Scripting | Data transformation using Pig Latin |
| **Apache Flink** | Stream processing | Low-latency stream analytics |
| **YARN** | Resource manager | Cluster resource allocation |

---

## **Section 7: Distributed File Systems**

### **7.1 What is a Distributed File System?**

**Definition:**

A **Distributed File System (DFS)** is a file system that stores data across **multiple machines** in a network, but makes it look like a **single unified file system** to the user.

**Why needed?**
- A single disk cannot hold petabytes of data.
- A distributed file system spreads data across hundreds or thousands of nodes.
- Provides **scalability**, **fault tolerance**, and **high throughput**.

---

### **7.2 HDFS — Hadoop Distributed File System**

**HDFS** is the most widely used distributed file system for Big Data, and the storage backbone of the Hadoop ecosystem.

**Key Design Goals:**
1. Store very large files (GB to TB per file).
2. Run on commodity hardware (cheap, standard servers).
3. Detect and recover from hardware failures automatically.
4. Optimized for batch processing (high throughput over low latency).

---

### **7.3 HDFS Architecture**

```
          ┌─────────────────────────────┐
          │        NameNode             │  ← Master
          │  (metadata: file locations) │
          └─────────────┬───────────────┘
                        │
          ┌─────────────┼──────────────┐
          ▼             ▼              ▼
    ┌──────────┐  ┌──────────┐  ┌──────────┐
    │DataNode 1│  │DataNode 2│  │DataNode 3│  ← Workers
    │ Block A  │  │ Block B  │  │ Block A  │
    │ Block C  │  │ Block A  │  │ Block B  │
    └──────────┘  └──────────┘  └──────────┘
```

**Two Types of Nodes:**

| Node | Role |
|------|------|
| **NameNode** (Master) | Stores metadata — which blocks are in which DataNode. Does NOT store actual data. |
| **DataNode** (Worker) | Stores actual data blocks. Reports heartbeat to NameNode. |

---

### **7.4 How HDFS Works**

#### **Writing a File:**

```
1. Client contacts NameNode → "I want to write file.txt"
2. NameNode assigns block locations across DataNodes.
3. Client writes data block-by-block to DataNodes.
4. Each block is replicated to 3 DataNodes (default replication factor = 3).
5. DataNodes send confirmation.
6. NameNode updates metadata.
```

#### **Reading a File:**

```
1. Client contacts NameNode → "I want to read file.txt"
2. NameNode returns list of DataNodes holding each block.
3. Client reads blocks directly from DataNodes (parallel).
4. Blocks are assembled into the complete file.
```

---

### **7.5 HDFS Key Concepts**

#### **Block Size**

- HDFS divides files into large fixed-size **blocks** (default: **128 MB** in modern Hadoop).
- A 1 GB file → 8 blocks of 128 MB each.
- Large blocks reduce NameNode metadata overhead.

```
  file.txt (512 MB)
  ┌──────┬──────┬──────┬──────┐
  │Block1│Block2│Block3│Block4│  each = 128 MB
  └──────┴──────┴──────┴──────┘
```

#### **Replication**

- Each block is copied to **3 DataNodes** (default replication factor = 3).
- Strategy: 1 copy on local rack, 2 copies on different racks.
- Protects against both **node failure** and **rack failure**.

#### **Fault Tolerance**

- DataNodes send **heartbeat signals** every 3 seconds to NameNode.
- If NameNode doesn't hear from a DataNode → assumes it's dead.
- NameNode automatically **re-replicates** the lost blocks from remaining copies.

---

### **7.6 HDFS Features and Limitations**

**Features:**

✅ Handles files of size GB to PB.  
✅ Runs on cheap commodity hardware.  
✅ Automatic fault tolerance through replication.  
✅ High throughput for batch reads.  
✅ Scales horizontally — just add more DataNodes.

**Limitations:**

❌ High latency — not suited for real-time (online) applications.  
❌ Not good for small files (wastes NameNode metadata space).  
❌ Does not support random writes — files are write-once, read-many.  
❌ NameNode is a **single point of failure** (addressed by HA NameNode in Hadoop 2+).

---

### **7.7 Other Distributed File Systems**

| DFS | By | Key Features |
|-----|----|--------------|
| **HDFS** | Apache/Hadoop | Open source, MapReduce native |
| **Amazon S3** | AWS | Object storage, highly available |
| **Google GFS** | Google | Inspired HDFS design |
| **Azure Blob** | Microsoft | Cloud object storage |
| **Ceph** | Open source | Block + object + file storage |
| **GlusterFS** | Red Hat | Network-attached storage |

---

## **Quick Revision Points**

### **Big Data — Why & Where:**
- Data explosion from social media, IoT, digitization, e-commerce.
- Sources: social, sensor, transactional, web, scientific.

### **6 V's:**

| V | Name | Key Point |
|---|------|-----------|
| V1 | Volume | Petabytes of data |
| V2 | Velocity | Real-time streaming |
| V3 | Variety | Structured / semi / unstructured |
| V4 | Veracity | Data quality and accuracy |
| V5 | Value | Business insight extraction |
| V6 | Variability | Context-dependent meaning |

### **Data Science Process (7 Steps):**
1. Problem Definition → 2. Data Collection → 3. Data Preparation → 4. EDA → 5. Model Building → 6. Evaluation → 7. Deployment

### **Scaling:**
- Vertical = bigger machine (limited).
- Horizontal = more machines (Big Data approach).

### **HDFS:**
- NameNode = master (metadata only).
- DataNode = worker (stores blocks).
- Block size = 128 MB (default).
- Replication factor = 3.
- Fault tolerant via heartbeat + re-replication.

### **MapReduce:**
```
Map → (key, value) pairs → Shuffle & Sort → Reduce → Final output
```

---

## **Expected Exam Questions**

> PYQs will be added after analysis — check back soon.

---

_These notes were compiled by [Deepak Modi](https://deepakmodi.dev)_  
_Last updated: May 2026_
