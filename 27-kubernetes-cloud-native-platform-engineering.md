# Chapter 17 - Kubernetes, Cloud Native & Platform Engineering (Principal Engineer Edition)

## Learning Objectives

- Understand Kubernetes internals
- Master container orchestration
- Understand Service Mesh architecture
- Learn GitOps and Platform Engineering
- Understand SRE principles
- Design cloud-native systems
- Operate production Kubernetes clusters

---

# 1. Cloud Native Fundamentals

Cloud Native systems are:

- Resilient
- Observable
- Scalable
- Automated

Principles:

- Containers
- Microservices
- DevOps
- Continuous Delivery

---

# 2. Containers vs Virtual Machines

## Virtual Machine

```text
Hardware
 OS
 Hypervisor
 VM
 App
```

## Container

```text
Hardware
 OS
 Container Runtime
 Container
 App
```

Containers are lighter and faster.

---

# 3. Docker Fundamentals

Core Concepts:

- Image
- Container
- Registry
- Volume
- Network

---

# 4. Kubernetes Overview

Kubernetes (K8s) orchestrates containers.

Responsibilities:

- Scheduling
- Scaling
- Self-healing
- Service discovery

---

# 5. Kubernetes Architecture

```text
Control Plane
  ├─ API Server
  ├─ Scheduler
  ├─ Controller Manager
  └─ ETCD

Worker Nodes
  ├─ Kubelet
  ├─ Kube Proxy
  └─ Pods
```

---

# 6. API Server

Central entry point.

Every operation goes through API Server.

---

# 7. ETCD

Distributed key-value store.

Stores cluster state.

---

# 8. Scheduler

Decides:

```text
Which Node Runs Which Pod
```

---

# 9. Controller Manager

Continuously reconciles desired state.

---

# 10. Pod

Smallest deployable unit.

A pod may contain:

- One container
- Multiple tightly coupled containers

---

# 11. ReplicaSet

Maintains desired pod count.

---

# 12. Deployment

Provides:

- Rolling updates
- Rollbacks
- Replica management

---

# 13. StatefulSet

Used for stateful workloads.

Examples:

- Kafka
- Redis
- PostgreSQL

---

# 14. DaemonSet

Runs one pod per node.

Examples:

- Fluentd
- Node Exporter

---

# 15. Service

Networking abstraction.

Types:

- ClusterIP
- NodePort
- LoadBalancer

---

# 16. Ingress

HTTP entry point into cluster.

---

# 17. ConfigMap

Stores configuration.

---

# 18. Secret

Stores sensitive data.

Examples:

- Passwords
- API Keys

---

# 19. Horizontal Pod Autoscaler

Automatically scales pods.

Metrics:

- CPU
- Memory
- Custom metrics

---

# 20. Vertical Pod Autoscaler

Adjusts resource allocation.

---

# 21. Resource Management

Requests:

```text
Guaranteed Resources
```

Limits:

```text
Maximum Resources
```

---

# 22. Rolling Deployment

Zero downtime deployment strategy.

---

# 23. Blue Green Deployment

Two environments:

- Blue
- Green

Switch traffic instantly.

---

# 24. Canary Deployment

Release to small percentage first.

---

# 25. Service Mesh

Adds networking layer.

Capabilities:

- Traffic control
- Security
- Observability

---

# 26. Istio

Most popular Service Mesh.

Components:

- Envoy
- Control Plane

---

# 27. Envoy Proxy

Sidecar proxy beside application.

---

# 28. Observability

Three pillars:

- Logs
- Metrics
- Traces

---

# 29. Prometheus

Metrics collection platform.

---

# 30. Grafana

Visualization platform.

---

# 31. OpenTelemetry

Industry standard telemetry framework.

---

# 32. Distributed Tracing

Tools:

- Jaeger
- Tempo
- Zipkin

---

# 33. GitOps

Infrastructure managed via Git.

Benefits:

- Auditability
- Repeatability
- Automation

---

# 34. ArgoCD

Popular GitOps platform.

Continuously synchronizes Git and cluster.

---

# 35. Helm

Kubernetes package manager.

---

# 36. Operators

Automate application lifecycle.

Example:

- Kafka Operator
- Database Operator

---

# 37. Platform Engineering

Goal:

```text
Developer Self-Service Platform
```

---

# 38. Internal Developer Platform

Provides:

- CI/CD
- Deployment
- Monitoring
- Security

---

# 39. Site Reliability Engineering (SRE)

Created by Google.

Focus:

- Reliability
- Automation

---

# 40. SLA, SLO, SLI

SLA:
- Agreement

SLO:
- Objective

SLI:
- Measurement

---

# 41. Error Budget

Available risk allowance.

Used to balance:

- Innovation
- Reliability

---

# 42. Incident Management

Process:

```text
Detect
Respond
Mitigate
Recover
Review
```

---

# 43. Production Case Study: Netflix

- Multi-region deployment
- Chaos engineering
- Massive autoscaling

---

# 44. Production Case Study: Spotify

Platform model:

- Self-service
- Golden paths
- Developer productivity

---

# 45. Production Case Study: Uber

Uses:

- Kubernetes
- Microservices
- Kafka
- Observability stack

---

# 46. Principal Engineer Checklist

- Multi-region?
- RTO/RPO?
- Disaster recovery?
- Capacity planning?
- Security model?
- Cost optimization?

---

# 47. Principal Engineer Interview Questions

1. How Kubernetes scheduler works?
2. Deployment vs StatefulSet?
3. Service vs Ingress?
4. HPA vs VPA?
5. Why Service Mesh?
6. Istio architecture?
7. GitOps benefits?
8. Helm vs Kustomize?
9. What is an Operator?
10. Explain SLO and Error Budget.
11. Design multi-region deployment.
12. Design Internal Developer Platform.

---

# Chapter Summary

✅ Containers
✅ Docker
✅ Kubernetes Architecture
✅ Pods
✅ Deployments
✅ StatefulSets
✅ Services
✅ Ingress
✅ ConfigMap
✅ Secret
✅ Autoscaling
✅ Rolling Updates
✅ Canary Deployments
✅ Service Mesh
✅ Istio
✅ Envoy
✅ Prometheus
✅ Grafana
✅ OpenTelemetry
✅ GitOps
✅ ArgoCD
✅ Helm
✅ Operators
✅ Platform Engineering
✅ SRE
✅ SLA/SLO/SLI
✅ Incident Management
✅ Principal Interview Questions
