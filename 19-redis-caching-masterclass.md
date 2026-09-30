# Chapter 19 - Redis Caching Masterclass

## Learning Objectives

- Understand Redis internals
- Design high-performance caching systems
- Implement distributed locking with Redis
- Solve cache consistency challenges
- Design scalable Redis clusters
- Integrate Redis with Spring Boot
- Prepare for Senior Java and Tech Lead interviews

---

# Part I. Redis Fundamentals

## What is Redis?

Redis (Remote Dictionary Server) is an in-memory data store used for caching, messaging, rate limiting, distributed locking, and real-time workloads.

Characteristics:
- In-memory
- Extremely fast
- Rich data structures
- Optional persistence
- High availability support

## Redis Data Structures

### String
```redis
SET user:1 "Tinh"
```

### Hash
```redis
HSET user:1 name Tinh
```

### List
```redis
LPUSH queue task1
```

### Set
```redis
SADD tags java spring
```

### Sorted Set
```redis
ZADD ranking 100 user1
```

### Stream
```redis
XADD orders *
```

---

# Part II. Redis Internals

## Event Loop Architecture

Redis uses:

```text
Single Thread
+
Non Blocking I/O
```

Benefits:
- No lock contention
- Predictable latency
- High throughput

## Memory Management

Topics:
- Memory fragmentation
- Eviction policies
- Max memory configuration

## Persistence

### RDB
- Snapshot based
- Small files
- Fast recovery

### AOF
- Append only file
- Better durability
- Larger storage

### Hybrid Persistence
Recommended for modern deployments.

---

# Part III. Cache Patterns

## Cache Aside

```text
Application
 ↓
Redis
 ↓ miss
Database
```

Most popular strategy.

## Read Through

Cache automatically loads data.

## Write Through

Cache and database updated together.

## Write Behind

Database updates asynchronously.

---

# Part IV. Cache Problems

## Cache Penetration

Solutions:
- Bloom Filter
- Cache null values

## Cache Breakdown

Solutions:
- Mutex lock
- Hot key protection

## Cache Avalanche

Solutions:
- Random TTL
- Multi-layer cache

## Cache Consistency

Strategies:
- Double delete
- Event driven invalidation

---

# Part V. Distributed Locking

## Redis Lock

```redis
SET lock_key value NX PX 30000
```

## Lock Release

Release only by lock owner.

## RedLock

Distributed lock across multiple Redis nodes.

---

# Part VI. Messaging

## Pub/Sub

```text
Publisher
 ↓
Redis
 ↓
Subscribers
```

## Redis Streams

Features:
- Consumer groups
- Replay support
- Acknowledgements

---

# Part VII. Rate Limiting

## Fixed Window
## Sliding Window
## Token Bucket
## Leaky Bucket

Common API protection techniques.

---

# Part VIII. Session Management

## Shared Session Storage

```text
App-1
App-2
App-3
 ↓
Redis
```

Enables horizontal scaling.

---

# Part IX. Redis Cluster

## Master Replica
## Sentinel
## Redis Cluster

Redis Cluster:
- High availability
- Sharding
- 16384 hash slots

---

# Part X. Spring Boot Integration

## Spring Data Redis

```xml
<dependency>
  <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

## RedisTemplate

```java
redisTemplate.opsForValue()
             .set("user:1", user);
```

## Spring Cache

```java
@Cacheable(value = "users", key = "#id")
public User getUser(Long id) {}
```

## Cache Evict

```java
@CacheEvict(value = "users", key = "#id")
```

---

# Part XI. Distributed Lock with Java

## Basic Lock

```java
Boolean locked = redisTemplate.opsForValue()
    .setIfAbsent(lockKey, lockValue, Duration.ofSeconds(30));
```

## Redisson

```java
RLock lock = redissonClient.getLock("inventory-lock");
lock.lock();
try {
    processOrder();
} finally {
    lock.unlock();
}
```

---

# Part XII. Real World Use Cases

## Inventory Reservation

Prevent overselling.

## Rate Limiting

Protect public APIs.

## Idempotency

Avoid duplicate payment processing.

## Leaderboard

```java
redisTemplate.opsForZSet()
    .add("leaderboard", playerId, score);
```

## Session Sharing

Support stateless deployments.

---

# Part XIII. Performance Engineering

## Hot Key Problem

Solutions:
- Replicated cache
- Local cache

## Big Key Problem

Solutions:
- Split structures
- Pagination

## Connection Pooling

Libraries:
- Lettuce
- Jedis

---

# Part XIV. Security & Monitoring

## Security

- Authentication
- TLS
- Network isolation

## Metrics

Monitor:
- Memory
- Ops/sec
- Evictions
- Cache Hit Ratio

## Observability

```text
Redis Exporter
 ↓
Prometheus
 ↓
Grafana
```

---

# Part XV. Interview Questions

1. Why is Redis fast?
2. Redis vs Memcached?
3. AOF vs RDB?
4. Cache Aside vs Write Through?
5. Cache Avalanche?
6. Cache Breakdown?
7. Distributed lock design?
8. Sentinel vs Cluster?
9. Hot Key problem?
10. Redis Streams vs Kafka?

---

# Tech Lead Checklist

✅ Redis Internals
✅ Persistence
✅ Cache Patterns
✅ Cache Consistency
✅ Distributed Locking
✅ Redisson
✅ Spring Cache
✅ RedisTemplate
✅ Rate Limiting
✅ Session Sharing
✅ Redis Cluster
✅ Monitoring
✅ Production Use Cases
✅ Interview Preparation
