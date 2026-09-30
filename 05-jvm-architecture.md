# Chapter 5 - JVM Architecture

## Learning Objectives

After completing this chapter, you will be able to:

- Understand JVM architecture end-to-end
- Explain class loading and class lifecycle
- Understand Heap, Stack, Metaspace and Native Memory
- Understand object creation and memory allocation
- Explain JIT compilation and runtime optimization
- Understand TLAB and Escape Analysis
- Understand reference types
- Diagnose OutOfMemoryError and StackOverflowError
- Analyze Heap Dump and Thread Dump
- Troubleshoot JVM issues in production
- Answer Senior Java interview questions confidently

---

# 1. What is JVM?

JVM (Java Virtual Machine) is the runtime environment responsible for:

- Loading classes
- Managing memory
- Executing bytecode
- Performing garbage collection
- Providing platform independence

Flow:

```text
Java Source
   ↓
javac
   ↓
Bytecode (.class)
   ↓
JVM
   ↓
Machine Code
```

---

# 2. High-Level JVM Architecture

```text
Class Loader Subsystem
        ↓
Runtime Data Areas
        ↓
Execution Engine
        ↓
Native Interface
        ↓
Native Libraries
```

Main Components:

- Class Loader
- Runtime Data Areas
- Execution Engine
- JNI
- Native Libraries

---

# 3. Class Loader Subsystem

Purpose:

```text
Load .class files into memory.
```

Class Loaders:

```text
Bootstrap ClassLoader
        ↓
Platform ClassLoader
        ↓
Application ClassLoader
```

---

# 4. Bootstrap ClassLoader

Loads:

```text
java.lang.*
java.util.*
java.io.*
```

Responsible for core JDK classes.

---

# 5. Platform ClassLoader

Loads:

```text
jdk.*
javax.*
```

---

# 6. Application ClassLoader

Loads:

```text
Application Classes
Third Party Libraries
```

Examples:

```text
Spring Boot
Hibernate
Jackson
```

---

# 7. Parent Delegation Model

Loading process:

```text
Application
    ↓
Platform
    ↓
Bootstrap
```

Benefits:

- Security
- Prevent duplicate class loading
- Consistent behavior

Interview Favorite.

---

# 8. Class Lifecycle

```text
Loading
 ↓
Linking
  ├ Verification
  ├ Preparation
  └ Resolution
 ↓
Initialization
 ↓
Usage
 ↓
Unloading
```

---

# 9. Runtime Data Areas

```text
Heap
Stack
Metaspace
PC Register
Native Method Stack
```

Critical Senior Topic.

---

# 10. Heap Memory

Purpose:

```text
Store Objects
```

Shared by all threads.

---

## Heap Structure

```text
Heap
 ├ Eden
 ├ Survivor S0
 ├ Survivor S1
 └ Old Generation
```

Most objects allocated in Eden.

---

# 11. Young Generation

Contains:

```text
Eden
S0
S1
```

Characteristics:

- Short-lived objects
- Frequent Minor GC

Examples:

```java
DTO
Request Object
Temporary Collections
```

---

# 12. Old Generation

Contains:

```text
Long-lived Objects
```

Examples:

```text
Cache
Singleton Beans
Large Structures
```

GC impacts response time significantly.

---

# 13. Stack Memory

Every thread has its own stack.

Contains:

```text
Method Frames
```

---

## Stack Frame

```text
Local Variables
Operand Stack
Return Address
```

Example:

```java
calculate()
```

creates a new frame.

---

# 14. StackOverflowError

Cause:

```text
Infinite Recursion
```

Example:

```java
public void loop() {
    loop();
}
```

---

# 15. Metaspace

Java 8+

Replaced:

```text
PermGen
```

Stores:

```text
Class Metadata
Methods
Annotations
```

Uses Native Memory.

---

# 16. Program Counter Register

Stores:

```text
Current instruction address.
```

Each thread owns a separate PC Register.

---

# 17. Native Method Stack

Used when calling native code.

Examples:

```java
JNI
C Libraries
OS APIs
```

---

# 18. Object Creation Lifecycle

```text
new Object()
 ↓
Memory Allocation
 ↓
Initialize Fields
 ↓
Constructor
 ↓
Reference Assignment
```

---

# 19. Object Header

Every Java object contains:

```text
Mark Word
Class Pointer
```

Used for:

- Hash Code
- Lock State
- GC Metadata

---

# 20. Object Layout

```text
Object Header
Instance Data
Padding
```

Interview Favorite.

---

# 21. String Pool

Purpose:

```text
Reuse String instances.
```

Example:

```java
String a = "java";
String b = "java";
```

Result:

```java
a == b
```

is true.

---

# 22. Integer Cache

Default cache range:

```text
-128 to 127
```

Example:

```java
Integer a = 100;
Integer b = 100;
```

Same cached object.

---

# 23. Reference Types

## Strong Reference

Default reference.

```java
Object obj = new Object();
```

---

## Soft Reference

Collected when memory pressure occurs.

Useful for caches.

---

## Weak Reference

Collected during next GC.

Used by:

```java
WeakHashMap
```

---

## Phantom Reference

Advanced cleanup mechanism.

---

# 24. Execution Engine

Responsible for:

```text
Executing Bytecode
```

Components:

```text
Interpreter
JIT Compiler
GC
```

---

# 25. Interpreter

Reads bytecode line-by-line.

Advantages:

- Fast startup

Disadvantages:

- Slower execution

---

# 26. JIT Compiler

Converts bytecode to machine code.

Benefits:

- Better runtime performance

---

## Tiered Compilation

```text
Interpreter
 ↓
C1 Compiler
 ↓
C2 Compiler
```

---

# 27. Escape Analysis

Determines whether object escapes method scope.

Benefits:

```text
Stack Allocation
Lock Elimination
```

---

# 28. TLAB (Thread Local Allocation Buffer)

Each thread receives allocation area.

Benefits:

```text
Reduce contention
Fast allocation
```

---

# 29. Direct Memory

Outside Heap.

Examples:

```java
ByteBuffer.allocateDirect()
```

Advantages:

- Faster I/O

Risk:

```text
OutOfMemoryError:
Direct buffer memory
```

---

# 30. Native Memory

Used by:

- Metaspace
- JNI
- Direct Buffers

Not visible in Java Heap.

---

# 31. OutOfMemoryError Variants

## Java Heap Space

Heap exhausted.

---

## GC Overhead Limit Exceeded

Too much GC.

Too little progress.

---

## Metaspace

Too many classes.

ClassLoader leak.

---

## Direct Buffer Memory

Direct memory exhausted.

---

## Unable To Create Native Thread

OS thread limit reached.

---

# 32. Heap Dump

Capture memory state.

Tools:

```bash
jmap
```

```bash
jcmd
```

Analysis:

```text
MAT
VisualVM
```

---

# 33. Thread Dump

Capture thread state.

Command:

```bash
jstack PID
```

Useful for:

- Deadlock
- High CPU
- Blocking issue

---

# 34. JVM Diagnostic Tools

## jps

List JVM processes.

## jstack

Thread dump.

## jmap

Heap dump.

## jcmd

Modern diagnostic tool.

## VisualVM

GUI monitoring.

## JConsole

JMX monitoring.

---

# 35. Production Troubleshooting

## High Memory Usage

Check:

- Heap Dump
- Retained Objects
- Cache Growth

---

## High CPU

Check:

- Thread Dump
- Infinite Loops
- Excessive GC

---

## Frequent Full GC

Check:

- Heap Size
- Memory Leak
- Large Objects

---

## Metaspace Growth

Common Cause:

```text
ClassLoader Leak
```

---

# 36. Common JVM Interview Questions

1. Heap vs Stack?
2. What is Metaspace?
3. What is Parent Delegation?
4. Strong vs Weak Reference?
5. How String Pool works?
6. What is JIT?
7. What is Escape Analysis?
8. What causes StackOverflowError?
9. What causes OutOfMemoryError?
10. Heap Dump vs Thread Dump?
11. What is TLAB?
12. Direct Memory vs Heap Memory?
13. Why Metaspace replaced PermGen?
14. How classes are loaded?
15. How investigate high memory usage?

---

# Exercises

## Exercise 1

Draw complete JVM architecture.

## Exercise 2

Analyze Heap vs Stack allocation examples.

## Exercise 3

Generate and inspect Thread Dump.

## Exercise 4

Generate Heap Dump and identify largest objects.

## Exercise 5

Compare Strong, Soft, Weak, and Phantom References.

---

# Chapter Summary

✅ JVM Architecture
✅ Class Loaders
✅ Parent Delegation Model
✅ Runtime Data Areas
✅ Heap
✅ Stack
✅ Metaspace
✅ PC Register
✅ Native Method Stack
✅ Object Lifecycle
✅ Object Header
✅ String Pool
✅ Integer Cache
✅ Reference Types
✅ Execution Engine
✅ JIT
✅ Escape Analysis
✅ TLAB
✅ Direct Memory
✅ Native Memory
✅ OutOfMemoryError Variants
✅ Heap Dump
✅ Thread Dump
✅ JVM Tools
✅ Production Troubleshooting
✅ Senior JVM Interview Questions
