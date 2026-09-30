# Chapter 38 - Data Architecture for Architects (Complete Edition)

## Learning Objectives

After completing this chapter, you will:

- Understand enterprise data architecture principles
- Master OLTP, OLAP, Data Warehouse, Data Lake and Lakehouse concepts
- Design batch and streaming data platforms
- Understand CDC, ETL, ELT and event-driven data pipelines
- Apply Data Governance, Data Mesh and MDM practices
- Build AI-ready data platforms
- Make architecture decisions as a Solution Architect or Principal Engineer

---

# Part I. Data Architecture Fundamentals

Data Architecture defines how data is created, collected, processed, stored, secured, governed and consumed.

Key Goals:

- Scalability
- Reliability
- Security
- Data Quality
- Compliance
- Analytics Readiness
- AI Readiness

Architecture Layers:

```text
Data Sources
      ↓
Ingestion
      ↓
Storage
      ↓
Processing
      ↓
Serving
      ↓
Consumption
```

---

# Part II. Data Lifecycle

Stages:

1. Create
2. Collect
3. Store
4. Process
5. Analyze
6. Archive
7. Delete

Architect Responsibilities:

- Data retention strategy
- Compliance requirements
- Cost management
- Access policies

---

# Part III. OLTP vs OLAP

## OLTP

Characteristics:

- Low latency
- High concurrency
- Frequent updates
- ACID transactions

Examples:

- Online banking
- E-commerce orders
- Payment processing

Databases:

- PostgreSQL
- MySQL
- Oracle

## OLAP

Characteristics:

- Large scans
- Aggregations
- Historical analysis
- Reporting

Examples:

- BI dashboards
- Sales analytics
- Executive reports

Platforms:

- Snowflake
- Redshift
- BigQuery

---

# Part IV. Dimensional Modeling

## Fact Tables

Store business events.

Examples:

- Sales Facts
- Payment Facts

## Dimension Tables

Store descriptive attributes.

Examples:

- Customer
- Product
- Time

## Star Schema

```text
Dimension
    ↓
Fact
 ↑  ↑
Dimension
```

## Snowflake Schema

Normalized dimensions.

Tradeoff:

- Less duplication
- More joins

---

# Part V. Data Warehouse

Purpose:

- Analytics
- Reporting
- Historical trends

Characteristics:

- Structured data
- Curated datasets
- High query performance

Benefits:

- Single source of truth
- Business metrics consistency

Challenges:

- Data movement
- Data freshness

---

# Part VI. Data Lake

Stores raw data.

Supported Formats:

- CSV
- JSON
- Parquet
- Avro
- Images
- Video

Advantages:

- Cheap storage
- Flexible ingestion
- Massive scale

Challenges:

- Data swamp risk
- Governance requirements

---

# Part VII. Data Lakehouse

Combines:

```text
Data Warehouse
+
Data Lake
```

Technologies:

- Delta Lake
- Apache Iceberg
- Apache Hudi

Benefits:

- Open formats
- ACID support
- Unified architecture

---

# Part VIII. ETL and ELT

## ETL

Extract
→ Transform
→ Load

Traditional warehouse approach.

## ELT

Extract
→ Load
→ Transform

Modern cloud approach.

Benefits:

- Faster ingestion
- Better scalability

---

# Part IX. Change Data Capture (CDC)

Purpose:

Track database changes.

Methods:

- Triggers
- Timestamp Columns
- Transaction Logs

Tools:

- Debezium
- Oracle GoldenGate

Architecture:

```text
Database
    ↓
CDC
    ↓
Kafka
    ↓
Consumers
```

---

# Part X. Batch Processing

Characteristics:

- Scheduled jobs
- Large datasets
- Cost efficient

Examples:

- Daily reports
- Billing processing

---

# Part XI. Stream Processing

Characteristics:

- Near real-time
- Continuous processing

Frameworks:

- Kafka Streams
- Apache Flink
- Spark Streaming

Examples:

- Fraud detection
- Real-time recommendations

---

# Part XII. Data Pipeline Architecture

Components:

```text
Source
 ↓
Ingestion
 ↓
Transformation
 ↓
Storage
 ↓
Serving
```

Qualities:

- Reliability
- Observability
- Recoverability

---

# Part XIII. Data Quality

Dimensions:

- Accuracy
- Completeness
- Consistency
- Timeliness
- Uniqueness

Quality Checks:

- Schema Validation
- Business Rules
- Duplication Detection

---

# Part XIV. Data Governance

Objectives:

- Compliance
- Security
- Accountability

Components:

- Policies
- Standards
- Stewardship
- Metadata Management

---

# Part XV. Master Data Management (MDM)

Purpose:

Create a single source of truth.

Examples:

- Customer Master
- Product Master
- Supplier Master

Benefits:

- Consistency
- Better reporting

---

# Part XVI. Metadata Management

Types:

- Technical Metadata
- Business Metadata
- Operational Metadata

Examples:

- Table definitions
- Data owner
- Pipeline runtime

---

# Part XVII. Data Catalog

Purpose:

- Discoverability
- Governance
- Lineage tracking

Examples:

- Collibra
- DataHub
- AWS Glue Catalog

---

# Part XVIII. Data Lineage

Tracks data movement.

Example:

```text
Database
 ↓
Kafka
 ↓
Data Lake
 ↓
Dashboard
```

Benefits:

- Impact analysis
- Compliance
- Troubleshooting

---

# Part XIX. Data Mesh

Principles:

- Domain Ownership
- Data as Product
- Self-Service Platform
- Federated Governance

Benefits:

- Scalability of organization
- Faster delivery

Challenges:

- Governance complexity

---

# Part XX. Medallion Architecture

```text
Bronze
 ↓
Silver
 ↓
Gold
```

Bronze:
Raw data

Silver:
Cleaned data

Gold:
Business data

---

# Part XXI. Data Security

Practices:

- Encryption at Rest
- Encryption in Transit
- Tokenization
- Data Masking
- Access Control

---

# Part XXII. Data Privacy

Common Requirements:

- GDPR
- Data Retention
- Right to Erasure

Architect Concerns:

- Sensitive data classification
- Auditability

---

# Part XXIII. Analytics Architecture

Components:

- Warehouse
- Semantic Layer
- BI Layer

Tools:

- Power BI
- Tableau
- Looker

---

# Part XXIV. Event-Driven Data Architecture

```text
Applications
      ↓
Kafka
      ↓
Consumers
      ↓
Analytics Platform
```

Benefits:

- Near real-time insights
- Decoupled systems

---

# Part XXV. Data Architecture for AI and LLMs

Requirements:

- High quality data
- Metadata
- Governance
- Lineage

Supports:

- Machine Learning
- RAG
- AI Agents

---

# Part XXVI. Data Platform Architecture

Typical Components:

- Ingestion Layer
- Storage Layer
- Processing Layer
- Governance Layer
- Consumption Layer

---

# Part XXVII. Real-World Architectures

## E-Commerce

Orders → CDC → Kafka → Data Lake → Warehouse → Power BI

## Banking

Core Banking → Warehouse → Regulatory Reports

## IoT

Devices → Kafka → Data Lake → Analytics

---

# Part XXVIII. Common Anti-Patterns

❌ Data Silos

❌ Duplicate Pipelines

❌ No Governance

❌ No Ownership

❌ Data Swamp

❌ Poor Quality Controls

---

# Part XXIX. Architecture Decision Framework

Questions:

1. Real-time or batch?
2. Structured or unstructured?
3. Regulatory requirements?
4. Retention requirements?
5. Analytics requirements?
6. AI requirements?

---

# Part XXX. Interview Questions

1. OLTP vs OLAP?
2. Warehouse vs Lake?
3. Why Lakehouse?
4. ETL vs ELT?
5. Explain CDC.
6. What is Data Mesh?
7. What is MDM?
8. Explain Medallion Architecture.
9. How would you design a company data platform?
10. How do you support AI workloads?

---

# Architect Checklist

✅ OLTP
✅ OLAP
✅ Dimensional Modeling
✅ Data Warehouse
✅ Data Lake
✅ Lakehouse
✅ ETL
✅ ELT
✅ CDC
✅ Batch Processing
✅ Stream Processing
✅ Data Quality
✅ Governance
✅ MDM
✅ Metadata Management
✅ Data Catalog
✅ Data Lineage
✅ Data Mesh
✅ Medallion Architecture
✅ Analytics Platforms
✅ AI Data Platforms
✅ Enterprise Data Architecture
