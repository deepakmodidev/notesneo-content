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

### **High Priority Topics** (15 marks questions)

1. **6 V's of Big Data (Characteristics)** — (2024: 15 marks, 2023: 15 marks, 2022: 15 marks)
2. **HDFS — NameNode, DataNode, Blocks, Operations & Commands** — (2023: 15 marks, 2022: 15 marks) → Section 7 + 7.8
3. **Big Data Definition + Characteristics + Applications + Challenges** — (2024: 15 marks, 2023: 15 marks, 2022: 15 marks)
4. **Data Science Process (steps + real-world example)** — (2024: 15 marks) → Section 5 + 5.4
5. **Big Data Platform — Main Features (5 characteristics)** — (2022: 15 marks) → Section 9
6. **Foundation for Big Data System** — (2023: 15 marks) → Section 6
7. **Big Data Analytics Techniques (A/B testing, Data Mining, ML, NLP, Statistics, Data Fusion)** — (2022: 15 marks) → Section 8
8. **Types of Data — Measurement Scales (Nominal / Ordinal / Interval / Ratio)** — (2022: 15 marks) → Section 10
9. **Challenges in Big Data** — (2022: 15 marks) → Section 2.2

### **Medium Priority Topics** (Short answers)

1. **Six V in Big Data** — 2024 (2.5), 2022 (2.5)
2. **Big Data definition** — 2022 (2.5)
3. **YARN — Components & Features** — 2022 (2.5) → Section 6.4
4. **Data Sciences** — 2023 (2.5)
5. **DFS (Distributed File System)** — 2023 (2.5)
6. **5 challenges of Big Data** — 2024 (2.5)
7. **Hadoop (short note — HDFS + MapReduce + YARN)** — 2024 (7.5 marks) → Section 11

---

## **Section 1: Big Data — Why and Where**

### **1.1 What is Big Data?**

> PYQ: Explain Big Data. (2022, 2.5 marks)  
> PYQ: What is Big Data? Explain various characteristics, challenges and applications of Big Data. (2023, 15 marks)  
> PYQ: Define different techniques in Big Data analytics. (2022, 15 marks)

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

> PYQ: Discuss the following in detail: (i) Challenges in big data (ii) Types of Data. (2022, 15 marks)  
> PYQ: Enlist 5 challenges associated with managing and analyzing large volumes of data. (2024, 2.5 marks)  
> PYQ: Describe any five real life applications of Big Data. (2022, 15 marks)  
> PYQ: Write short note on real life applications of Big Data. (2023, 15 marks)

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

> PYQ: Six V in big data. (2022, 2.5 marks)  
> PYQ: Briefly elaborate the six V of big data. (2024, 2.5 marks)  
> PYQ: Explain six V's of Big Data in detail. (2023, 15 marks)  
> PYQ: Explain the characteristics of Big Data and discuss how they contribute to the challenges in managing large volumes of data. (2024, 15 marks)

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

> PYQ: Write short note on Data Sciences. (2023, 2.5 marks)  
> PYQ: Describe the steps involved in the Data Science process. How does each step contribute to extracting value from Big Data? (2024, 8 marks)  
> PYQ: Illustrate with a real-world scenario for steps involving Data Science process. (2024, 7 marks)

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

### **5.4 Real-World Scenario — Data Science Process Across Industries**

> PYQ: Illustrate with a real-world scenario for steps involving Data Science process. (2024, 7 marks)

The same 7-step process applies across industries — only the **domain context** changes. Below is a parallel walk-through for **Healthcare**, **Finance**, and **Retail**.

| Step | Healthcare | Finance | Retail |
|------|-----------|---------|--------|
| **1. Problem Definition** | Predict patient readmissions within 30 days | Detect fraudulent transactions / credit defaults | Increase sales by understanding customer patterns |
| **2. Data Collection** | Electronic Health Records (EHR), lab results, medical images (X-Ray, MRI) | Bank transaction logs, credit history, account activity | Customer purchase history, clickstream, loyalty card data |
| **3. Data Cleaning** | Clean patient records — fill missing vitals, standardize ICD codes | Standardize transaction formats across branches; remove duplicates | Deduplicate customer profiles, merge across channels |
| **4. EDA** | Identify disease outbreak patterns, age-disease correlations | Anomaly detection in spending behavior, peak fraud windows | Discover customer preferences, basket affinities |
| **5. Modeling** | Classifier to flag high-risk readmission patients | ML model for real-time fraud detection (Random Forest, XGBoost) | Churn prediction & recommendation engine |
| **6. Evaluation** | Validate diagnosis model accuracy (AUC, sensitivity) on test patients | Backtest fraud-detection precision/recall on past cases | Cross-validate churn predictions vs actual customer drop |
| **7. Deployment** | Embed model into hospital admission dashboard for doctors | Plug fraud-scoring API into live transaction stream | Deploy churn model into CRM; trigger retention offers |

**Key Insight:** The process is **domain-agnostic** — the value comes from translating domain expertise into the right problem definition and feature engineering at Steps 1–3.

---

## **Section 6: Foundations for Big Data Systems and Programming**

> PYQ: Write short note on foundation for Big Data system. (2023, 15 marks)  
> PYQ: What is Big Data Platform? Describe the main features of a big data platform in detail. (2022, 15 marks)  
> PYQ: Explain YARN. (2022, 2.5 marks)  
> PYQ: Write short note on Hadoop. (2024, 7.5 marks)

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

### **6.4 YARN — Yet Another Resource Negotiator**

> PYQ: Explain YARN. (2022, 2.5 marks)

**Definition:**

**YARN (Yet Another Resource Negotiator)** is a **cluster resource manager** in Hadoop. It was created by **separating the processing engine from the resource-management function** of classic MapReduce, and was introduced in **Hadoop 2.0** to remove the **Job Tracker bottleneck** of Hadoop 1.x.

In short: YARN lets multiple data-processing engines (MapReduce, Spark, Flink, Tez) share the same Hadoop cluster.

**YARN Architecture — 4 Components:**

```
   ┌──────────┐     submits job      ┌────────────────────┐
   │  Client  │ ───────────────────► │  Resource Manager  │
   └──────────┘                      │  (Cluster Master)  │
                                     └─────────┬──────────┘
                              allocates        │
                              containers       ▼
                              ┌────────────────────────────┐
                              │   Node Manager (per node)  │
                              │   ┌──────────────────────┐ │
                              │   │ MR App Master + Tasks│ │
                              │   └──────────────────────┘ │
                              └────────────────────────────┘
```

| Component | Role |
|-----------|------|
| **Client** | Submits MapReduce (or Spark/other) jobs to the cluster. |
| **Resource Manager (RM)** | Central master — manages and allocates resources (CPU, memory) across the entire cluster. |
| **Node Manager (NM)** | Runs on each worker machine — launches, monitors, and reports the status of containers. |
| **MapReduce Application Master (AM)** | One per job — negotiates resources with RM and supervises the tasks running the MapReduce job. |

**Features of YARN:**

- **Resource Management** — central allocation of CPU and memory.
- **Scalability** — supports thousands of nodes; removes the old Job Tracker bottleneck.
- **Cluster Utilization** — multiple frameworks (MR, Spark, Tez) share resources.
- **Flexibility** — not tied to MapReduce only; any distributed app can plug in.

---

## **Section 7: Distributed File Systems**

> PYQ: Write short note on DFS (Distributed File System). (2023, 2.5 marks)  
> PYQ: Define HDFS. Describe NameNode, DataNode and Block. Explain HDFS operations in detail. (2022, 15 marks)  
> PYQ: What is HDFS? Explain its components. (2023, 15 marks)

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

### **7.8 HDFS Operations & Commands**

> PYQ: Define HDFS. Describe NameNode, DataNode and Block. Explain HDFS operations in detail. (2022, 15 marks)

HDFS exposes a **shell-like command-line interface** (`hadoop fs` / `hdfs dfs`) for users to interact with the file system. The four main operations every student must know are: **Starting HDFS, Listing files, Inserting data, Retrieving data, and Shutting down**.

#### **1. Starting HDFS**

Before using HDFS, the file system must be formatted (only the first time) and the daemons (NameNode + DataNodes) must be started.

```bash
# First-time only — format the NameNode
$ hadoop namenode -format

# Start all HDFS daemons (NameNode, DataNodes, Secondary NN)
$ start-dfs.sh
```

#### **2. Listing Files in HDFS**

Once HDFS is running, use the `-ls` command to list the contents of a directory.

```bash
$ $HADOOP_HOME/bin/hadoop fs -ls <args>
```

Example:
```bash
$ hadoop fs -ls /user/input
```

#### **3. Inserting Data into HDFS**

Loading a local file into HDFS is a **3-step process**:

```bash
# Step 1 — Create an input directory in HDFS
$ hadoop fs -mkdir /user/input

# Step 2 — Transfer the local file to HDFS
$ hadoop fs -put /home/file.txt /user/input

# Step 3 — Verify that the file is uploaded
$ hadoop fs -ls /user/input
```

#### **4. Retrieving Data from HDFS**

Data can be **viewed in place** or **copied back** to the local file system.

```bash
# View file contents directly from HDFS
$ hadoop fs -cat /user/output/outfile

# Copy a file/directory from HDFS to local file system
$ hadoop fs -get /user/output/ /home/hadoop_tp/
```

#### **5. Shutting Down HDFS**

```bash
$ stop-dfs.sh
```

This stops all HDFS daemons cleanly.

**Operation Summary:**

| Operation | Key Command |
|-----------|-------------|
| Start HDFS | `start-dfs.sh` |
| List files | `hadoop fs -ls` |
| Make directory | `hadoop fs -mkdir` |
| Upload file | `hadoop fs -put` |
| View file | `hadoop fs -cat` |
| Download file | `hadoop fs -get` |
| Stop HDFS | `stop-dfs.sh` |

---

## **Section 8: Big Data Analytics Techniques**

> PYQ: Define the different techniques in Big Data analytics. (2022, 15 marks)

Big Data analytics is **not a single method** — it is a toolbox of techniques drawn from statistics, machine learning, AI, and database research. The six most important techniques are described below.

### **8.1 Six Core Techniques**

#### **1. A/B Testing**

- **Definition:** A controlled experiment comparing a **control group** (existing version) against one or more **test groups** (new variants) to determine which one improves a defined objective (e.g., click-through rate, conversions).
- **Example:** A retail website shows version A of a product page to 50% of visitors and version B to the other 50%. The variant with the higher purchase rate wins.

#### **2. Data Fusion and Data Integration**

- **Definition:** The process of **combining and analyzing data from multiple sources** so that insights are richer than any single source could deliver.
- **Example:** Combining smartphone GPS data, weather feeds, and social-media check-ins to map real-time traffic congestion.

#### **3. Data Mining**

- **Definition:** Extracting **hidden patterns and useful information** from large datasets using a combination of **statistics, machine learning, and database management**.
- **Example:** **Customer segmentation** — clustering supermarket shoppers into groups (budget, premium, bulk-buyers) based on purchase histories.

#### **4. Machine Learning**

- **Definition:** A family of algorithms that **make assumptions / learn patterns from data** and use those patterns to make predictions on new, unseen data. ML provides predictions that would be **impossible (or too slow) for human analysts**.
- **Example:** Netflix recommending movies, Gmail filtering spam, banks scoring credit-card fraud risk.

#### **5. Natural Language Processing (NLP)**

- **Definition:** A **sub-speciality of computer science, AI, and linguistics** that analyzes, understands, and generates **human language** (text and speech).
- **Example:** Sentiment analysis of tweets, chatbots, Google Translate, voice assistants (Alexa, Siri).

#### **6. Statistics**

- **Definition:** The classical science of **collecting, organizing, analyzing, interpreting, and presenting data** from surveys and experiments.
- **Example:** Computing the mean customer lifetime value, hypothesis testing for marketing campaigns, regression analysis.

### **8.2 Other Techniques (briefly)**

- **Spatial Analysis** — analyzing geographic / location-based data (GIS, maps).
- **Predictive Modelling** — building statistical / ML models to forecast future outcomes.
- **Association Rule Learning** — finding "if-then" relationships ("people who buy bread also buy butter").
- **Network Analysis** — studying nodes and edges in graphs (social networks, fraud rings).

### **8.3 Summary Table**

| # | Technique | Core Idea |
|---|-----------|-----------|
| 1 | A/B Testing | Control vs Test comparison |
| 2 | Data Fusion / Integration | Combine multiple sources |
| 3 | Data Mining | Extract patterns from large data |
| 4 | Machine Learning | Algorithms that learn from data |
| 5 | NLP | Understand human language |
| 6 | Statistics | Collect & interpret data |

---

## **Section 9: Big Data Platform — Main Features**

> PYQ: What is Big Data Platform? Describe the main features of a big data platform in detail. (2022, 15 marks)

### **9.1 What is a Big Data Platform?**

A **Big Data Platform** is an **integrated computing solution** that combines **software, tools, and hardware** to manage the full Big Data lifecycle — ingestion, storage, processing, analysis, and visualization — at petabyte scale.

Examples: Cloudera CDP, Hortonworks HDP, AWS EMR, Google BigQuery, Azure HDInsight.

### **9.2 Five Main Features (Characteristics)**

```
   ┌─────────────────────────────────────────┐
   │       Big Data Platform — 5 Features    │
   ├─────────────────────────────────────────┤
   │  1. Comprehensive                       │
   │  2. Integrated                          │
   │  3. Scalability                         │
   │  4. Extensible                          │
   │  5. Minimum Maintenance                 │
   └─────────────────────────────────────────┘
```

#### **1. Comprehensive**

- Handles **all the Big Data challenges** — Volume, Variety, and Velocity — within a single unified stack.
- Supports structured, semi-structured, and unstructured data, plus batch and stream pipelines.

#### **2. Integrated**

- Works **alongside existing information architecture** — traditional **databases, data warehouses, and BI tools** (Teradata, Tableau, Power BI, Informatica).
- Avoids data silos by exposing Big Data results back to enterprise reporting layers.

#### **3. Scalability**

- Designed to **scale from gigabytes to petabytes without redesign** — this is the role Hadoop plays.
- Storage must be **cost-efficient** (commodity disks, object storage) so scaling does not break budgets.

#### **4. Extensible**

- Easy to **accommodate newer technologies** as the company expands — new processing engines (Spark, Flink), new sources, new ML libraries.
- Naturally **integrates IoT and sensor data** into the same platform.

#### **5. Minimum Maintenance**

- Fault-tolerant design — failure of an individual node does not stop the platform.
- Individual hardware can be **upgraded or replaced without downtime**.
- Self-healing replication and automatic re-balancing.

### **9.3 Summary Table**

| Feature | Why it matters |
|---------|----------------|
| Comprehensive | Solves V-V-V challenges in one stack |
| Integrated | Plays well with existing DW / BI |
| Scalability | Petabyte growth without redesign |
| Extensible | Accepts new tech (IoT, ML, streaming) |
| Minimum Maintenance | Fault tolerant, hot-swappable hardware |

---

## **Section 10: Types of Data (Measurement Scales)**

> PYQ: Discuss the following in detail: (i) Challenges in big data (ii) Types of Data. (2022, 15 marks)

### **10.1 How Data is Classified**

Data is classified into **measurement scales** based on **three characteristics**:

| Characteristic | Question it answers |
|----------------|---------------------|
| **Order** | Does the order of observations matter? |
| **Distance** | Are the distances (intervals) between observations meaningful? |
| **True Zero** | Is there a real, absolute zero point? |

Based on these three properties, data falls into **four measurement scales**: **Nominal, Ordinal, Interval, and Ratio**.

```
   Nominal  →  Ordinal  →  Interval  →  Ratio
   (labels)   (rank)      (+ equal     (+ true zero
                            spacing)      → ratios)
```

### **10.2 The Four Measurement Scales**

#### **1. Nominal Scale**

- **Definition:** Categories or labels with **no inherent order** between them.
- **Examples:** Gender (Male/Female/Other), ethnicity, product type, blood group.
- **Properties:**
  - **Order:** Doesn't matter.
  - **Distance:** Not held (cannot subtract one category from another).
  - **True Zero:** None.
- **Allowed operations:** Counting, mode, chi-square tests.

#### **2. Ordinal Scale**

- **Definition:** Categories with a **natural order or ranking**, but the **intervals between ranks are unequal / unknown**.
- **Examples:** Customer ratings (Poor / Fair / Good / Excellent), survey responses (Strongly Disagree → Strongly Agree), military ranks, education level.
- **Properties:**
  - **Order:** Matters.
  - **Distance:** Not held (the gap between "Good" and "Excellent" is not equal to "Poor" to "Fair").
  - **True Zero:** None.
- **Allowed operations:** Median, percentiles, rank correlation.

#### **3. Interval Scale**

- **Definition:** Numerical data with **consistent (equal) intervals** between values, but **no true zero point**.
- **Examples:** Temperature in **Celsius** or **Fahrenheit**, calendar years, IQ scores.
- **Properties:**
  - **Order:** Matters.
  - **Distance:** Held — the gap between 20°C and 30°C equals the gap between 30°C and 40°C.
  - **True Zero:** None — 0°C does **not** mean "no temperature" (it's rescalable; 0°C ≠ 0°F).
- **Allowed operations:** Addition, subtraction, mean, standard deviation. **Ratios are NOT meaningful** (40°C is not "twice as hot" as 20°C).

#### **4. Ratio Scale**

- **Definition:** Numerical data with **equal intervals AND a true zero point**, making **ratios meaningful**.
- **Examples:** Weight, height, age, income, distance, time elapsed, temperature in **Kelvin**.
- **Properties:**
  - **Order:** Matters.
  - **Distance:** Held.
  - **True Zero:** Present — 0 kg means **no weight**; ₹0 means no income.
- **Allowed operations:** All arithmetic — including ratios ("60 kg is twice 30 kg").

### **10.3 Summary Comparison Table**

| Scale | Order | Distance | True Zero | Example | Key Stat |
|-------|:-----:|:--------:|:---------:|---------|----------|
| **Nominal** | ✘ | ✘ | ✘ | Gender, blood group | Mode, count |
| **Ordinal** | ✔ | ✘ | ✘ | Ratings, ranks | Median |
| **Interval** | ✔ | ✔ | ✘ | Celsius, IQ | Mean, SD |
| **Ratio** | ✔ | ✔ | ✔ | Weight, income | All operations |

**Rule of thumb:** Each scale **includes** the properties of the previous one — Ratio is the most powerful, Nominal the most limited.

---

## **Section 11: Hadoop — Detailed Note**

> PYQ: Write short note on Hadoop. (2024, 7.5 marks)

### **11.1 Definition**

**Hadoop** is an **open-source Java framework** developed by the Apache Software Foundation for **storing massive amounts of data** and **processing it in parallel** across clusters of commodity hardware. It is the de-facto standard for Big Data infrastructure.

Designed to be:
- **Distributed** — runs on hundreds/thousands of nodes.
- **Fault-tolerant** — survives hardware failures.
- **Scalable** — add more nodes to handle more data.
- **Cost-effective** — uses cheap commodity servers.

### **11.2 Three Core Components**

```
        ┌──────────────────────────────────┐
        │             HADOOP               │
        ├───────────┬──────────┬───────────┤
        │   HDFS    │ MapReduce│    YARN   │
        │ (Storage) │(Processing)│(Resource)│
        └───────────┴──────────┴───────────┘
```

#### **1. HDFS (Hadoop Distributed File System) — Storage**

- **Distributed Storage** — splits files into blocks and stores them across many DataNodes.
- **Scalability** — add DataNodes to grow capacity linearly.
- **Data Replication** — each block is replicated (default = **3 copies**) for fault tolerance.
- **Data Compression** — supports codecs (Snappy, Gzip, LZO) to reduce storage and I/O.

#### **2. MapReduce — Processing**

A parallel programming model that processes data in three phases:

```
  Map  →  Shuffle / Sort  →  Reduce
  ───────────────────────────────────
  Map:     Split data and emit (key, value) pairs
  Shuffle: Group all values by key across nodes
  Reduce:  Aggregate / combine values for final output
```

#### **3. YARN (Yet Another Resource Negotiator) — Resource Management**

- **Resource Management** — central CPU and memory allocation across the cluster.
- **Scalability** — supports thousands of nodes (replaces Hadoop-1 Job Tracker bottleneck).
- **Cluster Utilization** — multiple engines (MR, Spark, Tez, Flink) share the same cluster.
- **Flexibility** — supports varied workloads, not just MapReduce.

### **11.3 Hadoop in One Picture**

```
  ┌──────────────────────────────────────────────────┐
  │                   HADOOP CLUSTER                 │
  │                                                  │
  │   Storage  ─►  HDFS  (blocks + 3x replication)   │
  │   Compute  ─►  MapReduce / Spark / Tez           │
  │   Manage   ─►  YARN (RM + NM + AM)               │
  └──────────────────────────────────────────────────┘
```

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

### **YARN (4 components):**
- Client → Resource Manager → Node Manager → MR Application Master.
- Features: Resource Management, Scalability, Cluster Utilization, Flexibility.

### **HDFS Operations (commands):**
- Start: `hadoop namenode -format` → `start-dfs.sh`
- List: `hadoop fs -ls`
- Insert: `-mkdir` → `-put /home/file.txt /user/input` → `-ls`
- Retrieve: `-cat /user/output/outfile` / `-get /user/output/ /home/hadoop_tp/`
- Stop: `stop-dfs.sh`

### **Big Data Analytics Techniques (6):**
A/B Testing · Data Fusion / Integration · Data Mining · Machine Learning · NLP · Statistics.
*Other:* Spatial analysis, Predictive modelling, Association rule learning, Network analysis.

### **Big Data Platform — 5 Features:**
1. Comprehensive · 2. Integrated · 3. Scalability · 4. Extensible · 5. Minimum Maintenance.

### **Types of Data — 4 Measurement Scales:**

| Scale | Order | Distance | True Zero | Example |
|-------|:-----:|:--------:|:---------:|---------|
| Nominal | ✘ | ✘ | ✘ | Gender |
| Ordinal | ✔ | ✘ | ✘ | Ratings |
| Interval | ✔ | ✔ | ✘ | Celsius |
| Ratio | ✔ | ✔ | ✔ | Weight |

### **Hadoop (3 components):**
- **HDFS** — Distributed Storage + Scalability + 3-copy Replication + Compression.
- **MapReduce** — Map → Shuffle/Sort → Reduce.
- **YARN** — Resource Management + Scalability + Cluster Utilization + Flexibility.

### **Data Science Process — Domain Examples:**
Healthcare (readmission) · Finance (fraud) · Retail (churn) — same 7 steps, different domain context.

---

## **Expected Exam Questions**

### **15-Mark Questions:**

1. What is Big Data? Explain various characteristics, challenges and applications of Big Data. *(2023)*
2. Explain the characteristics of Big Data and discuss how they contribute to the challenges in managing large volumes of data. *(2024)*
3. Explain six V's of Big Data in detail. *(2023)*
4. Define HDFS. Describe NameNode, DataNode and Block. **Explain HDFS operations (start, list, insert, retrieve, stop) with commands in detail.** *(2022)*
5. What is HDFS? Explain its components. *(2023)*
6. **What is Big Data Platform? Describe the main features (Comprehensive, Integrated, Scalability, Extensible, Minimum Maintenance) of a big data platform in detail.** *(2022)*
7. Write short note on foundation for Big Data system. *(2023)*
8. **Define the different techniques in Big Data analytics (A/B Testing, Data Fusion, Data Mining, ML, NLP, Statistics).** *(2022)*
9. **Discuss the following in detail: (i) Challenges in big data (ii) Types of Data (Nominal, Ordinal, Interval, Ratio measurement scales).** *(2022)*
10. Describe any five real life applications of Big Data. *(2022)*
11. Write short note on real life applications of Big Data. *(2023)*

### **Mixed (8 + 7 marks):**

1. Describe the steps involved in the Data Science process. How does each step contribute to extracting value from Big Data? *(2024, 8 marks)*
2. **Illustrate with a real-world scenario (Healthcare / Finance / Retail) for steps involving Data Science process.** *(2024, 7 marks)*

### **Short Answer Questions (2.5 marks):**

1. Explain Big Data. *(2022)*
2. **Explain YARN — its 4 components (Client, Resource Manager, Node Manager, MR Application Master) and features.** *(2022)*
3. Six V in Big Data. *(2022)*
4. Briefly elaborate the six V of Big Data. *(2024)*
5. Write short note on Data Sciences. *(2023)*
6. Write short note on DFS. *(2023)*
7. Enlist 5 challenges associated with managing and analyzing large volumes of data. *(2024)*

### **Short Note (≈ 7.5 marks):**

1. **Write short note on Hadoop — covering HDFS (Storage + Replication + Compression), MapReduce (Map → Shuffle → Reduce), and YARN (Resource Manager).** *(2024)*

---

_These notes were compiled by [Deepak Modi](https://deepakmodi.dev)_  
_Last updated: May 2026_
