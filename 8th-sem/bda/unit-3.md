---
title: "Unit 3: Big Data Modeling and Management"
description: "Data Storage, Quality, Operations, Ingestion, Scalability, Security, Traditional DBMS vs Big Data Systems, Data Models — Structure, Operations, Constraints, Types."
author: "Deepak Modi"
date: "2026-05-10"
pdfUrl: ""
---

## Syllabus:

**Introduction to Big Data Modeling and Management:** Data Storage, Data Quality, Data Operations, Data Ingestion, Scalability and Security, Traditional DBMS and Big Data Management Systems, Real Life Applications, Data Model: Structure, Operations, Constraints, Types of Big Data Model.

---

## 🎯 PYQ Analysis for Unit 3

### **High Priority Topics** (15 marks questions)

1. **Data Models — Types (Relational, Key-Value, Document, Column, Graph)** — (2023: 15 marks) — *Section 8*
2. **Scalability — concept, vertical vs horizontal, challenges, traditional DBMS vs Big Data Mgmt (unified)** — (2024: 15 marks) — *Sections 5.1 + 5.3*
3. **Data Quality — importance (5 reasons), challenges at scale (3 V's), solutions (6 approaches)** — (2024: 15 marks) — *Sections 2.1–2.7*
4. **Big Data Management Techniques (8 techniques — governance, quality, mining, security, analytics, ML, predictive, centralized mgmt)** — (2023: 15 marks) — *Section 6.4*
5. **Traditional Data vs Big Data — Comparison** — (2022: 15 marks) — *Section 6.2*
6. **Real Life Applications of Big Data** — (2023: 15 marks, 2022: 15 marks) — *Section 7*

### **Medium Priority Topics** (Short answers)

1. **Data Ingestion** — 2023 (2.5 marks)
2. **Types of Data Models and their applications** — 2024 (2.5 marks)

---

## **Section 1: Data Storage in Big Data**

### **1.1 What is Data Storage?**

**Definition:**

**Data Storage** in the context of Big Data refers to the systems and technologies used to **store massive volumes of diverse data** reliably, efficiently, and in a way that supports large-scale processing and retrieval.

---

### **1.2 Types of Data Storage**

#### **1. File-Based Storage**

- Data stored as raw files on a distributed file system.
- No schema enforced at write time.
- Example: **HDFS**, **Amazon S3**, **Azure Data Lake Storage**.

```
  /data/
    ├── logs/
    │     ├── 2026-01-01.log
    │     └── 2026-01-02.log
    ├── images/
    └── transactions.csv
```

**Best for:** Raw data ingestion, data lakes, batch processing.

---

#### **2. Relational Storage**

- Data stored in tables with fixed schema.
- Uses SQL for querying.
- Example: **MySQL**, **PostgreSQL**, **Amazon Redshift** (analytical RDBMS).

**Best for:** Structured data, OLTP, traditional reporting.

---

#### **3. NoSQL Storage**

- Flexible schema for semi-structured and unstructured data.
- Types: Key-Value, Document, Column-Family, Graph.
- Example: **MongoDB**, **Cassandra**, **HBase**, **Redis**.

**Best for:** Real-time applications, flexible schema data, high write throughput.

---

#### **4. In-Memory Storage**

- Data stored in **RAM** instead of disk.
- Extremely fast access (microseconds vs milliseconds for disk).
- Example: **Redis**, **Memcached**, **Apache Spark (RDD caching)**.

**Best for:** Caching, real-time analytics, iterative ML algorithms.

---

#### **5. Object Storage**

- Data stored as **objects** (file + metadata + unique ID).
- Highly scalable, no hierarchy (flat namespace).
- Example: **Amazon S3**, **Google Cloud Storage**, **Azure Blob**.

**Best for:** Backups, media files, data lake foundation, archival.

---

### **1.3 Storage Comparison**

| Type | Schema | Scale | Speed | Best For |
|------|--------|-------|-------|----------|
| File (HDFS/S3) | No | Massive | Medium | Batch, data lake |
| RDBMS | Fixed | Limited | Medium | OLTP, reporting |
| NoSQL | Flexible | High | Fast | Real-time, varied data |
| In-Memory | Flexible | Limited (RAM) | Very fast | Caching, ML |
| Object Storage | No | Unlimited | Medium | Archival, media |

---

## **Section 2: Data Quality**

> PYQ: Discuss the importance of data quality in Big Data Management. What are the key challenges in ensuring data quality at scale? How can organizations address these challenges effectively? (2024, 15 marks)

### **2.1 What is Data Quality?**

**Definition:**

**Data Quality** refers to the **degree to which data is accurate, complete, consistent, timely, and fit for its intended use**. Poor data quality leads to wrong analysis, bad decisions, and loss of trust.

> "Garbage In, Garbage Out (GIGO)" — Low-quality input always produces unreliable output.

---

### **2.2 Dimensions of Data Quality**

| Dimension | Definition | Example of Problem |
|-----------|------------|--------------------|
| **Accuracy** | Data correctly represents real-world facts | Age = 250 years |
| **Completeness** | No missing values | Phone number field is blank |
| **Consistency** | Same data looks the same across sources | "Mumbai" vs "Bombay" |
| **Timeliness** | Data is up-to-date | Customer address from 5 years ago |
| **Validity** | Data conforms to defined formats/rules | Email without "@" |
| **Uniqueness** | No duplicate records | Same customer stored twice |
| **Integrity** | Relationships between data are correct | Order with no matching customer |

---

### **2.3 Common Data Quality Problems**

1. **Missing values** — null or blank fields.
2. **Duplicates** — same record stored more than once.
3. **Inconsistent formats** — date as "01/05/2026" vs "2026-05-01".
4. **Outliers** — values far outside normal range (may be errors).
5. **Stale data** — outdated information no longer valid.
6. **Referential integrity violations** — foreign key points to non-existent record.
7. **Encoding issues** — special characters corrupted.

---

### **2.4 Data Quality Management**

Steps to ensure data quality:

```
1. Profiling  → Analyze data to understand its current state
2. Cleansing  → Fix or remove bad data
3. Validation → Enforce rules at entry / ingestion
4. Monitoring → Continuously check data quality over time
5. Governance → Policies on who owns and is responsible for data
```

**Tools:** Apache Griffin, Great Expectations, Talend Data Quality, Informatica.

---

### **2.5 Importance of Data Quality in Big Data Management**

> PYQ: Discuss the importance of data quality in Big Data Management. (2024, 15 marks)

In Big Data environments, **the value of analytics is directly proportional to the quality of the data**. The following five reasons explain why quality is a non-negotiable foundation:

#### **1. Informed Decision-Making**
- High-quality data provides a **reliable basis** for business decisions.
- Executives, analysts, and managers depend on data to forecast trends and shape strategy.
- Poor data → wrong conclusions → costly strategic mistakes.

#### **2. Enhanced Operational Efficiency**
- Clean, accurate data **reduces errors, redundancies, and processing inefficiencies**.
- Less time wasted reconciling conflicting records → faster pipelines, lower compute cost.

#### **3. Regulatory Compliance**
- Industries like **healthcare, finance, and government** must follow strict regulations (HIPAA, GDPR, PCI-DSS, SOX).
- Quality data is required for **accurate reporting and auditing**; poor data → fines and legal risk.

#### **4. Improved Customer Experience**
- Accurate, complete customer data enables **personalised products, services, and communication**.
- Bad data leads to wrong recommendations, missed offers, and damaged customer trust.

#### **5. Optimized Data Analytics**
- Big Data analytics, ML models, and dashboards **depend entirely on data quality** for valid insights.
- Poor-quality input **undermines the value** of even the most sophisticated analytics platforms.

```
                ┌────────────────┐
   Raw Data  →  │  Quality Check │ → Reliable Insights → Better Decisions
                └────────────────┘
   (GIGO — without quality, output is unusable)
```

---

### **2.6 Key Challenges in Ensuring Data Quality at Scale**

Maintaining quality across petabyte-scale, fast-moving, heterogeneous data is far harder than on a traditional database. The challenges directly map to the **3 V's of Big Data**:

#### **1. Data Volume**
- With **petabytes streaming in daily**, manual monitoring becomes impractical.
- Even automated tools struggle to **profile, validate, and clean** at this scale without huge compute cost.

#### **2. Data Variety**
- Big Data combines **structured (RDBMS), semi-structured (JSON/XML), and unstructured (text, images, video)** sources.
- A **single uniform validation rule cannot cover all formats**, making consistency hard to enforce.

#### **3. Data Velocity**
- High-speed streaming sources (IoT sensors, clickstreams, social feeds) generate data **faster than it can be cleaned**.
- Rapid updates create **inconsistency** between source systems and downstream stores.

| Challenge | Root Cause | Typical Symptom |
|-----------|-----------|-----------------|
| Volume | Petabyte-scale ingestion | Missed bad records, slow profiling |
| Variety | Mixed structured + unstructured | Schema mismatches, conflicting values |
| Velocity | Real-time streams | Stale joins, duplicate / out-of-order events |

---

### **2.7 How Organizations Address Quality Challenges Effectively**

A robust quality strategy combines **policy, tooling, and process**. The following six approaches are widely adopted:

#### **1. Implement Data Governance Frameworks**
- Defines **how data is collected, managed, stored, and processed** across the organization.
- Assigns **data owners, stewards, and policies** so accountability is clear.

#### **2. Use Data Quality Tools**
- Specialized platforms automate profiling, cleansing, and validation.
- Examples: **Talend Data Quality, Informatica, Apache Nifi, Apache Griffin, Great Expectations**.

#### **3. Data Profiling and Monitoring**
- **Profiling** = analysing data to find anomalies, distributions, and missing values.
- **Continuous monitoring** detects quality drift early, before it pollutes downstream analytics.

#### **4. Data Integration and Standardization**
- Standardize **formats, units, codes, and structures** across heterogeneous systems.
- E.g., enforce ISO date format `YYYY-MM-DD` and uniform country codes.

#### **5. Data Cleansing and Enrichment**
- **Remove duplicates**, handle missing values, fix inconsistencies.
- **Enrich** records with reference data (e.g., add geo-coordinates from a postal code).

#### **6. Master Data Management (MDM)**
- Maintains a **single, consistent, authoritative view** of key business entities — customers, products, suppliers.
- Eliminates conflicting versions across silos (e.g., "Bombay" vs "Mumbai" for the same customer).

```
       Governance ──┐
       Tools ───────┤
       Profiling ───┼──►  CLEAN, TRUSTED DATA  ──►  Analytics
       Standardize ─┤
       Cleansing ───┤
       MDM ─────────┘
```

---

## **Section 3: Data Operations**

### **3.1 What are Data Operations?**

**Data Operations** (DataOps) refers to the **set of operations performed on data** during its lifecycle — from creation to deletion.

---

### **3.2 Core Data Operations**

| Operation | Description | SQL Equivalent |
|-----------|-------------|----------------|
| **Create** | Insert new data | INSERT |
| **Read** | Query and retrieve data | SELECT |
| **Update** | Modify existing data | UPDATE |
| **Delete** | Remove data | DELETE |
| **Aggregate** | Summarize data (sum, avg, count) | GROUP BY |
| **Filter** | Select subset of data | WHERE |
| **Join** | Combine data from multiple sources | JOIN |
| **Sort** | Order data by field | ORDER BY |
| **Transform** | Change data format or structure | ETL transform |

---

### **3.3 Types of Data Operations in Big Data**

#### **Batch Operations**
- Operate on large datasets at once.
- Scheduled jobs (nightly, weekly).
- Example: Monthly billing, end-of-day reports.

#### **Stream Operations**
- Operate on data as it flows in real time.
- Low latency.
- Example: Fraud alerts, live traffic routing.

#### **Interactive / Ad-hoc Operations**
- User-driven queries on demand.
- Example: Analyst runs a query to explore a dataset.

---

## **Section 4: Data Ingestion**

> PYQ: Write short note on Data Ingestion. (2023, 2.5 marks)

### **4.1 What is Data Ingestion?**

**Definition:**

**Data Ingestion** is the process of **importing data from various sources into a storage or processing system** for immediate use or later analysis.

It is the **first step** of any Big Data pipeline.

---

### **4.2 Types of Data Ingestion**

#### **1. Batch Ingestion**

- Data is collected over a period and loaded in chunks.
- Scheduled at fixed intervals (hourly, daily, weekly).

```
Source → Collect for 24 hours → Load all at once → Storage
```

**Best for:** Historical analysis, non-time-sensitive data.  
**Tools:** Sqoop, Spark batch jobs, Airflow.

---

#### **2. Real-Time / Streaming Ingestion**

- Data is ingested and processed continuously as it arrives.
- Very low latency (milliseconds to seconds).

```
Source → Kafka → Stream Processor → Storage / Dashboard
```

**Best for:** Fraud detection, live monitoring, IoT.  
**Tools:** Apache Kafka, Amazon Kinesis, Apache Flume.

---

#### **3. Micro-Batch Ingestion**

- A middle ground — data collected in very small batches (every few seconds/minutes).
- Example: Spark Structured Streaming.

---

### **4.3 Data Ingestion Challenges**

| Challenge | Description |
|-----------|-------------|
| **Schema mismatch** | Source and target formats don't match |
| **Data volume spikes** | Sudden surge overwhelms the ingestion system |
| **Latency** | Delay between data creation and availability |
| **Data loss** | Network failure during ingestion |
| **Duplicate data** | Same message ingested more than once |

**Solutions:** Kafka offset tracking, idempotent writes, schema registries, checkpointing.

---

## **Section 5: Scalability and Security**

> PYQ: Explain the concept of scalability in the context of Big Data storage and management systems. Discuss the scalability challenges associated with traditional DBMS and how they differ from those of Big Data Management System. (2024, 15 marks)

### **5.1 Scalability in Big Data**

(Refer to Unit 1, Section 4 for full detail on vertical vs horizontal scaling.)

**Key Scalability Techniques in Big Data:**

| Technique | Description |
|-----------|-------------|
| **Partitioning** | Split data across nodes by key (e.g., by date, region) |
| **Sharding** | Horizontal partitioning across database instances |
| **Replication** | Multiple copies of data for availability and read performance |
| **Load Balancing** | Distribute requests evenly across nodes |
| **Auto-scaling** | Automatically add/remove nodes based on load (cloud) |
| **Caching** | Store frequently accessed data in memory |

---

### **5.2 Security in Big Data**

Big Data systems deal with **sensitive personal, financial, and health data**, making security critical.

**Key Security Dimensions:**

#### **1. Authentication**
- Verify who is accessing the system.
- Tools: Kerberos (Hadoop), LDAP, OAuth.

#### **2. Authorization**
- Control what each user/role can do.
- Tools: Apache Ranger, Apache Sentry (Hadoop).
- Example: Analyst can READ data but not DELETE it.

#### **3. Encryption**

| Type | Description | Example |
|------|-------------|---------|
| **At Rest** | Data encrypted on disk | HDFS transparent encryption |
| **In Transit** | Data encrypted over network | TLS/SSL for Kafka |
| **End-to-End** | Encrypted from source to destination | Zero-knowledge systems |

#### **4. Auditing**
- Log all access and operations for compliance.
- Who accessed what data, when, and from where.
- Tools: Apache Ranger audit logs, AWS CloudTrail.

#### **5. Data Masking**
- Replace sensitive data with realistic fake data for testing.
- Example: Show "XXXX-XXXX-XXXX-1234" instead of full card number.

#### **6. Compliance**
- Laws and regulations govern data handling.
- **GDPR** (EU) — right to access, right to delete.
- **HIPAA** (US) — health data protection.
- **PCI-DSS** — payment card data protection.

---

### **5.3 Scalability — Traditional DBMS vs Big Data Management Systems (Unified Comparison)**

> PYQ: Explain the concept of scalability in the context of Big Data storage and management systems. Discuss the scalability challenges associated with traditional DBMS and how they differ from those of Big Data Management System. (2024, 15 marks)

**Scalability** is the ability of a system to **handle increasing volumes of data, users, and workload** without degradation in performance. In Big Data, scalability is the **most critical design property** because data grows exponentially.

#### **Two Types of Scalability**

| Type | Approach | Analogy |
|------|----------|---------|
| **Vertical (Scale Up)** | Add more **CPU, RAM, or storage** to a single server | Upgrade one truck to a bigger truck |
| **Horizontal (Scale Out)** | Add **more servers / nodes** to the network | Add more trucks to the fleet |

```
   Vertical:     [ Small Server ]  →  [   BIGGER  SERVER   ]
   Horizontal:   [ Node ]          →  [ Node ][ Node ][ Node ][ Node ]
```

---

#### **Scalability Challenges in Traditional DBMS**

Traditional relational DBMS (MySQL, Oracle, PostgreSQL) were designed for the **single-machine era**. At Big Data scale they hit serious limits:

**1. Limited Horizontal Scalability**
- Optimized primarily for **vertical scaling** — you upgrade one machine.
- Scaling out across nodes is possible but **complex and cost-prohibitive** at petabyte scale.

**2. Data Sharding Complexity**
- When data must span multiple servers, splitting it requires **manual sharding strategies**.
- Choosing the right shard key, rebalancing, and cross-shard joins are difficult and error-prone.

**3. Performance Degradation with Data Growth**
- As table sizes explode, **indexing and query optimization** become less effective.
- Joins and aggregations slow down dramatically; query plans break down.

**4. Relational Model Limitations**
- The **rigid, fixed schema** cannot easily accommodate unstructured (text, video, logs) or semi-structured (JSON, XML) data.
- Schema changes on huge tables are very expensive.

**5. High Costs**
- Vertical scaling requires **expensive enterprise-grade hardware** (high-end servers, SAN storage).
- The cost grows non-linearly and becomes **unsustainable** beyond a few terabytes.

---

#### **Scalability in Big Data Management Systems**

Big Data systems (Hadoop, Spark, Cassandra, MongoDB, BigQuery) were **built ground-up for scale-out**:

**1. Horizontal Scalability**
- Designed natively for **scale-out**: simply add more commodity nodes to the cluster.
- Cluster managers (YARN, Kubernetes) automatically distribute the new capacity.

**2. Data Distribution and Replication**
- Systems like **Hadoop HDFS** and **NoSQL stores** automatically distribute data across nodes.
- Built-in **replication** (e.g., HDFS default 3x) provides **fault tolerance** without manual effort.

**3. Schema Flexibility**
- **NoSQL** databases support **flexible / no fixed schema**, handling structured, semi-structured, and unstructured data uniformly.
- New fields can be added without downtime.

**4. Distributed Processing**
- Frameworks like **MapReduce and Apache Spark** process data **in parallel across all nodes**.
- Workloads scale linearly with cluster size.

**5. Cost-Effective Scaling**
- Built on **commodity hardware** or **cloud infrastructure**, making scaling significantly cheaper than vertical RDBMS scaling.

**6. Elasticity**
- Cloud-native services (**AWS EMR, Azure Synapse, Google BigQuery**) **auto-adjust resources** based on workload.
- Pay only for what you use; scale up for peak demand, down when idle.

---

#### **Side-by-Side Comparison**

| Aspect | Traditional DBMS | Big Data Management System |
|--------|-----------------|---------------------------|
| **Scaling Type** | Vertical (scale-up) | Horizontal (scale-out) |
| **Data Model** | Rigid relational schema | Flexible / schema-less (NoSQL) |
| **Sharding** | Manual, complex, error-prone | Automatic distribution across nodes |
| **Performance with Large Data** | Degrades as data grows | Scales linearly with nodes |
| **Cost of Scaling** | High — expensive hardware | Low — commodity / cloud |
| **Fault Tolerance** | Limited; needs extra setup | Built-in via replication |
| **Query Flexibility** | SQL only | SQL + MapReduce + APIs + streaming |

```
  Traditional DBMS:        Big Data System:
   ┌────────────┐           ┌───┐┌───┐┌───┐┌───┐
   │  BIG ONE   │           │ N ││ N ││ N ││ N │   (add more nodes)
   │   SERVER   │           └───┘└───┘└───┘└───┘
   └────────────┘             auto-shard + replicate
   vertical only             horizontal + elastic
```

---

## **Section 6: Traditional DBMS vs Big Data Management Systems**

> PYQ: Compare Traditional Data and Big Data. (2022, 15 marks)  
> PYQ: Explain different types of Big Data management techniques. (2023, 15 marks)

### **6.1 Overview**

Traditional DBMS was designed for an era of **smaller, structured data** on a **single machine**. Big Data Management Systems were designed for **massive, diverse data** across **clusters of machines**.

---

### **6.2 Detailed Comparison**

| Feature | Traditional DBMS | Big Data Management System |
|---------|-----------------|---------------------------|
| **Data Volume** | GB to small TB | TB to Exabytes |
| **Data Types** | Structured only | Structured + Semi + Unstructured |
| **Schema** | Fixed, schema-on-write | Flexible, schema-on-read |
| **Scaling** | Vertical (bigger machine) | Horizontal (more machines) |
| **Processing** | Single node | Distributed across cluster |
| **Query Language** | SQL | SQL + MapReduce + Dataflow |
| **Consistency** | Strong (ACID) | Eventual (BASE) |
| **Fault Tolerance** | Limited | Built-in (replication) |
| **Cost** | Expensive hardware | Commodity servers |
| **Speed** | Fast for small data | Fast for large-scale batch |
| **Real-time** | Good | Improving (Kafka, Spark) |
| **Examples** | MySQL, Oracle, PostgreSQL | Hadoop, HBase, Cassandra, Spark |

---

### **6.3 When to Use What?**

| Use Traditional DBMS when... | Use Big Data System when... |
|------------------------------|------------------------------|
| Data is structured and small | Data is TB/PB scale |
| ACID transactions are critical | Flexibility > strict consistency |
| Complex joins are needed | High write throughput needed |
| Mature tooling is required | Data has varied formats |
| Single-site deployment | Distributed, multi-node needed |

---

### **6.4 Big Data Management Techniques**

> PYQ: Explain different types of Big Data management techniques. (2023, 15 marks)

Modern organizations apply a **portfolio of techniques** to manage Big Data effectively. The eight most widely used are:

#### **1. Data Governance**
- Set of **policies, standards, and roles** that ensure data is **used consistently and correctly** across the organization.
- Defines who owns data, who can access it, and how it must be handled.

#### **2. Data Quality Management**
- Continuous process of **measuring and improving** the quality of organizational data.
- Covers accuracy, completeness, consistency, timeliness — keeps data fit for analytics.

#### **3. Data Mining**
- Applies **machine learning and statistical methods** to discover hidden patterns, correlations, and trends in large datasets.
- Powers tasks like market basket analysis and customer segmentation.

#### **4. Data Security**
- Protects data from **unauthorized access, breaches, leakage, and loss**.
- Uses encryption, authentication, authorization, masking, and auditing.

#### **5. Big Data Analytics**
- Extracts actionable insights from huge volumes — **market trends, customer preferences, hidden patterns**.
- Includes descriptive, diagnostic, predictive, and prescriptive analytics.

#### **6. Machine Learning**
- Algorithms that allow systems to **learn patterns and make predictions** without being explicitly programmed.
- Used for recommendation engines, fraud detection, image recognition.

#### **7. Predictive Analytics**
- Uses historical data + ML to **forecast future outcomes** — buyer preferences, demand, churn, equipment failure.
- Drives proactive business decisions.

#### **8. Centralized Data Management**
- **Stores and manages all organizational data in a single repository** (data warehouse / data lake).
- Eliminates silos, gives a unified view, simplifies governance and analytics.

```
              ┌─── Governance ──── Security ────┐
              │                                  │
   DATA  →   │  Quality Mgmt + Centralized Mgmt │   →  Business Value
              │                                  │
              └── Mining ─ Analytics ─ ML ─ Predictive ──┘
```

---

## **Section 7: Real-Life Applications**

> PYQ: Describe any five real life applications of Big Data. (2022, 15 marks)  
> PYQ: Write short note on real life applications of Big Data. (2023, 15 marks)

### **7.1 Applications of Big Data Modeling & Management**

**1. Healthcare:**
- **Electronic Health Records (EHR)** — managing patient data at hospital scale.
- **Genomics** — storing and querying 3 GB genome per patient.
- **Clinical trial management** — tracking outcomes across thousands of patients.

**2. Finance:**
- **Transaction management** — millions of records per second, ACID critical.
- **Risk modeling** — large-scale Monte Carlo simulations on historical data.
- **Regulatory compliance** — storing 7+ years of transaction history.

**3. Retail / E-commerce:**
- **Product catalog management** — millions of SKUs with varied attributes (document DB).
- **Customer 360** — unified view of customer across channels.
- **Real-time inventory** — Cassandra/HBase for low-latency stock updates.

**4. Telecommunications:**
- **Call Detail Records (CDR)** — billions of records daily, column-family stores.
- **Network topology** — graph databases for network maps.

**5. Social Media:**
- **User profiles** — document stores (MongoDB).
- **Connections/followers** — graph databases (Neo4j).
- **Posts and feeds** — time-series column stores (Cassandra).

---

## **Section 8: Data Models**

> PYQ: What are different types of data models and their applications in organizing and structuring large datasets? (2024, 2.5 marks)  
> PYQ: What is Modeling? Explain various types of data models with example. (2023, 15 marks)

### **8.1 What is a Data Model?**

**Definition:**

A **Data Model** is an **abstract representation** of how data is organized, stored, and accessed. It defines:
- The **structure** of data (how it is organized).
- The **operations** that can be performed on it.
- The **constraints** (rules) that data must satisfy.

**Purpose of a Data Model:**
- Provides a common language between developers and stakeholders.
- Guides database design.
- Ensures data integrity and consistency.

---

### **8.2 Three Components of a Data Model**

#### **1. Structure**
- How data is organized and stored.
- Defines entities, attributes, and relationships.

```
Student (StudentID, Name, Age, CourseID)
Course  (CourseID, CourseName, Credits)
```

#### **2. Operations**
- What you can do with the data.
- CRUD operations: Create, Read, Update, Delete.
- Queries, aggregations, transformations.

```
SELECT Name FROM Student WHERE Age > 20;
UPDATE Student SET Age = 23 WHERE StudentID = 001;
```

#### **3. Constraints**
- Rules that data must follow to remain valid.

| Constraint Type | Example |
|-----------------|---------|
| **Domain** | Age must be between 0 and 150 |
| **Key** | StudentID must be unique (primary key) |
| **Referential** | CourseID in Student must exist in Course table |
| **Not Null** | Name cannot be empty |
| **Check** | Salary must be > 0 |

---

### **8.3 Types of Big Data Models**

#### **1. Relational Model**

- Data organized in **tables** (relations) with rows and columns.
- Uses SQL.
- Strong schema, ACID properties.

```
Student Table:
| ID  | Name   | Age |
|-----|--------|-----|
| 001 | Deepak | 22  |
```

**When to use:** Structured data, transactional systems.

---

#### **2. Key-Value Model**

- Data stored as **(key, value)** pairs.
- No structure to the value — it's a blob.
- Extremely fast lookup.

```
"student:001" → "{"name":"Deepak","age":22}"
"session:xyz" → "active"
```

**When to use:** Caching, session management, shopping carts.

---

#### **3. Document Model**

- Data stored as **self-describing documents** (JSON, BSON, XML).
- Each document can have different fields.
- Nested structures supported.

```json
{
  "_id": "001",
  "name": "Deepak",
  "courses": ["ML", "BDA"],
  "address": {"city": "Jaipur"}
}
```

**When to use:** Content management, user profiles, product catalogs.

---

#### **4. Column-Family Model**

- Data stored in **rows** but grouped by **column families**.
- Optimized for reading/writing specific columns.
- Sparse data (rows can have different columns).

```
RowKey    | PersonalInfo          | Academics
──────────────────────────────────────────────
student01 | name=Deepak, age=22  | math=90
student02 | name=Ankit           | math=75, sci=80
```

**When to use:** Time-series, IoT, messaging, analytics.

---

#### **5. Graph Model**

- Data stored as **nodes (entities)** and **edges (relationships)**.
- Best when relationships between data are as important as the data itself.

```
(Deepak) ──FRIENDS──► (Ankit)
(Deepak) ──ENROLLED──► (ML Course)
```

**When to use:** Social networks, fraud detection, recommendation engines.

---

#### **6. Array / Vector Model**

- Data stored in multi-dimensional arrays.
- Used in scientific computing and geospatial data.
- Example: Satellite imagery stored as 3D arrays (lat × lon × time).

**When to use:** Scientific data, geospatial, raster images.

---

### **8.4 Types of Big Data Models — Summary Table**

| Model | Structure | Query Style | Example System | Best Use Case |
|-------|-----------|-------------|----------------|---------------|
| **Relational** | Tables | SQL | MySQL, Redshift | Transactions |
| **Key-Value** | Key→Value | GET/SET | Redis, DynamoDB | Caching |
| **Document** | JSON/BSON docs | Document query | MongoDB | Profiles, catalogs |
| **Column-Family** | Column groups | Row+column key | Cassandra, HBase | IoT, time-series |
| **Graph** | Nodes + Edges | Graph traversal | Neo4j, Neptune | Social, networks |
| **Array** | Multi-dim array | Array slicing | SciDB, NetCDF | Scientific, GIS |

---

## **Quick Revision Points**

### **Data Storage Types:**
- File (HDFS/S3), Relational, NoSQL, In-Memory, Object Storage.

### **Data Quality Dimensions:**
- Accuracy, Completeness, Consistency, Timeliness, Validity, Uniqueness, Integrity.

### **Importance of Data Quality (5 reasons):**
- Informed decision-making, operational efficiency, regulatory compliance, customer experience, optimized analytics.

### **Data Quality Challenges at Scale (3 V's):**
- Volume (manual checks impractical), Variety (mixed formats), Velocity (streams cause inconsistency).

### **Data Quality Solutions (6 approaches):**
- Governance frameworks, quality tools (Talend/Informatica/Nifi), profiling & monitoring, standardization, cleansing & enrichment, Master Data Management (MDM).

### **Data Ingestion Types:**
- Batch (Sqoop), Streaming (Kafka), Micro-batch (Spark Streaming).

### **Scalability Techniques:**
- Partitioning, Sharding, Replication, Load Balancing, Caching, Auto-scaling.

### **Scalability — DBMS vs Big Data (Unified):**
- DBMS challenges → limited horizontal scale, sharding complexity, performance drop, rigid schema, high cost.
- Big Data wins → horizontal scale, distribution + replication, schema flexibility, distributed processing, cost-effective, elastic cloud.

### **Security Layers:**
- Authentication, Authorization, Encryption (at rest + in transit), Auditing, Masking, Compliance.

### **Traditional DBMS vs Big Data:**

| | DBMS | Big Data |
|--|------|----------|
| Scale | GB | TB–EB |
| Schema | Fixed | Flexible |
| Scaling | Vertical | Horizontal |
| Consistency | ACID | BASE |

### **Data Model Components:**
- **Structure** → how organized
- **Operations** → what you can do
- **Constraints** → rules data must follow

### **Types of Big Data Models:**
Relational → Key-Value → Document → Column-Family → Graph → Array

### **Big Data Management Techniques (8):**
Data Governance, Data Quality Management, Data Mining, Data Security, Big Data Analytics, Machine Learning, Predictive Analytics, Centralized Data Management.

---

## **Expected Exam Questions**

### **15-Mark Questions:**

1. What is Modeling? Explain various types of data models with example. *(2023)*
2. Explain the concept of scalability in the context of Big Data storage and management systems. Discuss the scalability challenges associated with traditional DBMS and how they differ from those of Big Data Management System. *(2024)*
3. Discuss the importance of data quality in Big Data Management. What are the key challenges in ensuring data quality at scale? How can organizations address these challenges effectively? *(2024)*
4. Explain different types of Big Data management techniques. *(2023)*
5. Compare Traditional Data and Big Data. *(2022)*
6. Describe any five real life applications of Big Data. *(2022)*
7. Write short note on real life applications of Big Data. *(2023)*

### **Short Answer Questions (2.5 marks):**

1. Write short note on Data Ingestion. *(2023)*
2. What are different types of data models and their applications in organizing and structuring large datasets? *(2024)*

---

_These notes were compiled by [Deepak Modi](https://deepakmodi.dev)_  
_Last updated: May 2026_
