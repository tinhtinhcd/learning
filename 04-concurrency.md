# Chapter 4 - Concurrency

## Learning Objectives

Master Java concurrency from mid-level to senior architect level:

- Thread lifecycle and scheduling
- Java Memory Model (JMM) fundamentals
- Race conditions and thread safety
- synchronized, volatile, Atomic APIs
- CAS (Compare-And-Swap)
- ReentrantLock, ReadWriteLock, StampedLock
- ExecutorService and ThreadPoolExecutor internals
- CompletableFuture advanced patterns
- ForkJoinPool and Work Stealing
- Concurrent collections internals
- Producer-Consumer pattern
- Deadlock, Livelock, Starvation
- False Sharing and CPU Cache effects
- Virtual Threads
- Concurrency troubleshooting

---

# 1. Concurrency vs Parallelism

Concurrency:

```text
Multiple tasks make progress.
```

Parallelism:

```text
Multiple tasks execute simultaneously.
```

Example:

```text
1 CPU Core -> Concurrency
8 CPU Cores -> Parallelism
```

---

# 2. Process vs Thread

Process:

- Separate memory
- Heavyweight

Thread:

- Shared heap
- Lightweight

```text
JVM Process
 ├─ Main Thread
 ├─ GC Thread
 ├─ HTTP Worker
 └─ Scheduler Thread
```

---

# 3. Thread Lifecycle

```text
NEW
RUNNABLE
BLOCKED
WAITING
TIMED_WAITING
TERMINATED
```

Understand differences between:

- BLOCKED
- WAITING
- TIMED_WAITING

Interview favorite topic.

---

# 4. Race Condition

Example:

```java
counter++;
```

Actually:

```text
Read
Modify
Write
```

Two threads may overwrite each other.

---

# 5. Thread Safety

Thread-safe examples:

```java
AtomicInteger
ConcurrentHashMap
```

Not thread-safe:

```java
HashMap
ArrayList
StringBuilder
```

Thread-safe:

```java
StringBuffer
Vector
Hashtable
```

---

# 6. synchronized Deep Dive

Levels:

```java
synchronized method
```

```java
synchronized static method
```

```java
synchronized block
```

Lock granularity:

```java
synchronized(this)
```

Prefer smallest possible lock scope.

---

# 7. Java Memory Model (JMM) Introduction

Three concepts:

```text
Visibility
Atomicity
Ordering
```

Without synchronization:

Thread A writes value.

Thread B may not see it.

---

# 8. Happens-Before Rules

Critical senior interview topic.

Examples:

```text
Thread.start()
```

Happens-before new thread execution.

```text
unlock()
```

Happens-before

```text
subsequent lock()
```

Volatile write:

```text
happens-before
```

volatile read.

---

# 9. volatile Deep Dive

Guarantees:

✅ Visibility

❌ Atomicity

Good example:

```java
volatile boolean running;
```

Bad:

```java
volatile int counter;
counter++;
```

Still unsafe.

---

# 10. CAS (Compare And Swap)

Foundation for lock-free programming.

Pseudo logic:

```text
If current == expected
    update
Else
    retry
```

Used by:

```java
AtomicInteger
ConcurrentHashMap
```

Advantages:

- No blocking
- High performance

Disadvantage:

- Spin retries

---

# 11. Atomic Classes

```java
AtomicInteger
AtomicLong
AtomicBoolean
AtomicReference
```

Example:

```java
counter.incrementAndGet();
```

Backed by CAS.

---

# 12. ReentrantLock

Benefits over synchronized:

```java
tryLock()
```

```java
lockInterruptibly()
```

```java
Fair Lock
```

```java
Timeout Support
```

---

# 13. ReadWriteLock

Two lock types:

```text
Read Lock
Write Lock
```

Many readers.

One writer.

Useful:

- Cache
- Configuration store

---

# 14. StampedLock

Modern lock implementation.

Modes:

```text
Read
Write
Optimistic Read
```

Higher performance for read-heavy systems.

---

# 15. ExecutorService

Avoid raw thread creation.

```java
ExecutorService pool =
    Executors.newFixedThreadPool(10);
```

---

# 16. ThreadPoolExecutor Deep Dive

Core Components:

```text
Core Pool Size
Maximum Pool Size
Queue
Rejection Policy
```

Workflow:

```text
Task
 ↓
Core Thread
 ↓
Queue
 ↓
Extra Thread
 ↓
Reject
```

---

# 17. Thread Pool Queues

## LinkedBlockingQueue

Almost unbounded.

Risk:

```text
Memory Growth
```

## ArrayBlockingQueue

Fixed size.

Safer.

## SynchronousQueue

No storage.

Direct handoff.

Used by:

```java
CachedThreadPool
```

---

# 18. Rejection Policies

```java
AbortPolicy
```

```java
CallerRunsPolicy
```

```java
DiscardPolicy
```

```java
DiscardOldestPolicy
```

Senior interview favorite.

---

# 19. Future vs CompletableFuture

Future:

```java
future.get();
```

Blocking.

CompletableFuture:

```java
thenApply()
thenCompose()
allOf()
```

Supports async workflows.

---

# 20. CompletableFuture Advanced

Error handling:

```java
exceptionally()
```

```java
handle()
```

```java
whenComplete()
```

Composition:

```java
thenCombine()
```

```java
allOf()
```

```java
anyOf()
```

---

# 21. ForkJoinPool

Designed for:

```text
CPU Intensive Work
```

Example:

```text
Merge Sort
Recursive Computation
```

---

# 22. Work Stealing

Each worker has queue.

Idle worker steals tasks.

Benefits:

- Better CPU utilization
- Less contention

---

# 23. Producer Consumer Pattern

```text
Producer
   ↓
BlockingQueue
   ↓
Consumer
```

Implementations:

```java
LinkedBlockingQueue
```

Very common in enterprise systems.

---

# 24. ConcurrentHashMap Internals

Java 8+

Techniques:

```text
CAS
Bucket Level Locking
Tree Bins
```

Avoids locking full map.

Much more scalable than Hashtable.

---

# 25. CopyOnWriteArrayList Internals

Write:

```text
Copy Entire Array
```

Read:

```text
No Lock Needed
```

Perfect for:

```text
Many Reads
Few Writes
```

---

# 26. Deadlock

Example:

```text
A waits B
B waits A
```

Prevention:

- lock order
- timeout
- lock reduction

---

# 27. Livelock

Threads keep reacting.

No useful progress.

---

# 28. Starvation

Thread never receives resources.

---

# 29. False Sharing

Advanced topic.

Two variables share same CPU cache line.

Performance suffers despite no logical conflict.

Related annotation:

```java
@Contended
```

---

# 30. CPU Cache & Memory Barriers

Modern CPUs reorder instructions.

Memory barriers prevent illegal reordering.

Used internally by:

```java
volatile
synchronized
CAS
```

---

# 31. Lock-Free Programming

Goal:

```text
Avoid blocking threads.
```

Examples:

```java
AtomicInteger
ConcurrentLinkedQueue
```

---

# 32. Virtual Threads Overview

Java 21+.

```java
Thread.startVirtualThread(() -> {});
```

Advantages:

- Lightweight
- Millions of threads possible
- Excellent for IO workloads

Not best for:

```text
CPU-bound workloads
```

---

# 33. Spring Boot Concurrency Cases

Async methods:

```java
@Async
```

Background jobs:

```java
TaskExecutor
```

Scheduling:

```java
@Scheduled
```

---

# 34. Concurrency Troubleshooting

Common production issues:

## High CPU

Check:

```bash
top
jstack
```

## Deadlock

Check thread dump.

## Executor Saturation

Monitor:

```text
Active Threads
Queue Size
Rejected Tasks
```

## Thread Leak

Large thread count growth.

---

# 35. Senior Interview Questions

1. synchronized vs ReentrantLock?
2. volatile vs AtomicInteger?
3. CAS advantages and disadvantages?
4. Future vs CompletableFuture?
5. Why CompletableFuture is better?
6. How ConcurrentHashMap works?
7. What is Happens-Before?
8. What is False Sharing?
9. How ForkJoinPool works?
10. Virtual Threads vs Platform Threads?
11. How deadlock occurs?
12. How to investigate high CPU?
13. ThreadPoolExecutor workflow?
14. ReadWriteLock vs StampedLock?
15. Why CopyOnWriteArrayList is expensive?

---

# Chapter Summary

✅ Thread Lifecycle
✅ Race Condition
✅ Thread Safety
✅ synchronized
✅ volatile
✅ JMM
✅ Happens-Before
✅ CAS
✅ Atomic Classes
✅ ReentrantLock
✅ ReadWriteLock
✅ StampedLock
✅ ExecutorService
✅ ThreadPoolExecutor
✅ CompletableFuture
✅ ForkJoinPool
✅ Work Stealing
✅ Producer Consumer
✅ ConcurrentHashMap Internals
✅ CopyOnWriteArrayList
✅ Deadlock
✅ Livelock
✅ Starvation
✅ False Sharing
✅ Memory Barriers
✅ Lock-Free Programming
✅ Virtual Threads
✅ Spring Concurrency
✅ Concurrency Troubleshooting
✅ Senior Interview Questions
