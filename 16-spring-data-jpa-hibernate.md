# Chapter 16 - Spring Data JPA Hibernate

## Learning Objectives

After completing this chapter, you will be able to:

- Understand JPA architecture
- Understand Hibernate internals
- Master Entity Lifecycle
- Understand Persistence Context
- Understand Dirty Checking
- Understand Transaction behavior
- Solve N+1 problems
- Use Fetch Join and Entity Graphs
- Understand JPA Caching
- Use Optimistic and Pessimistic Locking
- Optimize database performance
- Troubleshoot production issues

---

# 1. What is JPA?

JPA (Jakarta Persistence API) is a specification.

It defines:

- Entity Mapping
- Persistence Context
- Transactions
- Query APIs

JPA is not an implementation.

---

# 2. What is Hibernate?

Hibernate is the most popular JPA implementation.

Responsibilities:

- SQL Generation
- Entity Management
- Caching
- Dirty Checking

---

# 3. Spring Data JPA

Built on top of JPA.

Benefits:

- Repository abstraction
- Query generation
- Pagination
- Auditing

---

# 4. Entity

```java
@Entity
class User {}
```

Represents a database table.

---

# 5. Entity Lifecycle

```text
Transient
 ↓
Managed
 ↓
Detached
 ↓
Removed
```

Critical interview topic.

---

# 6. Persistence Context

Acts as:

```text
First-Level Cache
```

Managed by EntityManager.

---

# 7. EntityManager

Core JPA interface.

Responsibilities:

- Persist
- Merge
- Remove
- Find

---

# 8. First-Level Cache

Scope:

```text
Persistence Context
```

Enabled automatically.

---

# 9. Second-Level Cache

Shared across sessions.

Providers:

- Ehcache
- Hazelcast
- Infinispan

---

# 10. Dirty Checking

Hibernate automatically detects changes.

```java
user.setName("John");
```

No explicit update required.

---

# 11. Flush

Synchronizes:

```text
Persistence Context
 ↓
Database
```

---

# 12. Flush vs Commit

Flush:

```text
Generate SQL
```

Commit:

```text
Persist Transaction
```

---

# 13. Repository Pattern

```java
JpaRepository<User, Long>
```

Provides CRUD operations.

---

# 14. Query Methods

Example:

```java
findByEmail()
```

Generated automatically.

---

# 15. JPQL

Object-oriented query language.

```java
SELECT u FROM User u
```

---

# 16. Native Queries

```java
@Query(nativeQuery = true)
```

Direct SQL execution.

---

# 17. Pagination

```java
Pageable
```

Essential for large datasets.

---

# 18. Sorting

```java
Sort.by("name")
```

---

# 19. Entity Relationships

```java
@OneToOne
@OneToMany
@ManyToOne
@ManyToMany
```

---

# 20. Lazy Loading

Default for collections.

Benefits:

- Reduced queries
- Better performance

---

# 21. Eager Loading

Loads related data immediately.

Risk:

```text
Over-fetching
```

---

# 22. N+1 Problem

Example:

```text
1 query for users
N queries for orders
```

Major production issue.

---

# 23. Fetch Join

Solution:

```java
JOIN FETCH
```

Reduces query count.

---

# 24. Entity Graph

Alternative to Fetch Join.

Provides dynamic fetch plans.

---

# 25. Cascade Types

```java
PERSIST
MERGE
REMOVE
ALL
```

---

# 26. Orphan Removal

```java
orphanRemoval = true
```

Automatically removes child entities.

---

# 27. Transactions

```java
@Transactional
```

Foundation of data consistency.

---

# 28. Isolation Levels

```text
READ_UNCOMMITTED
READ_COMMITTED
REPEATABLE_READ
SERIALIZABLE
```

---

# 29. Optimistic Locking

```java
@Version
```

Uses version column.

---

# 30. Pessimistic Locking

Database lock.

```java
LockModeType.PESSIMISTIC_WRITE
```

---

# 31. Batch Processing

```properties
hibernate.jdbc.batch_size=50
```

Improves insertion performance.

---

# 32. JDBC Batching

Reduces:

- Network calls
- SQL execution overhead

---

# 33. Hibernate Internals

Workflow:

```text
Entity
 ↓
Persistence Context
 ↓
Dirty Checking
 ↓
SQL Generation
 ↓
Database
```

---

# 34. SQL Generation

Hibernate converts entity changes into SQL automatically.

---

# 35. Auditing

```java
@CreatedDate
@LastModifiedDate
```

---

# 36. Common Production Problems

## N+1 Query

Most common Hibernate issue.

---

## LazyInitializationException

Accessing lazy relations outside transaction.

---

## Slow Queries

Check:

- Missing indexes
- Large joins
- N+1 problem

---

## Memory Growth

Large persistence contexts.

---

# 37. Performance Optimization

- Use pagination
- Prefer DTO projections
- Avoid unnecessary eager loading
- Use batch processing
- Monitor SQL execution
- Index correctly

---

# 38. DTO Projection

Avoid loading full entities.

Improves performance.

---

# 39. Database Indexing

Critical for query optimization.

Monitor:

```text
Execution Plans
```

---

# 40. Senior Interview Questions

1. JPA vs Hibernate?
2. Entity lifecycle?
3. Persistence Context?
4. Dirty Checking?
5. Flush vs Commit?
6. Lazy vs Eager?
7. N+1 Problem?
8. Fetch Join vs Entity Graph?
9. First-Level vs Second-Level Cache?
10. Optimistic vs Pessimistic Locking?
11. Why LazyInitializationException happens?
12. How @Transactional works?
13. How batch processing works?
14. How Hibernate generates SQL?
15. Production tuning strategies?

---

# Chapter Summary

✅ JPA Architecture
✅ Hibernate Internals
✅ Spring Data JPA
✅ Entity Lifecycle
✅ Persistence Context
✅ EntityManager
✅ Dirty Checking
✅ Flush & Commit
✅ Repository Pattern
✅ JPQL
✅ Native Queries
✅ Relationships
✅ Lazy Loading
✅ Eager Loading
✅ N+1 Problem
✅ Fetch Join
✅ Entity Graph
✅ Transactions
✅ Locking
✅ Caching
✅ Batch Processing
✅ DTO Projection
✅ Performance Optimization
✅ Production Troubleshooting
✅ Senior Interview Questions
