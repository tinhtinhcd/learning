# Chapter 16 - Kafka & Event Streaming (Principal Engineer Edition)

## Learning Objectives

After completing this chapter, you will understand:

- Kafka architecture and internals
- Log-based storage design
- Producer internals
- Consumer internals
- Partitioning strategy
- Replication protocol
- ISR mechanism
- KRaft architecture
- Kafka transactions
- Exactly Once Semantics
- Kafka Connect
- Schema Registry
- CDC with Debezium
- Event Streaming patterns
- Large-scale production architectures
- Principal Engineer interview topics

---

# 1. Why Event Streaming?

Traditional systems:

```text
Request -> Response
```

Event streaming:

```text
Producer -> Event Log -> Consumer
```

Benefits:

- Decoupling
- Scalability
- Replayability
- Real-time processing

---

# 2. Kafka Architecture

```text
Producer
  ↓
Broker
  ↓
Topic
  ↓
Partition
  ↓
Consumer Group
```

---

# 3. Broker

Responsibilities:

- Store data
- Replicate data
- Serve reads/writes

---

# 4. Topic

Logical event stream.

Examples:

```text
orders
payments
shipments
```

---

# 5. Partition

Unit of scalability.

Benefits:

- Parallel processing
- Horizontal scaling

---

# 6. Ordering Guarantees

Kafka guarantees ordering:

```text
Within Partition Only
```

---

# 7. Message Key

Example:

```java
orderId
```

Same key -> Same partition.

---

# 8. Kafka Storage Engine

Kafka is fundamentally:

```text
Distributed Append-Only Log
```

---

# 9. Log Segment

Partition contains:

```text
segment-1.log
segment-2.log
segment-3.log
```

---

# 10. Offset

Unique position inside partition.

Example:

```text
Offset 125
```

---

# 11. Producer Internals

Workflow:

```text
Serialize
 ↓
Partition
 ↓
Batch
 ↓
Compress
 ↓
Send
```

---

# 12. Producer Acknowledgements

acks=0
acks=1
acks=all

---

# 13. Idempotent Producer

Guarantees:

```text
No Duplicate Writes
```

---

# 14. Producer Batching

Configuration:

```properties
batch.size
linger.ms
```

Improves throughput.

---

# 15. Compression

Options:

- gzip
- snappy
- lz4
- zstd

---

# 16. Consumer Internals

Workflow:

```text
Poll
 ↓
Process
 ↓
Commit Offset
```

---

# 17. Consumer Group

Multiple consumers share partitions.

Provides scalability.

---

# 18. Consumer Rebalancing

Occurs when:

- Consumer joins
- Consumer leaves
- Partition changes

---

# 19. Offset Management

Kafka tracks:

```text
Consumer Progress
```

---

# 20. At-Most-Once

Possible data loss.

No duplicates.

---

# 21. At-Least-Once

No loss.

Duplicates possible.

---

# 22. Exactly Once Semantics

No loss.

No duplicates.

Most complex mode.

---

# 23. Replication

Purpose:

- High availability
- Fault tolerance

---

# 24. Leader Replica

Handles reads and writes.

---

# 25. Follower Replica

Replicates leader data.

---

# 26. ISR (In Sync Replicas)

Replicas fully caught up.

Critical Kafka concept.

---

# 27. Leader Election

Triggered when leader fails.

ISR member becomes new leader.

---

# 28. KRaft Architecture

Modern Kafka metadata management.

Replaces ZooKeeper.

---

# 29. Kafka Transactions

Used for:

```text
Atomic Multi-partition Writes
```

---

# 30. Event Design Principles

Event should be:

- Immutable
- Self-contained
- Versioned

---

# 31. Event Versioning

Strategies:

- Backward compatible
- Forward compatible

---

# 32. Schema Registry

Stores event schemas.

Benefits:

- Governance
- Compatibility checking

---

# 33. Serialization Formats

- JSON
- Avro
- Protobuf

---

# 34. Kafka Connect

Framework for integration.

Examples:

- Database
- S3
- Elasticsearch

---

# 35. CDC (Change Data Capture)

Capture database changes.

---

# 36. Debezium

Most common CDC platform.

Flow:

```text
MySQL
 ↓
Binlog
 ↓
Debezium
 ↓
Kafka
```

---

# 37. Event Streaming Patterns

- Event Notification
- Event Carried State Transfer
- Event Sourcing
- CQRS

---

# 38. Event Sourcing

Stores events instead of current state.

Benefits:

- Auditability
- Replay capability

---

# 39. CQRS + Kafka

Separate:

```text
Write Side
Read Side
```

---

# 40. Outbox Pattern

Recommended for reliable publishing.

---

# 41. Streaming Analytics

Tools:

- Kafka Streams
- Flink
- Spark Streaming

---

# 42. Kafka Streams

Embedded stream processing library.

---

# 43. Production Monitoring

Metrics:

- Consumer Lag
- Throughput
- Latency
- ISR Count

---

# 44. Common Production Issues

## Consumer Lag

Causes:

- Slow processing
- Insufficient consumers

## Rebalance Storm

Too many rebalances.

## Disk Pressure

Large retention configuration.

## Uneven Partitions

Poor key distribution.

---

# 45. LinkedIn Case Study

Kafka was created at LinkedIn.

Primary use:

- Activity streams
- Analytics pipeline

---

# 46. Uber Case Study

Kafka handles:

- Ride events
- Driver tracking
- Payment events

Millions of events per second.

---

# 47. Netflix Case Study

Kafka used for:

- Operational events
- Monitoring
- User activities

---

# 48. E-Commerce Event Architecture

```text
Order Service
 ↓
Kafka
 ↓
Inventory Service
 ↓
Payment Service
 ↓
Shipping Service
 ↓
Notification Service
```

Patterns:

- Saga
- Outbox
- CQRS

---

# 49. Principal Engineer Interview Questions

1. Kafka vs RabbitMQ?
2. Explain ISR.
3. Why partitions matter?
4. How ordering works?
5. Exactly-once internals?
6. Idempotent producer?
7. Kafka transactions?
8. ZooKeeper vs KRaft?
9. Event sourcing benefits?
10. Debezium architecture?
11. Schema Registry purpose?
12. Consumer lag troubleshooting?
13. Rebalancing internals?
14. Partition sizing strategy?
15. Design real-time order processing platform.

---

# Chapter Summary

✅ Kafka Architecture
✅ Broker
✅ Topics
✅ Partitions
✅ Storage Engine
✅ Offsets
✅ Producers
✅ Consumers
✅ Consumer Groups
✅ Replication
✅ ISR
✅ Leader Election
✅ KRaft
✅ Transactions
✅ Exactly Once Semantics
✅ Schema Registry
✅ Avro
✅ Protobuf
✅ Kafka Connect
✅ Debezium
✅ Event Streaming Patterns
✅ Kafka Streams
✅ Production Operations
✅ Principal Interview Questions
