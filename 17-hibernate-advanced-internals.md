# Chapter 12.1 - Hibernate Advanced Internals (Architect Edition)

## 1. Hibernate Architecture Deep Dive

```text
Application
  ↓
Spring Data JPA
  ↓
EntityManager
  ↓
Hibernate Session
  ↓
Persistence Context
  ↓
Action Queue
  ↓
JDBC
  ↓
Database
```

## 2. Session Internals

Session is Hibernate's core object.

Responsibilities:
- Persistence Context management
- Dirty Checking
- Entity Lifecycle
- Transaction Synchronization
- SQL execution

## 3. Stateful vs Stateless Session

### Stateful Session
- First-level cache
- Dirty checking
- Lifecycle tracking

### Stateless Session
- No Persistence Context
- No dirty checking
- Better for bulk processing

## 4. Persistence Context Deep Dive

Tracks every managed entity.

States:
- Managed
- Detached
- Removed

## 5. Action Queue

Hibernate does not execute SQL immediately.

Queue types:
- InsertAction
- UpdateAction
- DeleteAction
- CollectionAction

SQL executes during Flush.

## 6. Flush Internals

Flush synchronizes memory state with database.

### Flush Modes
- AUTO
- COMMIT
- MANUAL
- ALWAYS

## 7. Dirty Checking Algorithm

Workflow:

```text
Snapshot
   ↓
Compare Changes
   ↓
Generate UPDATE SQL
```

Cost increases with large Persistence Context.

## 8. Snapshot Mechanism

Hibernate stores original values.

During flush:

```text
Current State
vs
Snapshot State
```

## 9. Bytecode Enhancement

Optimizations:
- Faster dirty checking
- Lazy attribute loading
- Reduced memory usage

## 10. Hibernate Proxy Internals

Lazy loading relies on proxies.

```java
HibernateProxy
```

Proxy initializes real object on demand.

## 11. PersistentCollection Internals

Implementations:
- PersistentBag
- PersistentList
- PersistentSet
- PersistentMap

## 12. Bag vs List vs Set

Bag:
- Fast insert
- Allows duplicates

Set:
- Unique items
- Extra hashing cost

List:
- Ordering support

## 13. Fetch Strategies

### Lazy Fetch
Default recommendation.

### Eager Fetch
Can create over-fetching.

## 14. Batch Fetching

```properties
hibernate.default_batch_fetch_size=50
```

Reduces N+1 queries.

## 15. Subselect Fetching

Loads associations using one additional query.

Useful for read-heavy systems.

## 16. Fetch Profiles

Dynamic fetch strategy selection.

## 17. Query Compilation Pipeline

```text
JPQL
 ↓
HQL Parser
 ↓
SQL AST
 ↓
SQL
```

## 18. Query Plan Cache

Caches parsed queries.

Benefit:
- Less parsing overhead
- Better throughput

## 19. Statistics API

Enable monitoring:

```properties
hibernate.generate_statistics=true
```

Metrics:
- Query Count
- Cache Hits
- Entity Loads
- Flush Count

## 20. JDBC Connection Management

Lifecycle:

```text
Acquire
 ↓
Use
 ↓
Release
```

## 21. Connection Pool Integration

Common pools:
- HikariCP
- Tomcat Pool
- DBCP

## 22. Transaction Synchronization

Hibernate synchronizes Session with transaction lifecycle.

## 23. JTA vs Resource Local

Resource Local:
- Single database

JTA:
- Distributed transactions

## 24. Open Session In View (OSIV)

Keeps session open during request.

Pros:
- Avoid LazyInitializationException

Cons:
- Hidden SQL
- Performance risks

## 25. Multi-Tenancy

Strategies:
- Database per tenant
- Schema per tenant
- Shared database

## 26. Event System

Events:
- PreInsert
- PostInsert
- PreUpdate
- PostUpdate
- Delete

## 27. Entity Listeners

Examples:

```java
@PrePersist
@PostLoad
```

## 28. AttributeConverter

Convert custom types.

```java
AttributeConverter
```

## 29. Custom Hibernate Types

Use UserType for advanced mapping.

## 30. Naming Strategies

- ImplicitNamingStrategy
- PhysicalNamingStrategy

## 31. Second Level Cache Internals

Scopes:
- Entity Cache
- Collection Cache
- NaturalId Cache

## 32. Query Cache

Caches query results.

Use carefully.

## 33. Natural ID Cache

Optimizes lookup by business key.

## 34. Bulk Operations

```java
update User u set ...
```

Bypasses Persistence Context.

## 35. Write Behind Strategy

Hibernate batches SQL execution.

Improves performance.

## 36. Persistence Context Memory Leaks

Causes:
- Huge batches
- Long transactions
- Large managed entity count

Solution:

```java
flush();
clear();
```

## 37. Long Transaction Problems

Effects:
- Lock contention
- Memory growth
- Slow commits

## 38. Advanced Performance Tuning

Recommendations:
- DTO Projection
- Batch Writes
- Fetch Join
- Proper Indexes
- Limit Persistence Context Size

## 39. Real Production Incidents

### Incident 1
N+1 generated thousands of queries.

### Incident 2
OSIV created hidden SQL traffic.

### Incident 3
Large batch import caused OutOfMemoryError.

## 40. Senior Architect Interview Questions

1. Session vs EntityManager?
2. Explain Action Queue.
3. How Dirty Checking works?
4. What is Bytecode Enhancement?
5. Hibernate Proxy internals?
6. Batch Fetching vs Fetch Join?
7. Query Plan Cache?
8. OSIV pros and cons?
9. How Second-Level Cache works?
10. Why bulk updates bypass Persistence Context?
11. How prevent memory leaks?
12. Multi-tenancy strategies?
13. Event system internals?
14. Connection management lifecycle?
15. Hibernate performance tuning checklist?

## Chapter Summary

✅ Session Internals
✅ Action Queue
✅ Flush Modes
✅ Dirty Checking
✅ Snapshot Mechanism
✅ Bytecode Enhancement
✅ Hibernate Proxies
✅ Persistent Collections
✅ Batch Fetching
✅ Subselect Fetching
✅ Query Plan Cache
✅ Statistics API
✅ Connection Management
✅ OSIV
✅ Multi-Tenancy
✅ Event System
✅ Custom Types
✅ Second Level Cache
✅ Query Cache
✅ Bulk Operations
✅ Performance Tuning
✅ Production Incidents
✅ Architect Interview Questions
