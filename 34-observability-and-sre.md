# Chapter 34 - Observability And SRE

## Learning Objectives

- Understand Monitoring vs Observability
- Master Metrics, Logs and Traces
- Implement OpenTelemetry in modern systems
- Design SLI, SLO, SLA and Error Budgets
- Understand Google SRE principles
- Build production-grade observability platforms
- Operate reliable cloud-native systems
- Prepare for Architect and Principal Engineer interviews

---

# Part I. Introduction to Observability

## What is Observability?

Observability measures how easily internal system state can be understood from external outputs.

Observability enables engineers to answer:

```text
What happened?
Why did it happen?
How do we prevent it?
```

---

## Monitoring vs Observability

Monitoring:

```text
Known Unknowns
```

Observability:

```text
Unknown Unknowns
```

Monitoring alerts.

Observability explains.

---

# Part II. Three Pillars of Observability

## Metrics

Numerical measurements over time.

Examples:
- CPU Usage
- Memory Usage
- Request Rate
- Error Rate
- Latency

---

## Logs

Recorded events.

Examples:
- User Login
- Transaction Failure
- Service Restart

---

## Traces

Track requests across systems.

```text
Gateway
 ↓
Order Service
 ↓
Payment Service
 ↓
Notification Service
```

---

# Part III. Metrics Deep Dive

## Golden Signals

Google SRE Four Golden Signals:

- Latency
- Traffic
- Errors
- Saturation

---

## RED Method

For APIs:

- Rate
- Errors
- Duration

---

## USE Method

For Infrastructure:

- Utilization
- Saturation
- Errors

---

# Part IV. Logging

## Structured Logging

Bad:

```text
Payment failed
```

Good:

```json
{
  "service":"payment",
  "orderId":"1001",
  "status":"FAILED"
}
```

---

## Log Levels

- TRACE
- DEBUG
- INFO
- WARN
- ERROR

---

# Part V. Centralized Logging

Architecture:

```text
Application
 ↓
Fluent Bit
 ↓
Loki / Elasticsearch
 ↓
Grafana / Kibana
```

Tools:

- ELK Stack
- OpenSearch
- Loki

---

# Part VI. Distributed Tracing

## Why Tracing?

Microservices increase complexity.

```text
Client
 ↓
Gateway
 ↓
Order
 ↓
Payment
 ↓
Inventory
```

Need end-to-end visibility.

---

## Trace Components

### Trace
Entire journey.

### Span
Single operation.

### Context Propagation
Links all spans together.

---

# Part VII. OpenTelemetry

## Open Standard

Provides:

- Metrics
- Logs
- Traces

---

## Architecture

```text
Application
 ↓
OTel SDK
 ↓
OTel Collector
 ↓
Backend Systems
```

---

# Part VIII. Prometheus

## Metrics Collection

Spring Boot metrics:

```text
http_requests_total
jvm_memory_used_bytes
jvm_gc_pause_seconds
```

---

## Actuator Integration

```text
/actuator/prometheus
```

---

# Part IX. Grafana

## Dashboarding

Typical Dashboard:

- CPU
- Memory
- Latency
- Error Rate
- Throughput

---

# Part X. JVM Observability

Monitor:

## Heap Memory

- Used Heap
- Max Heap

## Garbage Collection

- Minor GC
- Major GC
- Pause Time

## Threads

- Active Threads
- Blocked Threads

## HikariCP

- Active Connections
- Connection Timeouts

---

# Part XI. Alerting

## Alert Design

Good Alert:

```text
Actionable
Accurate
Timely
```

---

## Alert Fatigue

Too many alerts reduce effectiveness.

---

# Part XII. SLI

## Service Level Indicator

Measured reliability metric.

Examples:

```text
Availability = 99.95%
P95 Latency = 250ms
```

---

# Part XIII. SLO

## Service Level Objective

Internal target.

Example:

```text
99.9% Availability
```

---

# Part XIV. SLA

## Service Level Agreement

Customer commitment.

Example:

```text
99.5% Availability
```

---

# Part XV. Error Budget

Example:

```text
SLO = 99.9%
```

Allowed downtime:

```text
0.1%
≈ 43 minutes/month
```

---

## Error Budget Strategy

Within budget:

```text
Release Features
```

Budget exhausted:

```text
Focus Reliability
```

---

# Part XVI. Site Reliability Engineering

## Goals

Balance:

```text
Innovation
+
Reliability
```

---

## SRE Responsibilities

- Reliability
- Automation
- Monitoring
- Capacity Planning
- Incident Response

---

# Part XVII. Toil Reduction

## What is Toil?

Manual repetitive work.

Examples:

- Manual deployment
- Restarting services
- Manual log investigation

Automation is preferred.

---

# Part XVIII. Incident Management

## Severity Model

- SEV1
- SEV2
- SEV3
- SEV4

---

## Incident Lifecycle

```text
Detect
 ↓
Triage
 ↓
Mitigate
 ↓
Recover
 ↓
Postmortem
```

---

# Part XIX. Blameless Postmortem

Questions:

- What happened?
- Why?
- Impact?
- Preventive actions?

Focus on systems, not people.

---

# Part XX. Capacity Planning

Monitor:

- CPU Growth
- Memory Growth
- Storage Growth
- Traffic Growth

Forecast future requirements.

---

# Part XXI. Reliability Patterns

## Retry

## Circuit Breaker

## Timeout

## Bulkhead

## Rate Limiting

---

# Part XXII. Production Readiness Review

Checklist:

✅ Health Check

✅ Metrics

✅ Logs

✅ Traces

✅ Dashboards

✅ Alerts

✅ Load Testing

✅ Security Review

✅ Backup Strategy

✅ Runbooks

---

# Part XXIII. Observability Architecture

```text
Spring Boot
      ↓
Micrometer
      ↓
OpenTelemetry
      ↓
Collector

      ↓
Prometheus
Grafana
Loki
Tempo

      ↓
AlertManager
PagerDuty
```

---

# Part XXIV. Interview Questions

1. Monitoring vs Observability?
2. Three Pillars of Observability?
3. What is Distributed Tracing?
4. What is OpenTelemetry?
5. Explain Prometheus Architecture.
6. What is SLI?
7. SLI vs SLO vs SLA?
8. What is Error Budget?
9. What is SRE?
10. Explain Four Golden Signals.
11. How do you investigate production latency?
12. How do you design an observability platform?

---

# SRE Checklist

✅ Metrics
✅ Logs
✅ Traces
✅ OpenTelemetry
✅ Prometheus
✅ Grafana
✅ Alerting
✅ SLI
✅ SLO
✅ SLA
✅ Error Budgets
✅ Capacity Planning
✅ Incident Management
✅ Postmortem
✅ Reliability Engineering
✅ Production Operations
