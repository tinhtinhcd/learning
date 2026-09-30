# Chapter 8 - Java Memory Model

## Learning Objectives

After completing this chapter, you will be able to:

- Understand the Java Memory Model (JMM)
- Explain Visibility, Atomicity, and Ordering
- Understand CPU Cache behavior
- Master Happens-Before rules
- Understand volatile internals
- Understand Memory Barriers
- Understand CAS internals
- Understand Unsafe and VarHandle
- Understand False Sharing and Cache Lines
- Diagnose concurrency bugs
- Answer Senior Java and JVM interview questions

---

# 1. Why Java Memory Model Exists

Without a memory model:

- CPUs may reorder instructions
- Compilers may optimize aggressively
- Threads may observe stale values

JMM defines rules for:

```text
Visibility
Atomicity
Ordering
```

---

# 2. Main Problems in Concurrent Programming

## Visibility Problem

Thread A updates a variable.

Thread B cannot immediately see the update.

## Race Condition

Multiple threads update shared state concurrently.

## Reordering

Instructions execute in a different order.

---

# 3. Visibility

Visibility means:

```text
One thread sees changes made by another thread.
```

Example:

```java
boolean running = true;
```

Worker thread may never observe updates.

---

# 4. Atomicity

Atomic operation:

```text
Cannot be interrupted midway.
```

Example:

```java
counter++;
```

Not atomic.

Internally:

```text
Read
Modify
Write
```

---

# 5. Ordering

Code:

```java
a = 1;
b = 2;
```

May execute as:

```java
b = 2;
a = 1;
```

if no ordering guarantee exists.

---

# 6. Main Memory vs Working Memory

JMM abstraction:

```text
Main Memory
      ↑↓
Thread Working Memory
```

Threads operate on local copies.

Not directly on shared memory.

---

# 7. CPU Cache

Modern CPUs contain:

```text
L1 Cache
L2 Cache
L3 Cache
RAM
```

Cache improves performance.

Can introduce visibility issues.

---

# 8. Cache Coherence

Problem:

```text
CPU1 Cache != CPU2 Cache
```

Solution:

```text
Cache Coherence Protocol
```

Example:

```text
MESI Protocol
```

---

# 9. MESI Protocol

States:

```text
Modified
Exclusive
Shared
Invalid
```

Guarantees cache consistency.

---

# 10. Happens-Before Introduction

Most important JMM concept.

Definition:

```text
If A happens-before B,
then effects of A are visible to B.
```

---

# 11. Program Order Rule

Inside same thread:

```java
a = 1;
b = 2;
```

Program order establishes happens-before.

---

# 12. Monitor Lock Rule

```java
synchronized(lock)
```

Unlock operation happens-before subsequent lock operation.

---

# 13. Volatile Rule

```java
volatile boolean running;
```

Write happens-before subsequent read.

---

# 14. Thread Start Rule

```java
thread.start();
```

Actions before start() become visible to the new thread.

---

# 15. Thread Join Rule

```java
thread.join();
```

After join completes:

all actions of worker thread are visible.

---

# 16. synchronized Deep Dive

Provides:

✅ Visibility

✅ Atomicity

✅ Ordering

---

# 17. volatile Deep Dive

Provides:

✅ Visibility

✅ Ordering

❌ Atomicity

Example:

```java
volatile int counter;
```

Still unsafe:

```java
counter++;
```

---

# 18. Memory Barriers

JVM inserts barriers around volatile operations.

Types:

```text
Load Barrier
Store Barrier
LoadLoad
LoadStore
StoreStore
StoreLoad
```

---

# 19. Store Buffer

CPU optimization.

Writes temporarily stay in store buffer.

May delay visibility.

Memory barriers solve this.

---

# 20. Instruction Reordering

Allowed when correctness is preserved.

May occur:

```text
Compiler
JIT
CPU
```

---

# 21. Double Checked Locking

Classic singleton pattern.

```java
private static volatile Singleton instance;
```

volatile is required.

Reason:

Prevent unsafe publication.

---

# 22. CAS (Compare And Swap)

Pseudo logic:

```text
If current == expected
    update
Else
    retry
```

Foundation of lock-free programming.

---

# 23. CAS Advantages

✅ Non-blocking

✅ High performance

✅ Better scalability

---

# 24. CAS Limitations

ABA Problem

High contention retries.

CPU spinning.

---

# 25. Atomic Classes

Examples:

```java
AtomicInteger
AtomicLong
AtomicReference
```

Built using CAS.

---

# 26. Unsafe API

Internal JVM API.

Example:

```java
sun.misc.Unsafe
```

Capabilities:

- Direct memory access
- CAS operations
- Low-level concurrency

---

# 27. VarHandle

Modern replacement for Unsafe.

Introduced in Java 9.

Benefits:

- Supported API
- Better safety

---

# 28. False Sharing

Two variables:

```text
Independent
```

But stored on same cache line.

Causes unnecessary cache invalidation.

---

# 29. Cache Line

Typical size:

```text
64 Bytes
```

False sharing occurs at cache line level.

---

# 30. @Contended

Annotation used to reduce false sharing.

```java
@Contended
```

Adds memory padding.

---

# 31. Safe Publication

Ways:

```java
final
volatile
static initialization
synchronized
```

---

# 32. Immutable Objects

Example:

```java
String
```

Benefits:

- Naturally thread-safe
- Easier reasoning

---

# 33. Escape Analysis and JMM

JIT determines whether object escapes thread scope.

Possible optimizations:

```text
Stack Allocation
Lock Elimination
```

---

# 34. Real Production Bugs

## Visibility Bug

Thread never sees stop signal.

Cause:

Missing volatile.

---

## Race Condition

Incorrect counter values.

Cause:

Missing synchronization.

---

## Unsafe Publication

Partially initialized object visible.

---

# 35. JMM Interview Questions

1. What is JMM?
2. Visibility vs Atomicity?
3. What problems does volatile solve?
4. Why volatile cannot guarantee atomicity?
5. What are Happens-Before rules?
6. What is instruction reordering?
7. What are memory barriers?
8. How CAS works?
9. What is ABA problem?
10. Unsafe vs VarHandle?
11. What is false sharing?
12. What does @Contended do?
13. Why is double-checked locking dangerous without volatile?
14. What is safe publication?
15. How CPU cache affects concurrency?

---

# Production Troubleshooting Checklist

✅ Check data races
✅ Check shared mutable state
✅ Verify volatile usage
✅ Verify synchronization
✅ Inspect thread dumps
✅ Check false sharing hotspots
✅ Benchmark under concurrency
✅ Monitor CPU cache effects

---

# Chapter Summary

✅ Java Memory Model
✅ Visibility
✅ Atomicity
✅ Ordering
✅ CPU Cache
✅ Cache Coherence
✅ MESI
✅ Happens-Before
✅ synchronized
✅ volatile
✅ Memory Barriers
✅ Reordering
✅ CAS
✅ Atomic Classes
✅ Unsafe
✅ VarHandle
✅ False Sharing
✅ Cache Line
✅ @Contended
✅ Safe Publication
✅ Immutable Objects
✅ Production Case Studies
✅ Senior Interview Questions
