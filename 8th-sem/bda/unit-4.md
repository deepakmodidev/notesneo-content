---
title: "Unit 4: Big Data Integration and Processing"
description: "Big Data Processing, Data Query and Retrieval, Information Integration, Processing Pipelines, Analytical and Aggregation Operations, and Big Data Workflow Management Tools."
author: "Deepak Modi"
date: "2026-05-10"
pdfUrl: ""
---

## Syllabus:

**Big Data Integration and Processing:** Big Data Processing, Retrieving: Data Query and retrieval, Information Integration, Big Data Processing pipelines, Analytical operations, Aggregation operation, High level Operation, Tools and Systems: Big Data workflow Management.

---

## 🎯 PYQ Analysis for Unit 4

### **High Priority Topics** (15 marks questions) — ✅ Full Coverage

1. **MapReduce — Working + Word Count Program** — (2023: 15 marks) → covered in §1.5
2. **Hive — Features, Integration, Workflow, Architecture** — (2023: 15 marks) → covered in §9
3. **Pig — Architecture, Pig Latin Commands** — (2023: 15 marks) → covered in §10
4. **Real Time Analytics — technologies, working** — (2022: 15 marks) → covered in §1.6
5. **Big Data Processing Pipelines — components, working** — (2024: 15 marks) → covered in §4
6. **Hive Query Language (HQL)** — (2023: 15 marks) → covered in §9.7

### **Medium Priority Topics** (Short answers)

1. **MapReduce (definition)** — 2022 (2.5 marks) → covered in §1.5
2. **Big Data Processing Pipeline (definition)** — 2024 (2.5 marks) → covered in §4.1

> Unit 4 PYQ coverage is now comprehensive — all major 15-mark questions from 2022, 2023, and 2024 have dedicated sections.

---

## **Section 1: Big Data Processing**

> PYQ: Explain MapReduce. (2022, 2.5 marks)  
> PYQ: Explain MapReduce working. Write a program for Word Count using MapReduce. (2023, 15 marks)  
> PYQ: What is Real Time Analytics? Discuss their technologies in detail. (2022, 15 marks)

### **1.1 What is Big Data Processing?**

**Definition:**

**Big Data Processing** is the act of **collecting, transforming, analyzing, and generating insights from massive datasets** using distributed computing systems. Since Big Data cannot fit on a single machine, processing is spread across a **cluster of nodes** working in parallel.

---

### **1.2 Types of Big Data Processing**

#### **1. Batch Processing**

- Data is collected over a time period and processed **all at once**.
- High throughput, not real-time.
- Suitable for large, stable datasets.

```
Collect data → Store → Process entire dataset → Output results

Example:
  Daily sales data → Hadoop MapReduce → Revenue report
```

**Characteristics:**

| Feature | Description |
|---------|-------------|
| Latency | High (hours to days) |
| Throughput | Very high |
| Data size | Very large (entire dataset) |
| Use case | ETL jobs, billing, historical analysis |

**Tools:** Hadoop MapReduce, Apache Spark (batch mode), Apache Hive.

---

#### **2. Real-Time / Stream Processing**

- Data is processed **continuously** as it arrives, event by event.
- Very low latency (milliseconds to seconds).
- Data is never fully "at rest" — processed on the fly.

```
Data arrives → Immediate processing → Immediate output

Example:
  Credit card transaction → Fraud model → Alert (within 200ms)
```

**Characteristics:**

| Feature | Description |
|---------|-------------|
| Latency | Very low (ms–seconds) |
| Throughput | Lower than batch |
| Data size | Unbounded stream (infinite) |
| Use case | Fraud detection, live dashboards, IoT alerts |

**Tools:** Apache Kafka, Apache Flink, Apache Storm, Spark Streaming.

---

#### **3. Interactive / Ad-hoc Processing**

- User runs **on-demand queries** against stored data.
- Results expected within seconds to minutes.
- Analyst-driven exploration.

```
Analyst types query → Engine processes → Results shown in seconds

Example:
  SELECT region, SUM(sales) FROM data WHERE year=2025 GROUP BY region;
```

**Tools:** Apache Hive, Presto, Apache Impala, Google BigQuery, Spark SQL.

---

#### **4. Graph Processing**

- Specialized processing for **graph-structured data**.
- Traverses nodes and edges to find patterns.
- Example: Finding shortest path, detecting communities.

**Tools:** Apache Spark GraphX, Apache Giraph, Neo4j.

---

### **1.3 Batch vs Stream Processing**

| | Batch | Stream |
|--|-------|--------|
| **Trigger** | Scheduled or manual | Continuous |
| **Data** | Bounded (fixed size) | Unbounded (infinite) |
| **Latency** | Hours | Milliseconds |
| **Complexity** | Lower | Higher |
| **Example** | Nightly ETL | Live fraud detection |
| **Tools** | Hadoop, Hive | Kafka, Flink, Storm |

---

### **1.4 Lambda Architecture**

**Lambda Architecture** combines **batch and stream processing** to get the best of both worlds.

```
              ┌──────────────────────────────────┐
              │         Data Sources             │
              └────────────────┬─────────────────┘
                               │
               ┌───────────────┼────────────────┐
               ▼               │                ▼
       ┌──────────────┐        │      ┌──────────────────┐
       │  Batch Layer │        │      │   Speed Layer    │
       │ (Hadoop/Spark│        │      │ (Kafka + Flink)  │
       │  full data)  │        │      │ (real-time views)│
       └──────┬───────┘        │      └────────┬─────────┘
              │                │               │
              ▼                │               ▼
       ┌──────────────┐        │      ┌──────────────────┐
       │ Serving Layer│◄───────┘      │   Merge results  │
       │ (Hive/HBase) │◄──────────────┘                  │
       └──────────────┘
              │
              ▼
         Query Results
```

**Three Layers:**
- **Batch Layer** — processes all historical data, gives complete but delayed results.
- **Speed Layer** — processes only recent data, gives fast but possibly incomplete results.
- **Serving Layer** — merges batch and speed results, answers queries.

---

### **1.5 MapReduce — Detailed Working & Word Count Program**

> PYQ: Explain MapReduce. (2022, 2.5 marks)  
> PYQ: Explain MapReduce working. Write a program for Word Count using MapReduce. (2023, 15 marks)

**Definition:**

**MapReduce** is a programming model and execution framework for processing very large datasets in parallel across a distributed cluster. It splits the job into two key user-defined functions — **Map** (transforms input into intermediate key-value pairs) and **Reduce** (aggregates intermediate values per key) — while the framework itself handles parallelism, fault tolerance, and data distribution.

---

#### **Part A: MapReduce — Six (Seven) Phases of Working**

```
   Input File
       │
       ▼
┌──────────────┐
│ Input Phase  │  Record Reader → (key, value) pairs
└──────┬───────┘
       ▼
┌──────────────┐
│  Map Phase   │  user-defined map() → intermediate (k, v) pairs
└──────┬───────┘
       ▼
┌────────────────────┐
│ Intermediate Keys  │  output of all mappers
└──────┬─────────────┘
       ▼
┌──────────────────────────┐
│ Combiner (OPTIONAL)      │  local mini-reducer per mapper
└──────┬───────────────────┘
       ▼
┌──────────────────────┐
│  Shuffle & Sort      │  pull, group, sort by key
└──────┬───────────────┘
       ▼
┌──────────────┐
│   Reducer    │  user-defined reduce() → final (k, v) pairs
└──────┬───────┘
       ▼
┌──────────────┐
│ Output Phase │  Output Formatter + Record Writer → file
└──────────────┘
```

**1. Input Phase**
- A **Record Reader** translates each record in the input file into a parsed form.
- Sends the parsed records to the mapper as **key-value pairs** (e.g., `(byte_offset, line_text)`).

**2. Map Phase**
- The user-defined **`map()`** function takes a series of key-value pairs as input.
- Processes each pair and generates **zero or more output key-value pairs**.
- Runs in parallel on every chunk (input split) of the dataset.

**3. Intermediate Keys**
- The key-value pairs generated by the mapper are called **intermediate keys**.
- They are written to the local disk of each mapper node before being shuffled.

**4. Combiner (Optional)**
- A **local Reducer** that groups similar data emitted from the Map phase into identifiable sets.
- Aggregates values in a **small scope (one mapper)** — reduces the volume of data transferred during shuffle.
- **Not part of the main MapReduce algorithm** — it is an optimization step.

**5. Shuffle and Sort**
- The Reducer task **downloads** the grouped key-value pairs from all mappers to its local machine.
- The pairs are **sorted by key** into a larger data list.
- The list groups equivalent keys together so their values can be iterated easily inside the reducer.

**6. Reducer**
- Takes the grouped key-value paired data as input.
- Runs the user-defined **`reduce()`** function on each group.
- Data can be **aggregated, filtered, or combined** in many ways.
- Produces **zero or more output key-value pairs**.

**7. Output Phase**
- An **Output Formatter** translates the final key-value pairs from the Reducer.
- Writes them to a file in HDFS using a **Record Writer**.

---

#### **Part B: Word Count Program (Pseudocode)**

```
function MAP(String key, String value):
    // key is document name, value is the document content
    for each word w in value:
        emit(w, 1)

function REDUCE(String key, Iterator values):
    // key has a word name, values is a list of numbers
    sum = 0
    for each v in values:
        sum += v
    emit(key, sum)
```

**Explanation of Word Count using MapReduce:**

- **Input** → a collection of documents (`key = document name`, `value = entire document as ASCII string`).
- The **`map`** function takes each `(document-name, document)` pair, traverses the document, and emits a `(word, 1)` pair for every word it finds.
- The **middle (shuffle/sort) stage** sorts and groups these counts by word name so that all `1`s for the same word arrive at the same reducer.
- The **`reduce`** function adds up all the counts for each word and outputs a `(word, total_count)` tuple.
- **`emit`** simply returns the key-value pair — from the map function it goes to a reducer; from the reduce function it goes back to the distributed file system.

---

#### **Part C: Sample Run — "cat dog cat bird dog cat"**

**Input:**
```
Document D1 = "cat dog cat bird dog cat"
```

**Step 1: Map output (per word, emit 1):**
```
(cat, 1)  (dog, 1)  (cat, 1)  (bird, 1)  (dog, 1)  (cat, 1)
```

**Step 2: Shuffle & Sort (group by key):**
```
bird → [1]
cat  → [1, 1, 1]
dog  → [1, 1]
```

**Step 3: Reduce output (sum the list):**
```
(bird, 1)
(cat,  3)
(dog,  2)
```

**Final result:** `cat = 3`, `dog = 2`, `bird = 1`.

---

### **1.6 Real-Time Analytics — Detailed Technologies & Working**

> PYQ: What is Real Time Analytics? Discuss their technologies in detail. (2022, 15 marks)

#### **What is Real-Time Analytics?**

**Real-time analytics** in Big Data is the process of **analyzing data as soon as it is generated**. It lets users see, examine, and recognize data **as it enters a system**. Logic and mathematics are applied to that data so users can **make real-time decisions**.

- Stands at the forefront of decision-making transformation — businesses can respond **dynamically** to changing market conditions, customer behaviors, and operational challenges.
- Real-time analytics applications respond to queries within **seconds** and must handle **large data with high velocity and low reaction time**.
- Widely used in **financial databases** to notify trading decisions.
- Analytics can be **on-demand** (notifies results when the user requests) or **continuous** (renovates answers automatically on events).

**Examples of real-time customer analytics:**
1. Viewing orders as they happen for better tracing and fashion identification.
2. Continually modernizing customer activity (page views, shopping cart use) to understand user etiquette.
3. Choosing customers with advancement as they shop for items in a store, affecting real-time decisions.

---

#### **Real-Time Analytics — Working (5 Component Areas)**

```
┌────────────────────────────────────────────────────────────┐
│ 1. Data Ingestion (Kafka, Kinesis, RabbitMQ)               │
│                              ↓                              │
│ 2. Data Processing Engines (Flink, Storm, Spark Streaming) │
│                              ↓                              │
│ 3. Real-Time Querying (Druid, ClickHouse, Redshift)        │
│                              ↓                              │
│ 4. Data Storage (InfluxDB, MongoDB, Cassandra, HBase)      │
│                              ↓                              │
│ 5. Visualization & Alerts (Grafana, Kibana, Tableau)       │
└────────────────────────────────────────────────────────────┘
```

**1. Data Ingestion**
- **Continuous Data Collection** — systems continuously collect data from sensors, IoT devices, social media feeds, transaction logs, and application databases in structured, semi-structured, and unstructured formats.
- **Stream Processing** — data is ingested as **streams**, captured and processed in real-time as it arrives. Tools such as **Apache Kafka**, **RabbitMQ**, and **Amazon Kinesis** handle high-throughput streams reliably.

**2. Data Processing Engines**
- **Stream Processing Platforms** — **Apache Flink**, **Apache Storm**, and **Spark Streaming** handle continuous data flows; they perform complex event processing, transformations, aggregations, and filtering in real-time.
- **In-Memory Processing** — data is processed in **memory** rather than on disk to ensure low-latency processing; significantly speeds up processing time.
- **Parallel Processing** — distributes the workload across multiple nodes and processors to handle large volumes efficiently.

**3. Real-Time Querying**
- **Low-Latency Query Engines** — **Apache Druid**, **ClickHouse**, and **Amazon Redshift Spectrum** run queries on streaming data with minimal delay; they are optimized for low-latency execution.
- **Complex Queries** — users can perform joins, aggregations, window functions, and pattern matching on streaming data for sophisticated real-time analysis.

**4. Data Storage**
- **Time-Series Databases** — **InfluxDB**, **TimescaleDB**, and **OpenTSDB** are optimized for time-stamped data; they efficiently store and retrieve real-time data points.
- **NoSQL Databases** — **MongoDB**, **Cassandra**, and **HBase** for unstructured and semi-structured data; flexible storage that **scales horizontally**.

**5. Visualization Tools & Alerts**
- **Dashboards / BI Tools** — **Tableau**, **Power BI**, **Grafana**, and **Kibana** provide interactive and customizable visualizations to monitor and analyze data in real-time.
- **Alerts and Notifications** — configurable triggers based on **predefined conditions or thresholds**; enable proactive responses to system failures, security breaches, and significant business-metric changes.

---

#### **Real-Time Analytics Technologies (List)**

| Technology | Role |
|------------|------|
| **Streaming data processing** | Continuous data flow from one or more sources at high speed |
| **Event streaming platforms** | Process data events as they occur |
| **Apache Kafka** | Event streaming platform providing a data store for ingesting/processing streams |
| **Apache Storm** | Processes streaming data; identifies patterns and correlations |
| **Apache Flink** | Open-source technology for stream processing |
| **Apache Pinot** | Open-source technology for real-time analytics |
| **Machine Learning** | Detects trends, makes faster decisions, automates actions and recommendations |
| **Event-Driven Architecture (EDA)** | Architectural pattern letting applications respond to events in real-time |
| **Data Pipeline** | Set of steps that ingests, processes, and transforms data from various sources into an analysis-ready format |

---

## **Section 2: Data Query and Retrieval**

> PYQ: What is Hive? Explain Hive features, Hive integration and workflow and architecture in detail. (2023, 15 marks)  
> PYQ: Write short note on Hive Query Language (HQL). (2023, 15 marks)  
> PYQ: Write short note on Pig architecture and commands. (2023, 15 marks)

### **2.1 What is Data Querying?**

**Definition:**

**Data Query and Retrieval** is the process of **searching for and extracting specific data** from a storage system based on conditions or criteria.

---

### **2.2 SQL-Based Querying on Big Data**

Even though Big Data systems aren't always relational, many provide **SQL interfaces** because SQL is well-known and powerful.

**SQL on Big Data Tools:**

| Tool | SQL Interface | Underlying System |
|------|--------------|-------------------|
| **Apache Hive** | HiveQL (SQL-like) | Hadoop / HDFS |
| **Spark SQL** | Standard SQL | Apache Spark |
| **Presto** | Standard SQL | Multiple data sources |
| **Apache Impala** | Standard SQL | HDFS / HBase |
| **Google BigQuery** | Standard SQL | Google Cloud |
| **Amazon Athena** | Standard SQL | Amazon S3 |

---

### **2.3 Query Execution in Distributed Systems**

When a query runs on a Big Data cluster, it is broken into parallel tasks:

```
User Query:
  SELECT city, COUNT(*) FROM orders GROUP BY city

                    ▼

        Query Planner / Optimizer
                    │
         Split into parallel tasks
                    │
       ┌────────────┼────────────┐
       ▼            ▼            ▼
    Node 1       Node 2       Node 3
  (Process      (Process     (Process
  Shard 1)      Shard 2)     Shard 3)
       │            │            │
       └────────────┼────────────┘
                    ▼
              Merge & Aggregate
                    ▼
              Final Result
```

---

### **2.4 Indexing in Big Data**

**Indexing** speeds up data retrieval by creating a fast lookup structure.

| Index Type | Description | Example |
|------------|-------------|---------|
| **Primary Index** | On primary key | User ID lookup |
| **Secondary Index** | On non-key columns | Search by city |
| **Inverted Index** | Word → document mapping | Full-text search (Elasticsearch) |
| **Bitmap Index** | Bit vector per value | Gender, status columns |
| **Partitioned Index** | Index per partition | Date-partitioned tables |

---

### **2.5 NoSQL Query Patterns**

Different NoSQL systems have different query styles:

| System | Query Style | Example |
|--------|-------------|---------|
| **MongoDB** | Document query | `db.users.find({city:"Jaipur"})` |
| **Cassandra** | CQL (SQL-like) | `SELECT * FROM users WHERE id=001` |
| **HBase** | Row key + column scan | `get 'users', 'row001'` |
| **Redis** | GET/SET commands | `GET user:001` |
| **Neo4j** | Cypher graph query | `MATCH (u:User)-[:FRIEND]->(f) RETURN f` |

---

## **Section 3: Information Integration**

### **3.1 What is Information Integration?**

**Definition:**

**Information Integration** is the process of **combining data from multiple, heterogeneous sources** into a unified view that can be queried and analyzed as if it were a single dataset.

**Why needed?**
- Organizations have data in many places: RDBMS, cloud, files, APIs.
- Analysts need a single consistent view.
- Without integration: siloed data, inconsistent reports, duplicate effort.

---

### **3.2 Challenges of Information Integration**

| Challenge | Description |
|-----------|-------------|
| **Schema heterogeneity** | Different sources use different field names / types |
| **Semantic conflicts** | "customer" in one system = "client" in another |
| **Data format mismatch** | CSV in one, JSON in another |
| **Inconsistency** | Same customer has different names in two systems |
| **Scale** | Integrating petabytes across dozens of sources |
| **Latency** | Keeping integrated view up-to-date in real time |

---

### **3.3 Approaches to Information Integration**

#### **1. Data Warehousing (ETL-based)**
- Extract from all sources, transform to common schema, load into warehouse.
- Centralized integrated view.
- Batch, not real-time.

#### **2. Data Virtualization**
- No data is physically moved.
- A virtual layer translates queries to each source on the fly.
- Real-time but complex.

```
User Query → Virtual Layer → Query Source A + Source B → Merge → Result
```

#### **3. Data Federation**
- Similar to virtualization — a federated engine queries multiple sources simultaneously.
- Tools: **Presto**, **Apache Drill**.

#### **4. Data Lake Integration**
- Dump all raw data into a data lake.
- Use schema-on-read to integrate at query time.

---

### **3.4 Master Data Management (MDM)**

**MDM** ensures there is a **single, authoritative, consistent version** of key business data (customers, products, locations).

```
Multiple systems have "customer" data:
  CRM:     ID=C01, Name=Deepak Modi
  Billing: ID=B99, Name=D. Modi
  Website: ID=W445, Name=deepak.modi

MDM resolves these to:
  Master: ID=M001, Name=Deepak Modi (canonical)
```

---

## **Section 4: Big Data Processing Pipelines**

> PYQ: What do you mean by Big Data Processing pipeline? (2024, 2.5 marks)  
> PYQ: Describe the key components of Big Data processing pipelines. How do these components work together to ingest, process, and analyze large volumes of data? (2024, 15 marks)

### **4.1 What is a Processing Pipeline?**

**Definition:**

A **Big Data Processing Pipeline** is a series of **data processing steps** chained together, where the output of one step is the input of the next, forming an **automated data flow** from raw ingestion to final output.

```
Ingest → Validate → Clean → Transform → Analyze → Store → Serve
  │          │         │         │           │        │       │
  ▼          ▼         ▼         ▼           ▼        ▼       ▼
Kafka     Schema    Remove    Aggregate   ML Model  HDFS  Dashboard
          check     nulls     by region             /S3
```

---

### **4.2 Pipeline Stages**

| Stage | Activity | Tools |
|-------|----------|-------|
| **Ingestion** | Collect data from sources | Kafka, Flume, Sqoop |
| **Validation** | Check data quality and schema | Great Expectations |
| **Cleaning** | Remove bad/missing data | Spark, Pandas |
| **Transformation** | Reshape, enrich, aggregate | Spark, dbt, Hive |
| **Analysis** | Apply models or queries | Spark MLlib, SQL |
| **Storage** | Save results | HDFS, S3, RDBMS |
| **Serving** | Expose to end users | APIs, dashboards |

---

### **4.3 Pipeline Patterns**

#### **1. ETL Pipeline**
```
Source → Extract → Transform → Load → Warehouse
```

#### **2. Streaming Pipeline**
```
Events → Kafka → Flink/Spark Streaming → Real-time store → Dashboard
```

#### **3. ML Pipeline**
```
Raw data → Clean → Feature engineering → Train model → Evaluate → Deploy
```

#### **4. Reverse ETL Pipeline**
```
Data Warehouse → Extract → Load into → CRM / Marketing Tool
(Insights pushed back to operational systems)
```

---

### **4.4 Pipeline Design Principles**

1. **Idempotency** — running the pipeline multiple times gives the same result (no duplicates).
2. **Fault Tolerance** — pipeline recovers from failures without data loss.
3. **Modularity** — each stage is independent and replaceable.
4. **Monitoring** — every stage logs metrics and alerts on failure.
5. **Scalability** — pipeline scales with data volume automatically.

---

## **Section 5: Analytical Operations**

### **5.1 What are Analytical Operations?**

**Analytical operations** are computations performed on data to **derive insights, patterns, and knowledge**.

---

### **5.2 Types of Analytical Operations**

#### **1. Descriptive Analytics**
- Describes **what happened** in the past.
- Summary statistics: mean, median, mode, min, max.
- Visualizations: charts, dashboards.

```
"Total sales in Q1 2026 were ₹4.5 crore."
```

#### **2. Diagnostic Analytics**
- Explains **why something happened**.
- Drill-down analysis, correlation analysis.

```
"Sales dropped in March because of a supply chain disruption."
```

#### **3. Predictive Analytics**
- Predicts **what will happen** in the future.
- Uses ML models, regression, time-series forecasting.

```
"Sales in Q2 2026 are predicted to grow by 12%."
```

#### **4. Prescriptive Analytics**
- Recommends **what action to take**.
- Optimization algorithms, simulation.

```
"To maximize sales, increase inventory in Zone A by 20%."
```

**Analytics Maturity Ladder:**

```
   Prescriptive  ← What should we do?       (Most complex, most value)
       ▲
   Predictive    ← What will happen?
       ▲
   Diagnostic    ← Why did it happen?
       ▲
   Descriptive   ← What happened?            (Simplest, least value)
```

---

### **5.3 OLAP Operations**

**OLAP (Online Analytical Processing)** is a set of operations for multidimensional data analysis.

**OLAP Cube:**

```
         Time
          │
          │  ──── Sales Data ────
          │
          └─────────────────────► Region
         /
        /
     Product
```

**Key OLAP Operations:**

| Operation | Description | Example |
|-----------|-------------|---------|
| **Roll-up** | Aggregate to higher level | Day → Month → Year |
| **Drill-down** | Go to finer detail | Year → Month → Day |
| **Slice** | Fix one dimension, view others | Sales for 2025 only |
| **Dice** | Fix multiple dimensions | Sales in 2025, in North region |
| **Pivot** | Rotate the cube (change view) | Show products as rows, regions as columns |

---

## **Section 6: Aggregation Operations**

### **6.1 What is Aggregation?**

**Definition:**

**Aggregation** is the process of **combining multiple data values into a single summary value**. It reduces a large dataset to meaningful statistics.

---

### **6.2 Common Aggregation Functions**

| Function | Description | Example |
|----------|-------------|---------|
| **COUNT** | Number of records | COUNT(*) = 1000 rows |
| **SUM** | Total of values | SUM(sales) = ₹50,000 |
| **AVG** | Average value | AVG(age) = 25.3 |
| **MIN** | Minimum value | MIN(price) = ₹99 |
| **MAX** | Maximum value | MAX(price) = ₹9,999 |
| **STDDEV** | Standard deviation | Spread of salaries |
| **MEDIAN** | Middle value | Median income |
| **GROUP BY** | Aggregate per group | Sales per region |

---

### **6.3 Aggregation in Big Data Systems**

#### **MapReduce Aggregation**

```
MAP:     Emit (region, sales_amount) for each transaction
REDUCE:  For each region, SUM all sales_amounts
OUTPUT:  (North, 50000), (South, 35000), (East, 42000)
```

#### **Spark Aggregation**

```python
df.groupBy("region").agg(
    F.sum("sales").alias("total_sales"),
    F.count("order_id").alias("order_count"),
    F.avg("sales").alias("avg_sales")
)
```

#### **Hive SQL Aggregation**

```sql
SELECT region,
       SUM(sales)   AS total_sales,
       COUNT(*)     AS num_orders,
       AVG(sales)   AS avg_order
FROM sales_table
GROUP BY region
ORDER BY total_sales DESC;
```

---

### **6.4 Aggregation Challenges in Big Data**

| Challenge | Solution |
|-----------|----------|
| **Data skew** | One key has far more records than others → slow reducer | Salting / repartitioning |
| **Memory overflow** | Aggregation result too large for RAM | External sorting, spill to disk |
| **Approximate aggregation** | Exact count of billions is slow | HyperLogLog for COUNT DISTINCT |
| **Streaming aggregation** | Continuous data, can't wait for all | Windowed aggregation |

---

## **Section 7: High-Level Operations**

### **7.1 What are High-Level Operations?**

High-level operations in Big Data refer to **complex, multi-step data transformations and analyses** that go beyond simple CRUD or aggregation. They are often expressed in declarative languages and executed as optimized distributed jobs.

---

### **7.2 Key High-Level Operations**

#### **1. Join Operations**

Combining data from two or more datasets.

| Join Type | Description |
|-----------|-------------|
| **Inner Join** | Only matching records from both datasets |
| **Left Join** | All records from left + matching from right |
| **Right Join** | All records from right + matching from left |
| **Full Outer Join** | All records from both, nulls where no match |
| **Cross Join** | Every combination (Cartesian product) |

**Distributed Join Strategies:**

- **Broadcast Join** — small dataset sent to all nodes (avoids shuffle).
- **Sort-Merge Join** — both datasets sorted, then merged (large datasets).
- **Hash Join** — one dataset hashed, other probes the hash table.

---

#### **2. Sorting and Ordering**

- Distributed sorting requires **shuffle** — moving data between nodes.
- **Total Order Sorting** — globally sorted across all nodes (expensive).
- **Partial Sort** — sorted within each partition (cheaper).

---

#### **3. Sampling**

- Taking a representative **subset** of data for faster analysis or testing.

```
Types:
  Random Sampling      → Pick N% of rows randomly
  Stratified Sampling  → Maintain class proportions
  Reservoir Sampling   → Sample from a stream of unknown size
```

---

#### **4. Filtering and Projection**

- **Filtering (WHERE)** — keep only rows matching a condition.
- **Projection (SELECT columns)** — keep only needed columns.

In columnar formats (Parquet), projection pushdown means only the required columns are read from disk — huge performance win.

---

#### **5. Deduplication**

- Remove duplicate records from a large dataset.
- Challenging at scale — cannot load everything into memory.

```
Techniques:
  Exact dedup     → Hash each row, remove identical hashes
  Fuzzy dedup     → Use similarity (e.g., "Deepak" = "Deepk")
  Bloom filters   → Probabilistic set membership check
```

---

#### **6. Windowing / Sliding Window Operations**

Used in **stream processing** to analyze data within a time window.

```
Tumbling Window:   Fixed, non-overlapping windows
  [0–10s] [10–20s] [20–30s]

Sliding Window:    Overlapping windows
  [0–10s] [5–15s] [10–20s]

Session Window:    Based on activity gaps
  (group events close in time, split by inactivity)
```

**Example:**
```
Count fraud alerts in the last 5 minutes, updated every 1 minute.
→ Sliding window: size=5min, slide=1min
```

---

## **Section 8: Big Data Workflow Management**

### **8.1 What is Workflow Management?**

**Definition:**

**Big Data Workflow Management** is the **orchestration and scheduling of complex, multi-step data processing jobs** to ensure they run in the correct order, handle failures gracefully, and complete reliably.

A **workflow** (also called a **DAG — Directed Acyclic Graph**) defines the sequence and dependencies of tasks.

```
DAG Example:
  Extract_Data → Clean_Data → Transform → Train_Model → Evaluate → Deploy
       │               │            │
       └───────────────┴────────────┘
          (no cycles allowed)
```

---

### **8.2 Why Workflow Management is Needed**

- Big Data pipelines have **many dependent steps** — step 3 can't run until step 2 finishes.
- Jobs run on a **schedule** (daily, hourly).
- **Failures** need to be detected and retried automatically.
- Teams need **visibility** into what is running, what failed, and why.

---

### **8.3 Apache Airflow**

**Apache Airflow** is the most popular open-source workflow orchestration tool for data pipelines.

**Key Concepts:**

| Concept | Description |
|---------|-------------|
| **DAG** | Directed Acyclic Graph — the workflow definition |
| **Task** | One unit of work (e.g., run a Spark job) |
| **Operator** | Template for a task type (PythonOperator, BashOperator, SparkOperator) |
| **Scheduler** | Triggers DAGs on schedule |
| **Executor** | Runs the actual tasks (LocalExecutor, CeleryExecutor) |
| **Web UI** | Dashboard to monitor DAGs and task status |

**Example DAG (simplified):**

```python
with DAG("daily_etl", schedule_interval="@daily") as dag:
    extract = PythonOperator(task_id="extract", python_callable=run_extract)
    transform = SparkSubmitOperator(task_id="transform", application="transform.py")
    load = PythonOperator(task_id="load", python_callable=run_load)

    extract >> transform >> load   # define order
```

---

### **8.4 Apache Oozie**

**Apache Oozie** is a workflow scheduler specifically for **Hadoop jobs**.

- Defines workflows in **XML**.
- Supports MapReduce, Hive, Pig, Sqoop jobs.
- Coordinator jobs for time-based scheduling.

---

### **8.5 Other Workflow Tools**

| Tool | Type | Key Feature |
|------|------|-------------|
| **Apache Airflow** | General orchestration | Python DAGs, rich UI |
| **Apache Oozie** | Hadoop-specific | XML workflows, Hadoop-native |
| **Apache NiFi** | Data flow management | Drag-and-drop pipeline builder |
| **Prefect** | Modern orchestration | Cloud-native, Python |
| **Dagster** | Data orchestration | Strong typing, testing |
| **Luigi** | Batch orchestration | Simple Python tasks |
| **AWS Step Functions** | Cloud workflow | Serverless state machine |
| **dbt** | Transformation | SQL-based transform DAGs |

---

### **8.6 Monitoring and Observability**

A workflow system must also support **monitoring**:

| Metric | What to track |
|--------|--------------|
| **Job success rate** | % of pipelines completing without failure |
| **Latency** | How long each stage takes |
| **Data volume** | Records processed per job |
| **Queue depth** | Kafka lag — how far behind consumers are |
| **Resource usage** | CPU, memory, disk on cluster nodes |
| **Data quality** | % of records passing validation |

**Tools:** Grafana, Prometheus, Apache Ambari, AWS CloudWatch, Datadog.

---

## **Section 9: Apache Hive — Data Warehouse on Hadoop**

> PYQ: What is Hive? Explain Hive features, Hive integration and workflow and architecture in detail. (2023, 15 marks)  
> PYQ: Write short note on Hive Query Language (HQL). (2023, 15 marks)

### **9.1 What is Hive?**

- **Apache Hive** is a **data warehouse infrastructure tool** to process **structured data** in Hadoop.
- It resides on **top of Hadoop** to summarize Big Data and make querying and analyzing easy.
- Originally developed by **Facebook**, later open-sourced by the Apache Software Foundation as **Apache Hive**.
- Used by companies like **Amazon** (in **Amazon Elastic MapReduce**).

---

### **9.2 Features of Hive**

1. **Indexes** — provides indexes (including **bitmap indexes** since v0.10) to accelerate queries.
2. **Metadata in RDBMS** — stores metadata in a relational database, which reduces the time required for semantic checks during query execution.
3. **Built-in User-Defined Functions (UDFs)** — comes with UDFs to manipulate strings, dates, and data-mining tools; the UDF set is **extensible** to handle cases not covered by predefined functions.
4. **Algorithms for compressed data** — supports operations on compressed data using **DEFLATE, BWT, snappy**, etc.
5. **Schema in DB, Data in HDFS** — stores schemas in a database and processes the actual data into HDFS.
6. **OLAP-oriented** — built primarily for **Online Analytical Processing (OLAP)** workloads.
7. **Query Language** — provides **Hive Query Language (HVL / HiveQL)** — a SQL-like language for querying.

---

### **9.3 Hive Integration in Big Data**

"Hive integration" refers to using **Apache Hive** — a data warehouse system built on Hadoop — to **query and analyze large datasets** stored in distributed file systems.

- Lets users **easily access and manipulate massive amounts of data** using familiar **SQL-like syntax (HiveQL)** instead of writing complex MapReduce programs.
- Critical for **Big Data analysis** inside the Hadoop ecosystem because it lowers the barrier between data analysts (who know SQL) and the underlying distributed engine.

---

### **9.4 Workflow of Hive**

- Hive operates in **two modes**:
  - **Interactive mode** → commands go **directly to the Hive shell**.
  - **Non-interactive mode** → executes code in **console mode** (script execution).
- Data is divided into **partitions**, which in turn split into **buckets**.
- Execution plans are produced based on **aggregation patterns and data skew**.
- Easily processes large-scale information and provides **rich user interfaces** (Web UI, CLI).

---

### **9.5 Architecture of Hive**

```
┌────────────────────────────────────────────────────────────┐
│   USER INTERFACES                                          │
│   Web UI  |  Hive Command Line  |  HD Insight (Windows)    │
└──────────────────────┬─────────────────────────────────────┘
                       ▼
       ┌───────────────────────────────┐
       │ Meta Store ◄──► HiveQL Process│
       │                Engine         │
       └───────────────┬───────────────┘
                       ▼
              ┌─────────────────┐
              │ Execution Engine│
              └────────┬────────┘
                       ▼
                ┌─────────────┐
                │  MAP REDUCE │
                └──────┬──────┘
                       ▼
            ┌──────────────────────┐
            │ HDFS  /  HBASE       │
            │ (Data Storage)       │
            └──────────────────────┘
```

**Architectural Units:**

| Unit Name | Operation |
|-----------|-----------|
| **User Interface** | Hive Web UI, Hive CLI, Hive HD Insight — create the interaction between user and HDFS |
| **Meta Store** | Stores schema / metadata of tables and databases, columns and their data types, and HDFS mapping |
| **Hive QL Process Engine** | Performs SQL-like querying on the schema info in the Metastore; replaces the traditional approach of writing MapReduce programs in Java |
| **Execution Engine** | Conjunction of the HiveQL Process Engine and MapReduce; processes the query and generates results similar to MapReduce |
| **HDFS or HBASE** | Underlying data storage techniques used by Hive |

---

### **9.6 Data Flow Steps — Hive Query Execution (9 Steps)**

```
 UI → Driver → Compiler → Meta Store → Compiler → Driver
                                                    │
                                                    ▼
                          Execution Engine ──► MapReduce/HDFS
                                                    │
                                                    ▼
                                                 Results
```

1. **Execute the Query** from the UI (CLI / Web UI / JDBC).
2. **Get a plan** from the driver — the driver creates a task DAG (Directed Acyclic Graph) of stages.
3. **Get metadata request** sent from the compiler to the Meta Store.
4. **Sent metadata** is returned from the Meta Store to the compiler.
5. **Sending the plan back** to the driver after compilation and optimization.
6. **Execute the plan** in the execution engine.
7. **Fetching results** for the appropriate user query.
8. **Sending results** bi-directionally between the execution engine and the driver / UI.
9. The **execution engine** performs processing in **HDFS with MapReduce** and fetches results from data nodes created by the **job tracker** — acting as the connector between **Hive and Hadoop**.

---

### **9.7 Hive Query Language (HQL)**

**HiveQL** is a **SQL-like query language** used by Hive to process and analyze **structured data stored in a Metastore**.

- **SELECT statement** — retrieves data from a table.
- **WHERE clause** — filters data using a condition and gives a **finite result**; works similar to a condition in SQL; built-in operators and functions are used to generate an expression that fulfils the condition.

**Syntax:**

```sql
SELECT [ALL | DISTINCT] select_expr, select_expr, ...
FROM table_reference
[WHERE where_condition]
[GROUP BY col_list]
[HAVING having_condition]
[CLUSTER BY col_list | [DISTRIBUTE BY col_list] [SORT BY col_list]]
[LIMIT number];
```

**Common HQL Clauses:**

| Clause | Purpose |
|--------|---------|
| `SELECT` | Pick columns to project |
| `FROM` | Source table |
| `WHERE` | Row-level filter |
| `GROUP BY` | Group rows for aggregation |
| `HAVING` | Filter on aggregated groups |
| `CLUSTER BY` | Distribute + sort by same column |
| `DISTRIBUTE BY` | Route rows to reducers |
| `SORT BY` | Sort within each reducer |
| `LIMIT` | Restrict number of rows returned |

---

## **Section 10: Apache Pig — Data Flow Language**

> PYQ: Write short note on Pig architecture and commands. (2023, 15 marks)

### **10.1 What is Pig?**

- **Apache Pig** is a **high-level data processing language** used to analyze data in Hadoop.
- The language used is **Pig Latin** — provides rich **data types and operators** for various operations.
- A programmer writes a **Pig script** in Pig Latin and executes it using one of the execution mechanisms: **Grunt Shell**, **UDFs**, or **Embedded** mode.
- Scripts go through a series of **transformations** applied by the Pig framework to produce the desired output.
- **Internally**, Apache Pig converts these scripts into a **series of MapReduce jobs** that run on Hadoop.

---

### **10.2 Apache Pig Architecture**

```
                Pig Latin Scripts
                        │
                        ▼
   ┌──────────── Apache Pig ─────────────┐
   │   Grunt Shell   |   Pig Server      │
   │                                      │
   │            ┌─────────────┐           │
   │            │   Parser    │           │
   │            └──────┬──────┘           │
   │                   ▼                  │
   │            ┌─────────────┐           │
   │            │  Optimizer  │           │
   │            └──────┬──────┘           │
   │                   ▼                  │
   │            ┌─────────────┐           │
   │            │  Compiler   │           │
   │            └──────┬──────┘           │
   │                   ▼                  │
   │         ┌────────────────────┐       │
   │         │  Execution Engine  │       │
   │         └─────────┬──────────┘       │
   └───────────────────┼──────────────────┘
                       ▼
                  MapReduce
                       │
                       ▼
                    Hadoop
                       │
                       ▼
                     HDFS
```

**Components:**

1. **Parser** — handles Pig scripts; performs **syntax checking, type checking**, and other validations. The output is a **DAG (Directed Acyclic Graph)** representing the Pig Latin statements and logical operators (nodes = logical operators, edges = data flows).
2. **Optimizer** — receives the logical plan (DAG) and carries out **logical optimizations** like **projection** and **pushdown** to reduce processed data.
3. **Compiler** — compiles the optimized logical plan into a **series of MapReduce jobs**.
4. **Execution Engine** — submits the MapReduce jobs to Hadoop in **sorted order**; the jobs execute on Hadoop to produce the desired results.

---

### **10.3 Basic Pig Commands**

1. **`fs -ls`** — lists all files in HDFS.
   ```
   grunt> fs -ls
   ```
2. **`clear`** — clears the interactive Grunt shell.
   ```
   grunt> clear
   ```
3. **`history`** — shows previously executed commands.
   ```
   grunt> history
   ```
4. **Reading data** — load data into a relation:
   ```
   grunt> college_students = LOAD 'hdfs://localhost:9000/pig_data/college_data.txt'
          USING PigStorage(',')
          as (id:int, firstname:chararray, lastname:chararray, phone:chararray, city:chararray);
   ```
   - `PigStorage()` loads and stores data as **structured text files**.
5. **Storing data** — write a relation back to HDFS:
   ```
   grunt> STORE college_students INTO 'hdfs://localhost:9000/pig_Output/' USING PigStorage(',');
   ```
6. **`Dump`** — displays results on the screen; useful in debugging.
   ```
   grunt> Dump college_students;
   ```
7. **`Describe`** — views a relation's schema.
   ```
   grunt> describe college_students;
   ```
8. **`Explain`** — reviews the logical, physical, and MapReduce execution plans.
   ```
   grunt> explain college_students;
   ```
9. **`Illustrate`** — step-by-step execution of statements.
   ```
   grunt> illustrate college_students;
   ```

---

### **10.4 Intermediate Pig Commands**

1. **Group** — groups data with the same key.
   ```
   grunt> group_data = GROUP college_students by firstname;
   ```
2. **Cogroup** — like `Group`, but works with **more than one relation**.
3. **Join** — combines two or more relations; can be **self-join**, **inner-join**, or **outer-join**.
   ```
   grunt> customers3 = JOIN customers1 BY id, customers2 BY id;
   ```
4. **Cross** — Cartesian product of two or more relations.
   ```
   grunt> cross_data = CROSS customers, orders;
   ```
5. **Union** — merges two relations; the columns and domains of both relations must be **identical**.
   ```
   grunt> student = UNION student1, student2;
   ```

---

### **10.5 Advanced Pig Commands**

1. **Filter** — filters tuples based on a condition.
   ```
   grunt> filter_data = FILTER college_students BY city == 'Chennai';
   ```
2. **Distinct** — removes redundant tuples.
   ```
   grunt> distinct_data = DISTINCT college_students;
   ```
3. **Foreach** — generates data transformation based on column data.
   ```
   grunt> foreach_data = FOREACH student_details GENERATE id, age, city;
   ```
4. **Order by** — displays the result in **sorted order**.
   ```
   grunt> order_by_data = ORDER college_students BY age DESC;
   ```
5. **Limit** — gets a **limited number of tuples** from a relation.
   ```
   grunt> limit_data = LIMIT student_details 4;
   ```

---

## **Quick Revision Points**

### **Processing Types:**

| Type | Latency | Tools |
|------|---------|-------|
| Batch | Hours | Hadoop, Hive, Spark batch |
| Stream | ms–seconds | Kafka, Flink, Spark Streaming |
| Interactive | Seconds | Presto, Spark SQL, BigQuery |

### **Lambda Architecture:**
- Batch Layer (historical) + Speed Layer (real-time) + Serving Layer (merge).

### **OLAP Operations:**
- Roll-up, Drill-down, Slice, Dice, Pivot.

### **Analytics Types:**
- Descriptive → Diagnostic → Predictive → Prescriptive.

### **Aggregation Functions:**
- COUNT, SUM, AVG, MIN, MAX, STDDEV, GROUP BY.

### **High-Level Operations:**
- Join, Sort, Sample, Filter, Project, Deduplicate, Window.

### **Windowing:**
- Tumbling (non-overlapping), Sliding (overlapping), Session (activity-based).

### **Workflow Management:**
- DAG = task dependency graph.
- Apache Airflow = most popular orchestrator.
- Oozie = Hadoop-specific.
- NiFi = drag-and-drop flow management.

### **MapReduce Phases:**
- **7 phases:** Input → Map → Intermediate Keys → Combiner (optional) → Shuffle & Sort → Reduce → Output.
- **Combiner** = local mini-reducer per mapper; reduces shuffle volume; optional.
- **Shuffle & Sort** = group all intermediate values by key before reducer.

### **Word Count Algorithm:**
- `MAP(doc_name, doc)` → for each word `w` in doc: `emit(w, 1)`.
- `REDUCE(word, values)` → `sum = Σ values`; `emit(word, sum)`.
- Sample: `"cat dog cat bird dog cat"` → `(cat,3), (dog,2), (bird,1)`.

### **Real-Time Analytics — 5 Component Areas:**
1. Data Ingestion (Kafka, Kinesis, RabbitMQ)
2. Data Processing Engines (Flink, Storm, Spark Streaming)
3. Real-Time Querying (Druid, ClickHouse, Redshift)
4. Data Storage (InfluxDB, MongoDB, Cassandra, HBase)
5. Visualization & Alerts (Grafana, Kibana, Tableau, Power BI)

### **Real-Time Analytics Technologies:**
- Streaming data processing, Event streaming platforms, Apache Kafka, Apache Storm, Apache Flink, Apache Pinot, Machine Learning, Event-Driven Architecture (EDA), Data Pipeline.

### **Apache Hive — Key Points:**
- Data warehouse on top of Hadoop for **structured** data; originally by Facebook.
- **7 features:** Indexes, RDBMS metadata, UDFs, compression algorithms (DEFLATE/BWT/snappy), schema in DB, OLAP-built, HiveQL.
- **Architecture units:** User Interface → Meta Store + HiveQL Process Engine → Execution Engine → MapReduce → HDFS/HBase.
- **Workflow:** interactive vs non-interactive mode; data → partitions → buckets.
- **9 data-flow steps** for query execution.

### **HiveQL (HQL):**
- SQL-like; `SELECT … FROM … WHERE … GROUP BY … HAVING … CLUSTER BY / DISTRIBUTE BY / SORT BY … LIMIT`.

### **Apache Pig — Key Points:**
- High-level **data flow language**; written in **Pig Latin**; internally converted to MapReduce jobs.
- **Architecture:** Parser → Optimizer → Compiler → Execution Engine → MapReduce → Hadoop → HDFS.
- **Basic commands:** `fs -ls`, `clear`, `history`, `LOAD`, `STORE`, `Dump`, `Describe`, `Explain`, `Illustrate`.
- **Intermediate:** `Group`, `Cogroup`, `Join`, `Cross`, `Union`.
- **Advanced:** `Filter`, `Distinct`, `Foreach`, `Order by`, `Limit`.

---

## **Expected Exam Questions**

### **15-Mark Questions:**

1. Explain MapReduce working. Write a program for Word Count using MapReduce. *(2023)*
2. What is Hive? Explain Hive features, Hive integration and workflow and architecture in detail. *(2023)*
3. Write short note on Hive Query Language (HQL). *(2023)*
4. Write short note on Pig architecture and commands. *(2023)*
5. What is Real Time Analytics? Discuss their technologies in detail. *(2022)*
6. Describe the key components of Big Data processing pipelines. How do these components work together to ingest, process, and analyze large volumes of data? *(2024)*

### **Short Answer Questions (2.5 marks):**

1. Explain MapReduce. *(2022)*
2. What do you mean by Big Data Processing pipeline? *(2024)*

---

_These notes were compiled by [Deepak Modi](https://deepakmodi.dev)_  
_Last updated: May 2026_
