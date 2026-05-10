---
title: "Unit 2: Data Repositories and Big Data Platforms"
description: "RDBMS, NoSQL, Data Marts, Data Lakes, ETL, Data Pipelines, Big Data Processing Tools, Modern Data Ecosystem, Types of Data, File Formats, and Service Bindings."
author: "Deepak Modi"
date: "2026-05-10"
pdfUrl: ""
---

## Syllabus:

**Data Repositories and Big Data Platforms:** RDBMS, NoSQL, Data Marts, Data Lakes, ETL, and Data Pipelines, Foundations of Big Data, Big Data Processing Tools, Modern Data Ecosystem, Key Players, Types of Data, Understanding Different Types of File Formats, Sources of Data Using Service Bindings.

---

## 🎯 PYQ Analysis for Unit 2

> PYQs will be added after analysis — check back soon.

---

## **Section 1: RDBMS**

### **1.1 What is RDBMS?**

**Definition:**

A **Relational Database Management System (RDBMS)** is a database system that stores data in **tables (relations)** with rows and columns, and uses **SQL (Structured Query Language)** to manage and query data. Relationships between tables are established using **primary keys** and **foreign keys**.

**Simple Analogy:**

Think of an RDBMS like a well-organized set of Excel spreadsheets where each sheet is a table, and the sheets are linked to each other using unique IDs.

---

### **1.2 Key Concepts of RDBMS**

| Concept | Definition |
|---------|------------|
| **Table** | Collection of rows and columns (like a spreadsheet) |
| **Row (Tuple)** | One record / data entry |
| **Column (Attribute)** | One field / property |
| **Primary Key** | Unique identifier for each row |
| **Foreign Key** | Column that links to primary key of another table |
| **Schema** | Fixed structure defining table columns and data types |
| **SQL** | Language used to create, read, update, delete data |

---

### **1.3 ACID Properties**

RDBMS guarantees data integrity through **ACID properties**:

| Property | Meaning | Example |
|----------|---------|---------|
| **Atomicity** | Transaction is all-or-nothing | Bank transfer: debit + credit both happen or neither does |
| **Consistency** | DB always moves from one valid state to another | Balance can't go negative if rule says so |
| **Isolation** | Concurrent transactions don't interfere | Two users buying last ticket — only one succeeds |
| **Durability** | Committed data is permanently saved | Data survives power failure |

---

### **1.4 Advantages and Limitations of RDBMS**

**Advantages:**

✅ Structured and organized data.  
✅ Powerful querying with SQL.  
✅ Strong ACID guarantees.  
✅ Well-understood, mature technology.  
✅ Excellent for transactional (OLTP) workloads.

**Limitations in Big Data context:**

❌ Does not scale horizontally (designed for vertical scaling).  
❌ Fixed schema — cannot handle unstructured data (images, JSON, logs).  
❌ Poor performance with very large datasets (billions of rows).  
❌ Joins across large tables are slow.  
❌ Not designed for real-time streaming data.

**Popular RDBMS:** MySQL, PostgreSQL, Oracle, Microsoft SQL Server, SQLite.

---

## **Section 2: NoSQL**

### **2.1 What is NoSQL?**

**Definition:**

**NoSQL** (Not Only SQL) refers to a class of database systems that **do not use the traditional relational table model**. They are designed to handle:
- **Unstructured or semi-structured data**
- **Massive scale** (horizontal scaling)
- **High velocity** reads/writes
- **Flexible schemas** (no fixed column structure)

**Why NoSQL for Big Data?**

Traditional RDBMS struggles when:
- Data has no fixed structure (social media posts, sensor readings).
- Billions of records need to be read/written per second.
- Data needs to be spread across hundreds of servers.

---

### **2.2 Types of NoSQL Databases**

#### **1. Key-Value Stores**

- Simplest type — data stored as **(key, value)** pairs.
- Like a dictionary / hashmap.
- Very fast lookup by key.

```
Key         Value
───────────────────────────
user:001  → {"name":"Deepak","age":22}
user:002  → {"name":"Ankit","age":23}
session:x → "active"
```

**Examples:** Redis, DynamoDB, Riak  
**Use cases:** Caching, session management, leaderboards.

---

#### **2. Document Stores**

- Data stored as **documents** (usually JSON or BSON).
- Each document can have a **different structure** (schema-less).
- Documents are grouped in **collections** (like tables in RDBMS).

```json
{
  "_id": "001",
  "name": "Deepak",
  "courses": ["ML", "BDA"],
  "address": {
    "city": "Jaipur",
    "pin": "302001"
  }
}
```

**Examples:** MongoDB, CouchDB, Firebase Firestore  
**Use cases:** Content management, catalogs, user profiles, real-time apps.

---

#### **3. Column-Family Stores (Wide-Column)**

- Data stored in **rows**, but each row can have **different columns**.
- Columns are grouped into **column families**.
- Optimized for reading/writing specific columns across many rows.

```
Row Key   | Personal Info         | Scores
──────────┼───────────────────────┼──────────────
user001   | name="Deepak",age=22  | math=90,sci=85
user002   | name="Ankit"          | math=75
```

**Examples:** Apache HBase, Apache Cassandra, Google Bigtable  
**Use cases:** Time-series data, IoT, analytics, messaging systems.

---

#### **4. Graph Databases**

- Data stored as **nodes (entities)** and **edges (relationships)**.
- Best for data where relationships are the primary value.

```
(Deepak) ──FRIENDS──► (Ankit)
(Deepak) ──ENROLLED──► (ML Course)
(Ankit)  ──ENROLLED──► (BDA Course)
```

**Examples:** Neo4j, Amazon Neptune, ArangoDB  
**Use cases:** Social networks, fraud detection, recommendation engines, knowledge graphs.

---

### **2.3 RDBMS vs NoSQL**

| Feature | RDBMS | NoSQL |
|---------|-------|-------|
| **Data Model** | Tables (rows & columns) | Key-value, document, column, graph |
| **Schema** | Fixed (rigid) | Flexible (dynamic) |
| **Scaling** | Vertical (scale up) | Horizontal (scale out) |
| **Query Language** | SQL | Varies (no standard) |
| **ACID** | Full ACID | Often BASE (eventual consistency) |
| **Data Type** | Structured only | Structured, semi, unstructured |
| **Performance** | Slower at huge scale | Faster for simple queries at scale |
| **Examples** | MySQL, Oracle | MongoDB, Cassandra, Redis |
| **Use Case** | Banking, ERP | Social media, IoT, real-time |

**BASE properties (NoSQL alternative to ACID):**

| Property | Meaning |
|----------|---------|
| **B**asically Available | System is always available (may return stale data) |
| **S**oft State | State may change over time without input |
| **E**ventual Consistency | Data will eventually be consistent across nodes |

---

## **Section 3: Data Warehouses, Data Marts, and Data Lakes**

### **3.1 Data Warehouse**

**Definition:**

A **Data Warehouse** is a large, centralized repository that stores **integrated, historical, and structured data** from multiple sources, optimized for **analytical queries (OLAP)** rather than transactional processing (OLTP).

```
  Source Systems                     Data Warehouse
  ──────────────                     ───────────────
  Sales DB   ──┐
  HR DB      ──┼──► ETL Process ──► Centralized   ──► BI Reports
  Finance DB ──┤                    Warehouse         Analytics
  CRM        ──┘                    (OLAP)            Dashboards
```

**Key Characteristics:**

- **Subject-oriented** — organized around subjects (sales, customers).
- **Integrated** — data from multiple sources combined.
- **Non-volatile** — data is not deleted; historical data is kept.
- **Time-variant** — data is tracked over time (time dimension always present).

**Popular tools:** Amazon Redshift, Google BigQuery, Snowflake, Teradata.

---

### **3.2 Data Marts**

**Definition:**

A **Data Mart** is a **smaller, focused subset** of a data warehouse that serves the needs of a **specific department or business unit**.

```
                 ┌─────────────────┐
                 │  Data Warehouse │
                 └────────┬────────┘
          ┌───────────────┼───────────────┐
          ▼               ▼               ▼
   ┌─────────────┐ ┌─────────────┐ ┌─────────────┐
   │ Sales Mart  │ │ HR Mart     │ │ Finance Mart│
   └─────────────┘ └─────────────┘ └─────────────┘
   (Sales team)    (HR team)        (Finance team)
```

**Types:**

| Type | Description |
|------|-------------|
| **Dependent Mart** | Created from the central data warehouse |
| **Independent Mart** | Created directly from source systems |
| **Hybrid Mart** | Combination of both |

**Data Warehouse vs Data Mart:**

| | Data Warehouse | Data Mart |
|--|----------------|-----------|
| **Scope** | Enterprise-wide | Department-specific |
| **Size** | Very large (TB–PB) | Smaller (GB–TB) |
| **Users** | All departments | One team |
| **Build time** | Months | Weeks |

---

### **3.3 Data Lakes**

**Definition:**

A **Data Lake** is a centralized repository that stores **raw data in its original format** (structured, semi-structured, and unstructured) at any scale. Data is stored **as-is** until it is needed.

**Key Idea:** Store everything now, figure out the schema when you read it (**schema-on-read**).

```
  Sources                     Data Lake
  ───────                     ─────────
  IoT sensors ──┐
  Web logs    ──┼──► Store raw ──► Analytics
  Social media──┤    data as-is    ML models
  Videos      ──┤    (no schema)   Data science
  CSVs        ──┘
```

**Data Warehouse vs Data Lake:**

| | Data Warehouse | Data Lake |
|--|----------------|-----------|
| **Data Type** | Structured only | All types |
| **Schema** | Schema-on-write | Schema-on-read |
| **Users** | Business analysts | Data scientists |
| **Processing** | Pre-processed | Raw data |
| **Cost** | Higher | Lower (object storage) |
| **Agility** | Less flexible | Highly flexible |
| **Risk** | Low (clean data) | "Data Swamp" if unmanaged |

> **Data Swamp:** A data lake that becomes disorganized and unusable because data is dumped in without governance.

**Popular platforms:** AWS S3 + Glue, Azure Data Lake Storage, Google Cloud Storage, Databricks Delta Lake.

---

## **Section 4: ETL and Data Pipelines**

### **4.1 What is ETL?**

**Definition:**

**ETL** stands for **Extract, Transform, Load** — it is the process of moving data from source systems into a data warehouse or data lake for analysis.

```
  Source Systems          ETL Process              Target
  ──────────────         ─────────────            ────────
  Database A   ──► EXTRACT ──► TRANSFORM ──► LOAD ──► Data Warehouse
  Database B   ──►           (clean,              ──► Data Lake
  API / Files  ──►            convert,            ──► Analytics DB
                              aggregate)
```

---

### **4.2 Three Phases of ETL**

#### **Phase 1: Extract**
- Pull raw data from **multiple source systems**.
- Sources: RDBMS, flat files (CSV), APIs, web scraping, IoT sensors.
- Data may be in different formats and quality.
- **Full extraction** (all data) or **incremental extraction** (only changed data).

#### **Phase 2: Transform**
- The most complex phase.
- Clean and shape data into a consistent format for analysis.

**Common transformations:**

| Operation | Description |
|-----------|-------------|
| **Cleaning** | Handle missing values, remove duplicates |
| **Filtering** | Select only relevant rows/columns |
| **Mapping** | Convert data types (string → date) |
| **Aggregation** | Group and summarize (SUM, AVG, COUNT) |
| **Joining** | Combine data from multiple sources |
| **Sorting** | Order data |
| **Encoding** | Convert categories to codes |
| **Normalization** | Standardize numeric ranges |

#### **Phase 3: Load**
- Write the transformed data into the **target system** (data warehouse/lake).
- **Full load** — overwrite everything.
- **Incremental load** — only add new/changed records (delta load).

---

### **4.3 ELT vs ETL**

Modern cloud systems sometimes use **ELT** (Extract → Load → Transform):

| | ETL | ELT |
|--|-----|-----|
| **Order** | Transform before loading | Load raw, transform later |
| **Where transformed** | Separate transformation server | Inside the target system |
| **Best for** | Traditional data warehouses | Cloud data lakes / warehouses |
| **Flexibility** | Less (schema must match) | More (raw data preserved) |
| **Examples** | Informatica, Talend | dbt, BigQuery, Snowflake |

---

### **4.4 Data Pipelines**

**Definition:**

A **Data Pipeline** is an automated sequence of steps (stages) that moves data from one or more sources to a destination, performing transformations along the way.

**ETL is a type of data pipeline**, but pipelines can also include:
- Data validation
- Monitoring and alerting
- Scheduling
- Error handling and retries

**Pipeline Types:**

| Type | Description | Example |
|------|-------------|---------|
| **Batch Pipeline** | Processes data in chunks at scheduled intervals | Nightly ETL job |
| **Streaming Pipeline** | Processes data continuously in real time | Live fraud detection |
| **Lambda Architecture** | Combines batch + streaming layers | Twitter analytics |
| **Kappa Architecture** | Streaming only (no separate batch layer) | Kafka-based systems |

**Popular Data Pipeline Tools:**

| Tool | Type | Use Case |
|------|------|----------|
| Apache Airflow | Batch orchestration | Scheduling complex workflows |
| Apache Kafka | Streaming | Real-time event streaming |
| Apache NiFi | Data flow | Drag-and-drop pipeline builder |
| AWS Glue | Cloud ETL | Serverless ETL on AWS |
| dbt | Transformation | SQL-based data transformation |
| Spark | Batch + Stream | Large-scale data processing |

---

## **Section 5: Big Data Processing Tools**

### **5.1 Apache Hadoop**

**Hadoop** is an open-source framework for storing and processing Big Data in a **distributed** environment using clusters of commodity hardware.

**Core Components:**

```
┌───────────────────────────────────────┐
│              Hadoop Ecosystem         │
├───────────────────────────────────────┤
│  HDFS   │  Distributed file storage   │
│  YARN   │  Resource manager           │
│  MapReduce│ Batch processing engine   │
└───────────────────────────────────────┘
```

| Component | Role |
|-----------|------|
| **HDFS** | Distributed file system (storage) |
| **YARN** | Cluster resource manager (who gets CPU/memory) |
| **MapReduce** | Parallel batch processing model |

---

### **5.2 Apache Spark**

**Apache Spark** is a **fast, in-memory** distributed processing engine. It is the successor to MapReduce for most workloads.

**Key Advantage over MapReduce:**

```
MapReduce: Read from disk → Process → Write to disk → Read → Process → Write...
           (every step goes to disk = SLOW)

Spark:     Read from disk → Process in RAM → Process in RAM → Write to disk
           (keeps data in memory = UP TO 100x FASTER)
```

**Spark Components:**

| Component | Purpose |
|-----------|---------|
| **Spark Core** | Basic processing engine |
| **Spark SQL** | SQL queries on structured data |
| **Spark Streaming** | Real-time stream processing |
| **MLlib** | Machine learning library |
| **GraphX** | Graph processing |

---

### **5.3 Other Key Tools**

| Tool | Category | Purpose |
|------|----------|---------|
| **Apache Hive** | Query | SQL-like queries on HDFS (batch) |
| **Apache Pig** | Scripting | Data flow using Pig Latin language |
| **Apache HBase** | NoSQL DB | Real-time read/write on HDFS |
| **Apache Kafka** | Messaging | High-throughput event streaming |
| **Apache Storm** | Stream | Real-time stream processing |
| **Apache Flink** | Stream | Low-latency stateful stream processing |
| **Apache Sqoop** | Ingestion | Import/export between RDBMS and HDFS |
| **Apache Flume** | Ingestion | Collect and move log data to HDFS |
| **Zookeeper** | Coordination | Distributed coordination service |

---

## **Section 6: Modern Data Ecosystem and Key Players**

### **6.1 Modern Data Ecosystem**

The **Modern Data Ecosystem** is the complete landscape of tools, technologies, and processes that organizations use to collect, store, process, and analyze data.

```
┌─────────────────────────────────────────────────────────┐
│                  Modern Data Ecosystem                  │
├──────────────┬──────────────┬──────────────┬────────────┤
│  Data        │  Storage     │  Processing  │  Consume   │
│  Sources     │              │              │            │
├──────────────┼──────────────┼──────────────┼────────────┤
│ Databases    │ Data Lakes   │ Spark        │ BI Tools   │
│ APIs         │ Data Warehouses│ Kafka      │ ML Models  │
│ IoT devices  │ Cloud Storage│ Flink        │ Dashboards │
│ Web logs     │ HDFS         │ MapReduce    │ Reports    │
│ Social media │ NoSQL        │ Airflow      │ Apps       │
└──────────────┴──────────────┴──────────────┴────────────┘
```

---

### **6.2 Key Players in the Big Data Industry**

**Cloud Providers:**

| Company | Platform | Key Services |
|---------|----------|-------------|
| **Amazon (AWS)** | AWS | S3, EMR, Redshift, Glue, Kinesis |
| **Google** | GCP | BigQuery, Dataflow, Pub/Sub, Dataproc |
| **Microsoft** | Azure | Azure Data Lake, Synapse, HDInsight |

**Open Source / Software Vendors:**

| Company/Project | Contribution |
|-----------------|-------------|
| **Apache Foundation** | Hadoop, Spark, Kafka, Hive, Flink |
| **Databricks** | Managed Spark, Delta Lake |
| **Cloudera** | Enterprise Hadoop distribution |
| **MongoDB** | NoSQL document database |
| **Elastic** | Elasticsearch for search & analytics |
| **Confluent** | Managed Kafka platform |

**BI and Analytics:**

| Tool | Use |
|------|-----|
| **Tableau** | Data visualization |
| **Power BI** | Microsoft BI platform |
| **Looker** | Data exploration (Google) |
| **Grafana** | Monitoring dashboards |

---

## **Section 7: Types of Data**

### **7.1 Classification by Structure**

Data in the Big Data world falls into three categories:

#### **1. Structured Data**

- Has a **predefined schema** (fixed columns and data types).
- Stored in rows and columns.
- Easily searchable with SQL.

```
| ID  | Name    | Age | Salary  |
|-----|---------|-----|---------|
| 001 | Deepak  | 22  | 50000   |
| 002 | Ankit   | 23  | 55000   |
```

**Examples:** Bank transactions, HR records, inventory.  
**Storage:** RDBMS, CSV files.  
**Volume:** ~20% of all data generated.

---

#### **2. Semi-Structured Data**

- Has **some structure** but no strict schema.
- Uses **tags, keys, or markers** to separate elements.
- More flexible than structured data.

**JSON Example:**
```json
{
  "user": "Deepak",
  "age": 22,
  "skills": ["Python", "ML", "BDA"]
}
```

**XML Example:**
```xml
<student>
  <name>Deepak</name>
  <age>22</age>
</student>
```

**Examples:** JSON, XML, HTML, emails, log files, NoSQL documents.  
**Volume:** ~5–10% of all data.

---

#### **3. Unstructured Data**

- Has **no predefined format** or schema.
- Cannot be stored directly in RDBMS.
- Largest and fastest-growing category.

**Examples:**
- Text: emails, social media posts, chat logs
- Images: photos, medical scans, satellite images
- Audio: call recordings, music
- Video: surveillance footage, YouTube videos

**Volume:** ~80% of all data generated today.

---

### **7.2 Classification by Processing Time**

| Type | Description | Example |
|------|-------------|---------|
| **Historical / Batch** | Stored data processed in chunks | Monthly sales report |
| **Real-time / Streaming** | Data processed as it arrives | Live fraud alert |
| **Near real-time** | Small delay (seconds/minutes) | Dashboard refresh |

---

### **7.3 Classification by Source**

| Type | Description | Example |
|------|-------------|---------|
| **Internal data** | Generated within organization | Employee records |
| **External data** | From outside sources | Social media, open datasets |
| **First-party data** | Collected directly from customers | Website clicks |
| **Second-party data** | Shared from a partner | Partner CRM data |
| **Third-party data** | Purchased from data aggregators | Market research firms |

---

## **Section 8: File Formats in Big Data**

### **8.1 Why File Format Matters**

Choosing the right file format affects:
- **Storage space** (compression)
- **Query speed** (columnar vs row-based)
- **Compatibility** (which tools can read it)
- **Schema evolution** (can you add fields later?)

---

### **8.2 Common Big Data File Formats**

#### **1. CSV (Comma-Separated Values)**

```
name,age,city
Deepak,22,Jaipur
Ankit,23,Delhi
```

- Simple, human-readable text format.
- No compression (large file size).
- No schema enforcement.
- **Best for:** Small datasets, data exchange, spreadsheet imports.

---

#### **2. JSON (JavaScript Object Notation)**

```json
{"name": "Deepak", "age": 22, "city": "Jaipur"}
{"name": "Ankit",  "age": 23, "city": "Delhi"}
```

- Human-readable, flexible schema.
- Supports nested structures.
- Verbose (large file size).
- **Best for:** APIs, web data, semi-structured data.

---

#### **3. Parquet**

- **Columnar** storage format (stores data column by column, not row by row).
- Highly compressed.
- Optimized for **analytical queries** (reading specific columns).

```
Row-based (CSV):        Columnar (Parquet):
Row 1: Deepak,22,Jaipur     Name col:  Deepak, Ankit
Row 2: Ankit, 23, Delhi  → Age col:   22, 23
Row 3: ...                  City col:  Jaipur, Delhi
```

- **Best for:** Analytics on specific columns (most big data workloads).
- Used by: Spark, Hive, Hadoop, BigQuery.

---

#### **4. Avro**

- **Row-based** binary format.
- Schema stored with the data (self-describing).
- Supports **schema evolution** (can add/remove fields).
- **Best for:** Data serialization, Kafka messaging, Hadoop ingestion.

---

#### **5. ORC (Optimized Row Columnar)**

- Columnar format optimized for **Apache Hive**.
- Better compression than Parquet in some cases.
- Supports ACID transactions in Hive.
- **Best for:** Hive workloads, data warehousing.

---

#### **6. Sequence File**

- Hadoop-native binary format.
- Stores key-value pairs.
- Supports compression.
- **Best for:** Intermediate MapReduce output.

---

### **8.3 File Format Comparison**

| Format | Type | Compressed | Schema | Best For |
|--------|------|-----------|--------|----------|
| **CSV** | Row, text | No | No | Simple exchange |
| **JSON** | Row, text | No | Flexible | APIs, semi-structured |
| **Parquet** | Columnar, binary | Yes | Yes | Analytics (Spark, Hive) |
| **Avro** | Row, binary | Yes | Yes (embedded) | Streaming, Kafka |
| **ORC** | Columnar, binary | Yes | Yes | Hive, data warehouse |
| **Sequence** | Row, binary | Optional | No | Hadoop MapReduce |

---

## **Section 9: Sources of Data Using Service Bindings**

### **9.1 What are Service Bindings?**

**Service Bindings** (also called **data source connectors** or **service integrations**) are mechanisms that allow Big Data platforms to **connect to and ingest data from external services and sources** without manually moving files.

---

### **9.2 Types of Service Bindings / Data Sources**

#### **1. Database Connectors**

- Connect directly to RDBMS or NoSQL databases.
- Tools: **Apache Sqoop** (RDBMS ↔ HDFS), **Spark JDBC connector**.

```
MySQL Database ──► Sqoop ──► HDFS / Data Lake
Oracle DB      ──► JDBC  ──► Spark
```

---

#### **2. Message Queue / Streaming Services**

- Real-time data ingestion from event streams.
- Tools: **Apache Kafka**, **Amazon Kinesis**, **Google Pub/Sub**.

```
Web events / Clicks ──► Kafka Topic ──► Spark Streaming ──► Analytics
```

---

#### **3. REST APIs**

- Pull data from web services using HTTP requests.
- Response usually in JSON or XML.

```
Twitter API ──► HTTP GET ──► JSON data ──► Data Lake
Weather API ──► HTTP GET ──► JSON data ──► Analysis
```

---

#### **4. Cloud Storage Bindings**

- Direct access to cloud object storage.
- **AWS S3**, **Azure Blob Storage**, **Google Cloud Storage**.
- Spark / Hadoop can read files directly from S3 without downloading.

```
S3 bucket (CSV files) ──► Spark ──► Processed results ──► Redshift
```

---

#### **5. File System / FTP / SFTP**

- Batch file ingestion from file servers.
- Tools: **Apache Flume**, **NiFi**.

```
FTP Server (log files) ──► Flume ──► HDFS
```

---

#### **6. IoT and Sensor Data**

- Devices send data using MQTT or HTTP protocols.
- Platforms: **AWS IoT**, **Azure IoT Hub**.

```
Smart meter ──► MQTT ──► IoT Hub ──► Kafka ──► Analytics
```

---

#### **7. Web Scraping**

- Extract data from websites automatically.
- Tools: **Scrapy**, **BeautifulSoup**, **Selenium**.

```
Website ──► Scraper ──► JSON/HTML ──► Data Lake ──► Processing
```

---

### **9.3 Data Ingestion Summary**

| Source Type | Protocol / Tool | Use Case |
|-------------|-----------------|----------|
| RDBMS | Sqoop, JDBC | Migrate existing DB to HDFS |
| Event streams | Kafka, Kinesis | Real-time logs, clicks |
| REST APIs | HTTP, Requests | Social media, weather, finance |
| Cloud storage | S3, GCS, ADLS | Bulk file access |
| Files | Flume, NiFi, FTP | Log files, batch CSVs |
| IoT devices | MQTT, IoT Hub | Sensor readings |
| Web | Scrapy, Selenium | Public web data |

---

## **Quick Revision Points**

### **Data Repositories:**

```
RDBMS        → Structured, SQL, ACID, vertical scale
NoSQL        → Flexible, horizontal scale, BASE
  Types: Key-Value, Document, Column-Family, Graph
Data Warehouse → Integrated, historical, OLAP
Data Mart    → Subset of DW for one department
Data Lake    → Raw data, schema-on-read, all types
```

### **ETL:**
```
Extract → Transform → Load
  Extract:   Pull from sources
  Transform: Clean, map, aggregate
  Load:      Write to warehouse/lake
```

### **File Formats:**

| Format | Type | Best For |
|--------|------|----------|
| CSV | Row, text | Simple exchange |
| JSON | Row, text | APIs |
| Parquet | Columnar | Analytics (Spark) |
| Avro | Row, binary | Kafka, streaming |
| ORC | Columnar | Hive |

### **Types of Data:**
- **Structured** — fixed schema, SQL (20%)
- **Semi-structured** — JSON, XML, flexible (5–10%)
- **Unstructured** — images, video, text (80%)

### **Key Players:**
- Cloud: AWS, GCP, Azure
- Open source: Apache (Hadoop, Spark, Kafka)
- BI: Tableau, Power BI

### **Service Bindings:**
- DB connectors (Sqoop), Streams (Kafka), APIs (REST), Cloud (S3), IoT (MQTT), Web scraping.

---

## **Expected Exam Questions**

> PYQs will be added after analysis — check back soon.

---

_These notes were compiled by [Deepak Modi](https://deepakmodi.dev)_  
_Last updated: May 2026_
