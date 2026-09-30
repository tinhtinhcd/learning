# Chapter 13 - Spring Transaction Management (Complete Architect Edition)

## Learning Objectives

After completing this chapter, you will be able to:

- Understand Spring transaction architecture
- Master transaction propagation
- Understand isolation levels deeply
- Understand TransactionSynchronizationManager
- Understand Hibernate transaction integration
- Understand distributed transactions
- Compare 2PC and Saga patterns
- Implement Outbox Pattern
- Diagnose deadlocks and transaction issues
- Optimize transaction performance
- Answer Senior and Architect interview questions

---

# 1. Why Transactions Matter

Transactions guarantee:

```text
Atomicity
Consistency
Isolation
Durability
```

Known as ACID.

---

# 2. ACID Properties

## Atomicity

All operations succeed or fail together.

## Consistency

Database remains valid.

## Isolation

Concurrent transactions do not interfere.

## Durability

Committed data persists.

---

# 3. Spring Transaction Architecture

```text
Business Method
       ↓
AOP Proxy
       ↓
Transaction Manager
       ↓
Database
```

@Transactional is implemented using Spring AOP.

---

# 4. PlatformTransactionManager

Core Spring transaction abstraction.

Implementations:

- DataSourceTransactionManager
- JpaTransactionManager
- JtaTransactionManager

---

# 5. @Transactional

```java
@Transactional
public void transfer() {
}
```

Declarative transaction management.

---

# 6. Transaction Lifecycle

```text
Begin
 ↓
Business Logic
 ↓
Commit
```

On exception:

```text
Rollback
```

---

# 7. Transaction Proxy Flow

```text
Client
 ↓
Proxy
 ↓
Begin Transaction
 ↓
Method Execution
 ↓
Commit/Rollback
```

---

# 8. Rollback Rules

Default behavior:

```text
Rollback RuntimeException
```

Checked exceptions do not automatically rollback.

---

# 9. Custom Rollback Rules

```java
@Transactional(
 rollbackFor = Exception.class
)
```

---

# 10. Propagation Overview

Defines transaction behavior between methods.

Interview favorite topic.

---

# 11. REQUIRED

Default propagation.

```text
Join Existing
or
Create New
```

---

# 12. REQUIRES_NEW

Always creates new transaction.

Suspends current transaction.

---

# 13. SUPPORTS

Uses existing transaction if available.

Otherwise runs without transaction.

---

# 14. NOT_SUPPORTED

Suspends transaction.

Runs non-transactionally.

---

# 15. MANDATORY

Requires existing transaction.

Throws exception otherwise.

---

# 16. NEVER

Must not run within transaction.

---

# 17. NESTED

Creates savepoint.

Allows partial rollback.

---

# 18. Propagation Comparison

```text
REQUIRED
REQUIRES_NEW
SUPPORTS
MANDATORY
NESTED
```

Frequently asked in interviews.

---

# 19. Isolation Levels

Protect against data anomalies.

---

# 20. READ_UNCOMMITTED

Allows dirty reads.

Fastest.

Least safe.

---

# 21. READ_COMMITTED

Prevents dirty reads.

Default in many databases.

---

# 22. REPEATABLE_READ

Prevents non-repeatable reads.

Default in MySQL.

---

# 23. SERIALIZABLE

Highest isolation.

Most expensive.

---

# 24. Transaction Anomalies

- Dirty Read
- Non-repeatable Read
- Phantom Read

---

# 25. TransactionSynchronizationManager

Central Spring transaction context.

Stores:

- Resources
- Connections
- Current transaction metadata

---

# 26. ThreadLocal Usage

Spring transaction context relies heavily on:

```java
ThreadLocal
```

---

# 27. Hibernate Integration

```text
@Transactional
 ↓
JpaTransactionManager
 ↓
EntityManager
 ↓
Hibernate Session
```

---

# 28. Flush During Transaction

Hibernate may flush before:

- Commit
- Query execution

---

# 29. Read Only Transactions

```java
@Transactional(readOnly = true)
```

Benefits:

- Optimization
- Reduced overhead

---

# 30. Transaction Timeout

```java
@Transactional(timeout = 30)
```

Prevents long-running operations.

---

# 31. Deadlocks

Occurs when:

```text
Txn A waits for B
Txn B waits for A
```

---

# 32. Deadlock Prevention

Strategies:

- Consistent lock order
- Small transactions
- Proper indexing

---

# 33. Optimistic Locking

```java
@Version
```

Detects concurrent updates.

---

# 34. Pessimistic Locking

Database lock acquired immediately.

Suitable for high-contention scenarios.

---

# 35. Distributed Transactions

Multiple systems involved.

Example:

```text
Order Service
Payment Service
Inventory Service
```

---

# 36. Two-Phase Commit (2PC)

Flow:

```text
Prepare
 ↓
Commit
```

Pros:
- Strong consistency

Cons:
- Slow
- Complex

---

# 37. XA Transactions

Standard for distributed transactions.

Managed by transaction coordinator.

---

# 38. Saga Pattern

Alternative to 2PC.

Sequence of local transactions.

Uses compensation logic.

---

# 39. Choreography Saga

Services communicate using events.

No central coordinator.

---

# 40. Orchestration Saga

Central coordinator controls workflow.

---

# 41. Outbox Pattern

Goal:

```text
Database Changes
+
Message Publishing
```

Without inconsistency.

---

# 42. Eventual Consistency

Distributed systems commonly use:

```text
Eventually Consistent
```

Instead of strong consistency.

---

# 43. Transaction Performance Tuning

Recommendations:

- Keep transactions short
- Avoid remote calls inside transaction
- Minimize locks
- Batch updates

---

# 44. Common Production Issues

## Transaction Not Working

Causes:
- Self invocation
- Proxy bypass

---

## Unexpected Rollback

Causes:
- Hidden exception
- Nested transaction behavior

---

## Connection Pool Exhaustion

Cause:
- Long transactions

---

## Deadlock

Cause:
- Lock ordering issue

---

# 45. Real Production Cases

### Banking Transfer

Requires ACID guarantees.

### E-Commerce Order Flow

Uses Saga + Outbox.

### Reporting Service

Uses read-only transactions.

---

# 46. Senior Architect Interview Questions

1. How does @Transactional work internally?
2. Transaction Manager vs EntityManager?
3. REQUIRED vs REQUIRES_NEW?
4. NESTED vs REQUIRES_NEW?
5. Isolation levels comparison?
6. What is TransactionSynchronizationManager?
7. Why ThreadLocal is used?
8. How rollback works?
9. How deadlocks occur?
10. Optimistic vs Pessimistic Locking?
11. What is 2PC?
12. What is XA?
13. Saga vs 2PC?
14. Outbox Pattern benefits?
15. How tune transaction performance?

---

# Chapter Summary

✅ ACID
✅ Transaction Architecture
✅ TransactionManager
✅ @Transactional
✅ Rollback Rules
✅ Propagation Modes
✅ Isolation Levels
✅ TransactionSynchronizationManager
✅ ThreadLocal
✅ Hibernate Integration
✅ Deadlocks
✅ Optimistic Locking
✅ Pessimistic Locking
✅ Distributed Transactions
✅ XA
✅ 2PC
✅ Saga Pattern
✅ Outbox Pattern
✅ Eventual Consistency
✅ Production Troubleshooting
✅ Architect Interview Questions
