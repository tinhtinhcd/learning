# Chapter 22 - Microservices Architecture Masterclass

## Learning Objectives

- Understand why organizations move from Monolith to Microservices
- Design scalable microservices architectures
- Implement service communication patterns
- Handle distributed transactions and data consistency
- Apply resilience patterns in production systems
- Prepare for Senior Java, Tech Lead, and Solution Architect interviews

---

# Part I. Introduction to Microservices

## What is a Microservice?

A microservice is a small, independently deployable service that owns its business capability and data.

Characteristics:
- Independent deployment
- Business-focused
- Decentralized data ownership
- Autonomous team ownership

---

## Monolith vs Microservices

Monolith:

```text
UI
 ↓
Application
 ↓
Single Database
```

Microservices:

```text
Client
 ↓
API Gateway
 ↓
User Service
Order Service
Payment Service
```

Advantages:
- Independent deployment
- Better scalability
- Team autonomy

Challenges:
- Distributed systems complexity
- Monitoring
- Data consistency

---

# Part II. Domain Driven Design (DDD)

## Bounded Context

Examples:
- User Management
- Order Management
- Payment Management

Rule:

```text
One Service
=
One Business Domain
```

---

# Part III. Service Decomposition

## Bad Decomposition

```text
User CRUD Service
Product CRUD Service
```

## Good Decomposition

```text
Customer Service
Order Service
Inventory Service
Payment Service
```

Focus on business capability.

---

# Part IV. API Gateway Pattern

Architecture:

```text
Client
 ↓
API Gateway
 ↓
Microservices
```

Responsibilities:
- Routing
- Authentication
- Rate Limiting
- Logging

Tools:
- Spring Cloud Gateway
- Kong
- NGINX

---

# Part V. Service Discovery

Why?

Instances change dynamically.

Solutions:
- Eureka
- Consul
- Kubernetes Service Discovery

---

# Part VI. Inter-Service Communication

## Synchronous Communication

REST API:

```text
Order Service
 ↓
Payment Service
```

Pros:
- Simple

Cons:
- Tight coupling

---

## Asynchronous Communication

```text
Order Service
 ↓
Kafka
 ↓
Payment Service
```

Pros:
- Loose coupling
- Better scalability

---

# Part VII. Database per Service

Anti-pattern:

```text
Multiple Services
 ↓
Single Database
```

Recommended:

```text
Service A → DB A
Service B → DB B
```

Benefits:
- Loose coupling
- Independent deployment

---

# Part VIII. Distributed Transactions

Problem:

```text
Order Success
Payment Failed
```

Traditional 2PC:
- Complex
- Poor scalability

---

## Saga Pattern

```text
Order Created
 ↓
Reserve Inventory
 ↓
Process Payment
 ↓
Confirm Order
```

Compensation handles failures.

---

# Part IX. Event Driven Architecture

Event Example:

```text
OrderCreated
PaymentCompleted
OrderShipped
```

Benefits:
- Decoupling
- Scalability
- Auditability

---

# Part X. Resilience Patterns

## Circuit Breaker

```text
Too Many Failures
 ↓
Open Circuit
```

Tools:
- Resilience4j

---

## Retry Pattern

```java
@Retry(name = "payment")
```

---

## Bulkhead Pattern

Prevent one service from exhausting resources.

---

## Timeout Pattern

Always configure request timeout.

---

# Part XI. Observability

## Logging

Centralized logging:
- ELK
- OpenSearch

## Metrics

- Prometheus
- Grafana

## Tracing

- OpenTelemetry
- Jaeger
- Zipkin

---

# Part XII. Security in Microservices

Authentication:
- OAuth2
- JWT

Authorization:
- RBAC
- ABAC

Service-to-Service:
- mTLS
- Client Credentials

---

# Part XIII. Deployment Strategies

## Blue-Green Deployment

```text
Blue
 ↓
Green
```

## Canary Deployment

```text
5%
20%
50%
100%
```

---

# Part XIV. Spring Cloud Ecosystem

Components:
- Spring Cloud Gateway
- OpenFeign
- Config Server
- Kubernetes Integration

## OpenFeign Example

```java
@FeignClient(name="payment-service")
public interface PaymentClient {
}
```

---

# Part XV. Production Architecture Example

```text
Users
 ↓
API Gateway
 ↓
Auth Service
Order Service
Inventory Service
Payment Service
Notification Service
 ↓
Kafka
Redis
MySQL
```

---

# Part XVI. Common Anti-Patterns

- Distributed Monolith
- Shared Database
- Chatty Communication
- Large Services
- Missing Monitoring

---

# Part XVII. Interview Questions

1. Monolith vs Microservices?
2. Database per Service?
3. API Gateway benefits?
4. Service Discovery?
5. REST vs Kafka?
6. What is Saga Pattern?
7. Circuit Breaker?
8. Why Event Driven Architecture?
9. Distributed Transaction challenges?
10. How would you design an e-commerce platform?

---

# Tech Lead Checklist

✅ Domain Driven Design
✅ Service Decomposition
✅ API Gateway
✅ Service Discovery
✅ REST Communication
✅ Event Driven Architecture
✅ Database per Service
✅ Saga Pattern
✅ Circuit Breaker
✅ Observability
✅ Security
✅ Deployment Strategies
✅ Spring Cloud
✅ Production Architecture
✅ Interview Preparation
