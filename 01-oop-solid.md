# Chapter 1 - OOP, SOLID & Clean Object Design

## Learning Objectives

After completing this chapter, you will be able to:

- Understand the four pillars of Object-Oriented Programming (OOP)
- Apply the five SOLID principles in real-world applications
- Distinguish between Composition and Inheritance
- Design immutable and maintainable objects
- Understand Entity vs Value Object concepts
- Understand the relationship between Dependency Injection and DIP
- Identify common OOP anti-patterns
- Confidently answer Senior Java interview questions

---

# 1. Introduction to OOP

Object-Oriented Programming (OOP) is a programming paradigm that organizes software around objects.

An object contains:

- State (fields)
- Behavior (methods)

Example:

```java
public class User {

    private String username;

    public void login() {
        System.out.println("Login successful");
    }
}
```

State:

```java
username
```

Behavior:

```java
login()
```

Benefits of OOP:

- Reusability
- Maintainability
- Extensibility
- Better modeling of business domains

---

# 2. Encapsulation

## Definition

Encapsulation is the process of hiding internal implementation details and exposing only necessary operations.

The primary goal is to protect object state and ensure consistency.

## Poor Design Example

```java
public class BankAccount {
    public double balance;
}
```

Problem:

```java
account.balance = -100000;
```

Invalid values can be assigned directly.

## Good Design Example

```java
public class BankAccount {

    private double balance;

    public void deposit(double amount) {
        if (amount <= 0) {
            throw new IllegalArgumentException();
        }

        balance += amount;
    }

    public double getBalance() {
        return balance;
    }
}
```

## Benefits

### Data Protection

Prevent invalid data modification.

### Flexibility

Implementation can change without affecting consumers.

### Reduced Coupling

Consumers depend on behavior rather than internal implementation.

## Interview Questions

### What is encapsulation?

**Answer**

Encapsulation is the practice of hiding internal object state and exposing only controlled operations through public methods.

### Why is encapsulation important?

**Answer**

It protects data integrity, reduces complexity, and improves maintainability.

### Can getters and setters break encapsulation?

**Answer**

Yes. Overexposing setters may allow uncontrolled state changes and weaken encapsulation.

---

# 3. Inheritance

## Definition

Inheritance allows a class to reuse behavior from another class.

## Example

```java
class Animal {

    public void eat() {
        System.out.println("Eat");
    }
}

class Dog extends Animal {
}
```

## Advantages

- Code reuse
- Shared behavior
- Hierarchical design

## Disadvantages

- Tight coupling
- Fragile hierarchy
- Difficult to refactor

---

# 4. Composition

## Definition

Composition means building objects using other objects.

## Example

```java
public class Car {

    private Engine engine;
}
```

Relationship:

```text
Car HAS-A Engine
```

---

# Composition vs Inheritance

## Inheritance

```text
Dog IS-A Animal
```

## Composition

```text
Car HAS-A Engine
```

## Best Practice

Favor Composition Over Inheritance.

## Interview Question

### Composition vs Inheritance?

**Answer**

Composition is usually preferred because it promotes flexibility, reduces coupling, and simplifies future changes.

### When should inheritance be used?

**Answer**

Only when a true IS-A relationship exists.

---

# 5. Polymorphism

## Definition

Polymorphism allows multiple implementations to be accessed through a common interface.

## Example

```java
public interface PaymentService {
    void pay();
}
```

```java
public class PaypalPayment implements PaymentService {

    @Override
    public void pay() {
        System.out.println("Pay with Paypal");
    }
}
```

```java
public class CreditCardPayment implements PaymentService {

    @Override
    public void pay() {
        System.out.println("Pay with Card");
    }
}
```

Usage:

```java
PaymentService service = new PaypalPayment();
service.pay();
```

## Benefits

- Extensibility
- Loose coupling
- Easier testing

## Interview Question

### What is polymorphism?

**Answer**

Polymorphism allows different implementations to be treated through a common abstraction.

### Compile-time vs Runtime polymorphism?

**Answer**

Compile-time: Method overloading.

Runtime: Method overriding.

---

# 6. Abstraction

## Definition

Abstraction hides implementation details while exposing capabilities.

## Example

```java
public interface NotificationService {

    void send();
}
```

Consumers do not need to know whether implementation uses:

- Email
- SMS
- Kafka
- Push Notification

## Interview Question

### Abstraction vs Encapsulation?

**Answer**

Abstraction hides implementation complexity.

Encapsulation hides internal data.

---

# 7. SOLID Principles

## S - Single Responsibility Principle (SRP)

A class should have only one reason to change.

### Bad Example

```java
class UserService {

    void saveUser() {}

    void sendEmail() {}

    void generateReport() {}
}
```

### Better Design

```text
UserService
EmailService
ReportService
```

### Interview Question

What is SRP?

**Answer**

Each class should have only one responsibility.

---

## O - Open Closed Principle (OCP)

Software should be:

- Open for extension
- Closed for modification

### Bad Example

```java
if(type.equals("PAYPAL")) {}
else if(type.equals("CARD")) {}
```

### Better Design

```java
interface PaymentStrategy {
    void pay();
}
```

Interview:

Strategy Pattern is one of the most common examples of OCP.

---

## L - Liskov Substitution Principle (LSP)

Subtypes should be replaceable with base types.

### Bad Example

```java
class Bird {
    void fly() {}
}
```

```java
class Penguin extends Bird {
}
```

Penguins cannot fly.

Violation of LSP.

---

## I - Interface Segregation Principle (ISP)

Clients should not depend on methods they do not use.

### Bad Example

```java
interface Worker {
    void work();
    void eat();
    void sleep();
}
```

### Better Design

```java
interface Workable {}
interface Eatable {}
interface Sleepable {}
```

---

## D - Dependency Inversion Principle (DIP)

High-level modules should depend on abstractions rather than implementations.

### Bad Example

```java
class UserService {
    OracleDatabase database;
}
```

### Better Design

```java
class UserService {
    Database database;
}
```

### Relationship to Spring

Dependency Injection is a practical implementation of DIP.

Examples:

```java
@Autowired
```

```java
@Bean
```

```java
@Configuration
```

---

# 8. Entity vs Value Object

## Entity

An Entity has identity.

Example:

```java
User
```

```java
userId
```

Uniquely identifies the object.

## Value Object

A Value Object is defined entirely by its values.

Examples:

```java
Money
Address
Coordinate
```

## Interview Question

### Entity vs Value Object?

**Answer**

Entities are identified by IDs.

Value Objects are identified by their attributes.

---

# 9. Immutable Objects

## Definition

Immutable objects cannot change after creation.

## Example

```java
public final class User {

    private final String name;

    public User(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}
```

## Benefits

### Thread Safety

No synchronization required.

### Predictability

State never changes.

### Easier Debugging

Fewer side effects.

## Java 17 Record

```java
public record User(
        String name,
        Integer age
) {}
```

Record is a modern immutable data carrier.

---

# 10. Common OOP Anti-Patterns

## God Class

One class doing too many things.

Example:

```text
UserService
 ├─ Database
 ├─ Email
 ├─ Logging
 ├─ Validation
 └─ Reporting
```

## Deep Inheritance

```text
A
 └─ B
     └─ C
         └─ D
             └─ E
```

Hard to maintain.

## Anemic Domain Model

Objects contain only getters and setters.

Business logic exists elsewhere.

## Primitive Obsession

Using primitive types where domain objects should exist.

Bad:

```java
String countryCode;
```

Better:

```java
Country country;
```

---

# Senior Interview Questions

## Q1. Abstraction vs Encapsulation?

Answer:

Encapsulation protects data.
Abstraction hides complexity.

## Q2. Composition vs Inheritance?

Answer:

Prefer composition because it reduces coupling and improves flexibility.

## Q3. Most commonly violated SOLID principles?

Answer:

SRP and OCP.

## Q4. Why does Spring use interfaces heavily?

Answer:

To support polymorphism, loose coupling, testing, and dependency inversion.

## Q5. Why are immutable objects beneficial in concurrent applications?

Answer:

Because immutable objects are inherently thread-safe.

---

# Exercises

## Exercise 1

Design a Payment System using:

- OCP
- Strategy Pattern
- Dependency Injection

## Exercise 2

Refactor a God Class into multiple SRP-compliant services.

## Exercise 3

Convert a mutable DTO into a Java 17 Record.

---

# Chapter Summary

✅ Encapsulation

✅ Inheritance

✅ Composition

✅ Polymorphism

✅ Abstraction

✅ SOLID Principles

✅ Entity vs Value Object

✅ Immutable Objects

✅ DIP and Dependency Injection

✅ OOP Anti-Patterns

✅ Senior Java Interview Questions

This chapter provides the design foundation required for Spring Framework, Clean Architecture, Domain-Driven Design, and modern Java application development.
