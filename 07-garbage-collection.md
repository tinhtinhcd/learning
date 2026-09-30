# Chapter 6 - Garbage Collection (Complete Edition)

## Sections Included

### Core GC
- Reachability Analysis
- GC Roots
- Reference Types
- Generational GC
- Minor GC
- Major GC
- Full GC
- Stop-The-World
- Mark/Sweep/Compact
- Serial GC
- Parallel GC
- CMS
- G1GC
- ZGC
- Shenandoah
- GC Logs
- GC Tuning
- Memory Leak Analysis

### Advanced GC Internals
- SATB (Snapshot At The Beginning)
- Remembered Set (RSet)
- Card Table
- Write Barrier
- Read Barrier
- Concurrent Marking
- G1 Mixed GC
- Humongous Objects
- Evacuation Failure
- Promotion Failure
- Allocation Failure
- ZGC Colored Pointers
- Load Barrier
- ZPages
- Shenandoah Brooks Pointer
- Generational ZGC
- GC Ergonomics
- Kubernetes GC Tuning
- Production Case Studies

---

# 1. Reachability Analysis
Objects are collected when unreachable from GC Roots.

GC Roots:
- Thread Stack
- Static Fields
- JNI References
- System Classes

---

# 2. Generational GC
Most objects die young.

```text
Young Gen
 ├ Eden
 ├ S0
 └ S1

Old Gen
```

---

# 3. Minor, Major and Full GC

## Minor GC
Young Generation only.

## Major GC
Old Generation.

## Full GC
Entire heap + related memory areas.

---

# 4. GC Algorithms

## Mark
Identify live objects.

## Sweep
Reclaim memory.

## Compact
Reduce fragmentation.

---

# 5. GC Collectors

## Serial GC
Single GC thread.

## Parallel GC
Maximum throughput.

## CMS
Low pause legacy collector.

## G1GC
Default modern collector.

## ZGC
Ultra-low latency.

## Shenandoah
Concurrent compaction.

---

# 6. G1GC Deep Dive

## Heap Regions

```text
Region-based Heap
```

No fixed Young/Old memory spaces.

---

## SATB (Snapshot At The Beginning)

Used by G1 concurrent marking.

Concept:

```text
Mark objects visible at marking start.
```

Provides consistent view while application runs.

---

## Remembered Set (RSet)

Tracks references crossing regions.

Benefit:

```text
Avoid full heap scan.
```

---

## Card Table

Heap divided into cards.

Used to identify modified memory regions efficiently.

---

## Write Barrier

Executed when reference updated.

Purpose:

- Maintain RSet
- Support concurrent marking

---

## Mixed GC

G1 can collect:

```text
Young Regions
+
Selected Old Regions
```

This is called Mixed GC.

---

## Humongous Objects

Large objects spanning multiple regions.

Examples:

```java
Large byte[]
Large String
```

May increase fragmentation.

---

## Evacuation Failure

Occurs when JVM cannot move live objects.

Result:

```text
Long GC pause
Potential Full GC
```

---

# 7. ZGC Deep Dive

Goal:

```text
< 10ms pause time
```

Even on very large heaps.

---

## Colored Pointers

ZGC stores metadata inside object references.

Used to track:

- Mark state
- Relocation state

---

## Load Barrier

Executed while loading references.

Enables concurrent relocation.

---

## ZPages

ZGC memory pages.

Optimized for fast allocation and relocation.

---

## Generational ZGC

Modern ZGC supports generations.

Benefits:

- Reduced CPU usage
- Better throughput
- Lower memory overhead

---

# 8. Shenandoah Deep Dive

Primary goal:

```text
Predictable low pauses
```

---

## Brooks Pointer

Extra forwarding pointer.

Allows object relocation while application continues.

---

# 9. Allocation Failure

Eden lacks free space.

Triggers:

```text
Minor GC
```

---

# 10. Promotion Failure

Object cannot move from Young to Old generation.

Potential result:

```text
Full GC
```

---

# 11. GC Ergonomics

JVM automatically adjusts:

- Heap Sizes
- Region Counts
- Thread Counts
- GC Strategies

---

# 12. GC Log Analysis

Enable:

```bash
-Xlog:gc*
```

Important Metrics:

- Pause Time
- Allocation Rate
- Promotion Rate
- Full GC Count
- Old Gen Utilization

---

# 13. Memory Leak Patterns

Common causes:

- Static Collections
- ThreadLocal Misuse
- Cache Growth
- Listener Leaks
- ClassLoader Leaks

---

# 14. Heap Dump Analysis

Workflow:

1. Capture dump
2. Open MAT
3. Find Dominator Tree
4. Check Retained Size
5. Locate GC Root Path

---

# 15. Kubernetes GC Tuning

Common Settings:

```bash
-XX:+UseG1GC
-Xms
-Xmx
```

Recommendations:

- Respect container limits
- Monitor GC pause time
- Monitor RSS memory

---

# 16. Production Case Studies

## Frequent Full GC

Symptoms:

- Latency spikes
- CPU increase

Root Causes:

- Memory leak
- Heap too small

---

## High Old Gen Usage

Potential causes:

- Cache retention
- Large object graphs

---

## Direct Memory OOM

Common in:

- Netty
- Kafka
- NIO Applications

---

# Senior Interview Questions

1. Minor GC vs Full GC?
2. How does G1GC work?
3. What is SATB?
4. What is Remembered Set?
5. Why is G1 called Garbage First?
6. What are Humongous Objects?
7. G1GC vs ZGC?
8. What are Colored Pointers?
9. What is a Write Barrier?
10. What is a Load Barrier?
11. What is Promotion Failure?
12. How investigate memory leaks?
13. How read GC logs?
14. How tune G1GC?
15. How tune GC in Kubernetes?

---

# Chapter Summary

✅ Reachability Analysis
✅ GC Roots
✅ Reference Types
✅ Generational GC
✅ Minor GC
✅ Major GC
✅ Full GC
✅ G1GC Internals
✅ SATB
✅ Remembered Set
✅ Card Table
✅ Write Barrier
✅ Mixed GC
✅ Humongous Objects
✅ ZGC
✅ Colored Pointers
✅ Load Barrier
✅ Generational ZGC
✅ Shenandoah
✅ Brooks Pointer
✅ GC Ergonomics
✅ Heap Dump Analysis
✅ GC Logs
✅ Kubernetes Tuning
✅ Production Case Studies
✅ Senior Interview Questions
