# Chapter 10 - Design Patterns Masterclass 

## How To Study This Chapter

For each pattern:

1. Problem Statement
2. Mermaid Diagram
3. Java Example
4. Sequence Flow
5. Real World Usage
6. Interview Notes

---

# Builder Pattern

## Problem

Too many constructor parameters.

```java
User user = new User("Tinh","Ly","Van","VN","Bac Ninh");
```

## Diagram

```mermaid
classDiagram
class User
class UserBuilder
UserBuilder --> User
```

## Code

```java
User user = User.builder()
    .firstName("Tinh")
    .lastName("Ly")
    .build();
```

## Real Project

- DTO creation
- Configuration objects
- Spring builders

---

# Factory Method Pattern

## Problem

Create objects without exposing creation logic.

```mermaid
classDiagram
class Payment
class PaypalPayment
class MomoPayment
class PaymentFactory
PaymentFactory --> Payment
```

```java
Payment payment = factory.create("PAYPAL");
```

## Usage

- Spring BeanFactory
- JDBC Drivers

---

# Singleton Pattern

## Problem

Need exactly one instance.

```mermaid
classDiagram
class ConfigManager {
 +getInstance()
}
```

```java
public enum ConfigManager {
 INSTANCE;
}
```

## Usage

- Logger
- Cache Manager

---

# Adapter Pattern

## Problem

Integrate incompatible APIs.

```mermaid
classDiagram
class PaymentService
class PaypalSDK
class PaypalAdapter
PaymentService <|.. PaypalAdapter
PaypalAdapter --> PaypalSDK
```

```java
adapter.pay();
```

```mermaid
sequenceDiagram
Client->>Adapter: pay()
Adapter->>PaypalSDK: execute()
```

## Usage

- Legacy integration
- SAP integration

---

# Facade Pattern

## Problem

Hide complex subsystem.

```mermaid
flowchart LR
Client --> Facade
Facade --> ServiceA
Facade --> ServiceB
Facade --> ServiceC
```

```java
orderFacade.placeOrder();
```

---

# Proxy Pattern

## Problem

Add control before accessing target.

```mermaid
flowchart LR
Client --> Proxy
Proxy --> RealService
```

Examples:

- Spring AOP
- JDK Dynamic Proxy

---

# Decorator Pattern

## Problem

Add behavior dynamically.

```mermaid
flowchart LR
Coffee --> MilkDecorator
MilkDecorator --> SugarDecorator
```

```java
coffee = new SugarDecorator(
           new MilkDecorator(coffee));
```

---

# Strategy Pattern

## Problem

Switch algorithms at runtime.

```mermaid
flowchart TD
PaymentService --> CreditCardStrategy
PaymentService --> PaypalStrategy
PaymentService --> MomoStrategy
```

```java
strategy.pay();
```

## Usage

- Payment methods
- Sorting algorithms

---

# Observer Pattern

## Problem

Notify multiple services when event occurs.

```mermaid
flowchart LR
OrderCreated --> EmailService
OrderCreated --> SMSService
OrderCreated --> AuditService
```

## Usage

- Event Driven Architecture
- Spring Events

---

# Command Pattern

## Problem

Encapsulate request as object.

```mermaid
flowchart LR
Client --> Command
Command --> Receiver
```

Example:

```java
command.execute();
```

---

# Template Method Pattern

## Problem

Reuse common workflow.

```mermaid
flowchart TD
Validate --> Process
Process --> Save
Save --> Notify
```

Subclass customizes steps.

---

# Chain of Responsibility

## Problem

Pass request through handlers.

```mermaid
flowchart LR
Request --> Auth
Auth --> Validation
Validation --> Business
```

Usage:

- Spring Security Filter Chain

---

# State Pattern

## Problem

Behavior changes based on current state.

```mermaid
stateDiagram-v2
[*] --> Created
Created --> Paid
Paid --> Shipped
Shipped --> Delivered
```

Examples:

- Order lifecycle

---

# Pattern Selection Guide

| Scenario | Pattern |
|-----------|----------|
| Complex Object Creation | Builder |
| Runtime Algorithm | Strategy |
| Event Notification | Observer |
| Legacy Integration | Adapter |
| Simplified API | Facade |
| Access Control | Proxy |
| Workflow Reuse | Template Method |
| Request Pipeline | Chain of Responsibility |

---

# Senior Java Interview Questions

1. Strategy vs State?
2. Adapter vs Facade?
3. Proxy vs Decorator?
4. Why Builder over Constructor?
5. Where does Spring use Factory?
6. Where does Spring use Proxy?
7. Observer vs Event Driven?
8. Explain Filter Chain pattern.

---

# Architect Checklist

✅ Singleton
✅ Factory
✅ Builder
✅ Adapter
✅ Facade
✅ Proxy
✅ Decorator
✅ Strategy
✅ Observer
✅ Command
✅ Template Method
✅ State
✅ Chain of Responsibility
