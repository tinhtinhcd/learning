# Chapter 2 - Collections Framework

## Learning Objectives

After completing this chapter, you will be able to:

- Understand the complete Java Collections Framework
- Select the right collection for different use cases
- Master HashMap internals
- Understand ConcurrentHashMap internals
- Understand equals() and hashCode() contracts
- Understand Hash Collisions, Load Factor, Rehashing
- Understand Red-Black Tree fundamentals
- Understand Iterators and Collection traversal
- Understand Comparable vs Comparator
- Understand Fail-Fast vs Fail-Safe behavior
- Analyze Big-O complexity
- Answer Senior Java interview questions confidently

---

# 1. Collections Framework Overview

```text
Iterable
 └─ Collection
     ├─ List
     │   ├─ ArrayList
     │   ├─ LinkedList
     │   └─ Vector
     │
     ├─ Set
     │   ├─ HashSet
     │   ├─ LinkedHashSet
     │   └─ TreeSet
     │
     └─ Queue
         ├─ PriorityQueue
         └─ ArrayDeque

Map
 ├─ HashMap
 ├─ LinkedHashMap
 ├─ TreeMap
 ├─ Hashtable
 ├─ ConcurrentHashMap
 ├─ WeakHashMap
 └─ IdentityHashMap
```

Collections provide:

- Dynamic sizing
- Searching
- Sorting
- Grouping
- Thread-safe alternatives

---

# 2. List Interface

## Characteristics

- Ordered
- Allows duplicates
- Supports index access

```java
List<String> names = new ArrayList<>();
```

---

# 3. ArrayList

## Internal Structure

```text
Dynamic Array
```

### Resize Strategy

```java
newCapacity = oldCapacity + oldCapacity / 2
```

### Complexity

```text
get()      O(1)
add()      O(1) amortized
remove()   O(n)
contains() O(n)
```

### Advantages

- Fast random access
- Cache-friendly
- Most common List implementation

### Disadvantages

- Expensive middle insertion/removal

### Interview Questions

Q: Why is get() O(1)?

A: Elements are stored in contiguous memory and accessed directly by index.

Q: Why can add() become expensive?

A: Resizing requires allocating a larger array and copying all elements.

---

# 4. LinkedList

## Internal Structure

```text
Node
 ├─ previous
 ├─ value
 └─ next
```

Example:

```text
A <-> B <-> C
```

### Complexity

```text
get()      O(n)
insert()   O(1)*
remove()   O(1)*
```

*Assuming node reference already known.

### Interview Question

Q: ArrayList vs LinkedList?

A: ArrayList is preferred for read-heavy workloads. LinkedList is useful for frequent insertion/deletion when node position is known.

---

# 5. Vector

Legacy List implementation.

Characteristics:

- Thread-safe
- Synchronized methods
- Usually slower than ArrayList

Interview:

Q: Why is Vector rarely used?

A: Modern applications prefer ArrayList or Concurrent Collections.

---

# 6. Set Interface

## Characteristics

- No duplicates
- Unique elements only

---

# 7. HashSet

## Internal Structure

HashSet uses HashMap internally.

```java
HashMap<E,Object>
```

Dummy value:

```java
PRESENT
```

### Complexity

```text
add()      O(1)
remove()   O(1)
contains() O(1)
```

Interview:

Q: How does HashSet work?

A: Elements are stored as keys of an internal HashMap.

---

# 8. LinkedHashSet

Maintains insertion order.

Benefits:

- Predictable iteration order
- No duplicates

Complexity remains approximately O(1).

---

# 9. TreeSet

## Internal Structure

```text
Red-Black Tree
```

Automatically sorted.

### Complexity

```text
add()      O(log n)
remove()   O(log n)
contains() O(log n)
```

Interview:

Q: HashSet vs TreeSet?

A:
HashSet is faster.
TreeSet maintains sorting.

---

# 10. Queue Interface

FIFO structure.

Implementations:

- LinkedList
- PriorityQueue
- ArrayDeque

---

# 11. PriorityQueue

Elements ordered by priority.

```java
PriorityQueue<Integer> pq = new PriorityQueue<>();
```

Example Output:

```text
1 2 3 4 5
```

Internal Structure:

```text
Binary Heap
```

Complexity:

```text
offer() O(log n)
poll()  O(log n)
peek()  O(1)
```

---

# 12. ArrayDeque

Double-ended queue.

Supports:

```text
addFirst()
addLast()
removeFirst()
removeLast()
```

Often preferred over Stack.

---

# 13. Map Interface

Stores:

```text
Key -> Value
```

Keys must be unique.

---

# 14. HashMap Deep Dive

## Internal Structure

```text
Bucket Array
   ↓
Linked List
   ↓
Red-Black Tree
```

## put() Flow

1. Call hashCode()
2. Compute bucket
3. Locate bucket
4. Compare using equals()
5. Insert or replace value

### Complexity

```text
get() O(1)
put() O(1)
```

Average case.

---

# 15. Hash Collision

Occurs when multiple keys map to the same bucket.

Example:

```text
key1 → bucket 3
key2 → bucket 3
```

### Java 7

Collision storage:

```text
Linked List
```

### Java 8+

If bucket size exceeds threshold:

```text
Treeify
```

Convert to:

```text
Red-Black Tree
```

Performance improves:

```text
O(n) → O(log n)
```

---

# 16. equals() and hashCode()

## Contract

If:

```java
a.equals(b)
```

Then:

```java
a.hashCode() == b.hashCode()
```

Must be true.

### Interview Question

Why override both?

Answer:

HashMap uses hashCode() to locate buckets and equals() to compare keys.

---

# 17. Load Factor

Default:

```java
0.75
```

Formula:

```text
size > capacity × loadFactor
```

Triggers:

```text
Rehashing
```

---

# 18. Rehashing

Process:

1. Create larger bucket array
2. Redistribute entries

Example:

```text
16 -> 32
```

Cost:

```text
O(n)
```

Best Practice:

```java
new HashMap<>(1000)
```

when approximate size is known.

---

# 19. LinkedHashMap

Maintains insertion order.

Common Usage:

- LRU Cache
- Ordered iteration

---

# 20. TreeMap

## Internal Structure

```text
Red-Black Tree
```

Complexity:

```text
put() O(log n)
get() O(log n)
```

Interview:

Q: HashMap vs TreeMap?

A:
HashMap is faster.
TreeMap provides sorting.

---

# 21. Hashtable

Legacy synchronized Map.

Characteristics:

- Thread-safe
- Entire structure synchronized

Generally replaced by ConcurrentHashMap.

---

# 22. ConcurrentHashMap

## Why Needed?

HashMap is not thread-safe.

Hashtable scales poorly.

## Modern Approach

- Fine-grained synchronization
- CAS operations
- Better parallelism

Interview:

Q: HashMap vs Hashtable vs ConcurrentHashMap?

A:
HashMap → fastest, not thread-safe.
Hashtable → thread-safe but poor scalability.
ConcurrentHashMap → thread-safe and scalable.

---

# 23. WeakHashMap

Keys held through weak references.

When key becomes unreachable:

```text
Garbage Collector may remove entry.
```

Use Cases:

- Metadata caches
- Temporary mappings

---

# 24. IdentityHashMap

Comparison uses:

```java
==
```

instead of

```java
equals()
```

Use Cases:

- Reference tracking
- Object graph processing

---

# 25. Comparable vs Comparator

## Comparable

Natural ordering.

```java
class User implements Comparable<User>
```

Single ordering strategy.

---

## Comparator

External ordering.

```java
Comparator<User>
```

Multiple sorting strategies.

Interview:

Q: Comparable vs Comparator?

A:
Comparable defines natural ordering inside the class.
Comparator defines external ordering logic.

---

# 26. Iterator vs ListIterator

## Iterator

Supported:

```java
next()
hasNext()
remove()
```

Forward only.

---

## ListIterator

Supported:

```java
previous()
next()
add()
set()
```

Bidirectional traversal.

---

# 27. Fail-Fast vs Fail-Safe

## Fail-Fast

Examples:

```java
ArrayList
HashMap
HashSet
```

Throws:

```java
ConcurrentModificationException
```

when collection modified during iteration.

---

## Fail-Safe

Examples:

```java
ConcurrentHashMap
CopyOnWriteArrayList
```

Iterates over a snapshot.

No exception.

Interview:

Q: Difference?

A:
Fail-Fast detects structural changes.
Fail-Safe works on copied/snapshot data.

---

# 28. Big-O Cheat Sheet

```text
ArrayList
get()         O(1)
add()         O(1)
remove()      O(n)

LinkedList
get()         O(n)
insert()      O(1)

HashMap
get()         O(1)
put()         O(1)

TreeMap
get()         O(log n)

HashSet
contains()    O(1)

TreeSet
contains()    O(log n)

PriorityQueue
offer()       O(log n)
poll()        O(log n)
```

---

# 29. Common Pitfalls

## Mutable Keys

Never modify keys after insertion.

## Missing equals/hashCode

Produces incorrect Set and Map behavior.

## Using LinkedList Everywhere

Usually worse than ArrayList.

## Incorrect Comparator

May break TreeMap and TreeSet ordering behavior.

---

# Senior Interview Questions

### Q1. How does HashMap work internally?

HashMap uses hashCode() for bucket location and equals() for key comparison.

### Q2. Why is load factor 0.75?

Balanced trade-off between memory usage and performance.

### Q3. When does HashMap become O(log n)?

After treeification of heavily-collided buckets.

### Q4. Why does HashSet use HashMap?

Reuse proven hash-based implementation.

### Q5. Why is ConcurrentHashMap faster than Hashtable?

It avoids locking the entire structure.

### Q6. Difference between Comparable and Comparator?

Comparable defines natural ordering.
Comparator provides external ordering.

### Q7. What causes ConcurrentModificationException?

Modifying a Fail-Fast collection during iteration.

---

# Exercises

## Exercise 1

Implement User class with equals() and hashCode().

## Exercise 2

Benchmark ArrayList vs LinkedList.

## Exercise 3

Trace HashMap.put() step-by-step.

## Exercise 4

Implement custom Comparator.

## Exercise 5

Demonstrate ConcurrentModificationException.

---

# Chapter Summary

✅ List
✅ Set
✅ Queue
✅ Map
✅ ArrayList
✅ LinkedList
✅ HashSet
✅ LinkedHashSet
✅ TreeSet
✅ HashMap
✅ LinkedHashMap
✅ TreeMap
✅ ConcurrentHashMap
✅ WeakHashMap
✅ IdentityHashMap
✅ PriorityQueue
✅ ArrayDeque
✅ equals()
✅ hashCode()
✅ Collision
✅ Load Factor
✅ Rehashing
✅ Red-Black Tree
✅ Comparable
✅ Comparator
✅ Iterator
✅ ListIterator
✅ Fail-Fast
✅ Fail-Safe
✅ Big-O Analysis
✅ Senior Interview Questions
