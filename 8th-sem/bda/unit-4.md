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

> PYQs will be added after analysis — check back soon.

---

## **Section 1: Big Data Processing**

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

## **Section 2: Data Query and Retrieval**

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

---

## **Expected Exam Questions**

> PYQs will be added after analysis — check back soon.

---

_These notes were compiled by [Deepak Modi](https://deepakmodi.dev)_  
_Last updated: May 2026_
