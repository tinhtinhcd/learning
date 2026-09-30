# Chapter 33 - Cloud Architecture Fundamentals

## Learning Objectives

- Understand Cloud Computing Models
- Design scalable cloud-native systems
- Learn Networking, Security, and IAM concepts
- Master High Availability and Disaster Recovery
- Understand Containers, Kubernetes, and Serverless
- Apply Well-Architected Framework principles
- Prepare for Architect and Principal Engineer interviews

---

# Part I. Cloud Computing Fundamentals

## Cloud Service Models

### IaaS
- AWS EC2
- Azure VM
- Google Compute Engine

### PaaS
- Azure App Service
- Google App Engine

### SaaS
- Microsoft 365
- Salesforce

---

# Part II. Deployment Models

## Public Cloud
AWS, Azure, GCP

## Private Cloud
Internal infrastructure.

## Hybrid Cloud
Combination of on-premises and public cloud.

## Multi Cloud
Using multiple cloud providers.

---

# Part III. Compute Services

## Virtual Machines
Traditional infrastructure.

## Containers
Docker-based workloads.

## Kubernetes
Container orchestration platform.

## Serverless
- AWS Lambda
- Azure Functions
- Cloud Functions

---

# Part IV. Cloud Storage

## Object Storage
Examples:
- Amazon S3
- Azure Blob Storage
- Google Cloud Storage

## Block Storage
Examples:
- EBS
- Managed Disks

## File Storage
Examples:
- EFS
- Azure Files

---

# Part V. Databases

## Relational Databases
- RDS
- Aurora
- Cloud SQL

## NoSQL Databases
- DynamoDB
- CosmosDB
- Bigtable

---

# Part VI. Cloud Networking

## VPC
Private network inside cloud.

## Subnets
- Public Subnet
- Private Subnet

## Route Tables
Control traffic routing.

## NAT Gateway
Allow outbound internet access.

## Load Balancers
- Layer 4
- Layer 7

---

# Part VII. Identity and Access Management

## IAM
Authentication and Authorization.

## Least Privilege Principle
Grant only required permissions.

## Service Accounts
Used for workload authentication.

---

# Part VIII. Security Architecture

## Security Layers
- Network Security
- Identity Security
- Data Security
- Application Security

## Secrets Management
- AWS Secrets Manager
- Azure Key Vault
- HashiCorp Vault

---

# Part IX. High Availability

## Multi-AZ

```text
AZ1
AZ2
AZ3
```

Provides redundancy.

## Multi-Region

```text
Singapore
Tokyo
```

Provides disaster recovery.

---

# Part X. Scalability

## Vertical Scaling
Increase server resources.

## Horizontal Scaling
Add more instances.

## Auto Scaling
Scale based on demand.

---

# Part XI. Cloud Architecture Patterns

## Stateless Applications

## Caching Layer
Redis.

## Queue-Based Systems
Kafka, RabbitMQ.

## Event Driven Architecture

## CQRS Pattern

---

# Part XII. Cloud Native Architecture

Principles:
- Containers
- Microservices
- Automation
- Immutable Infrastructure

---

# Part XIII. Kubernetes Managed Services

## EKS
Amazon Kubernetes.

## AKS
Azure Kubernetes Service.

## GKE
Google Kubernetes Engine.

---

# Part XIV. Service Mesh

Examples:
- Istio
- Linkerd

Benefits:
- Traffic Management
- Security
- Observability

---

# Part XV. Serverless Architecture

## Benefits
- Pay per use
- No infrastructure management

## Challenges
- Cold start
- Vendor lock-in

---

# Part XVI. Well-Architected Framework

Pillars:
- Operational Excellence
- Security
- Reliability
- Performance Efficiency
- Cost Optimization
- Sustainability

---

# Part XVII. Cost Optimization & FinOps

## Common Waste
- Idle VMs
- Overprovisioned Databases
- Unused Storage

## FinOps Goals
- Visibility
- Accountability
- Optimization

---

# Part XVIII. Cloud Migration Strategies

## 6R Model
- Rehost
- Replatform
- Refactor
- Repurchase
- Retire
- Retain

---

# Part XIX. Landing Zone

Components:
- Accounts
- Networking
- Logging
- Monitoring
- IAM
- Security Controls

---

# Part XX. Multi-Tenant Architecture

## Shared Database

## Shared Schema

## Dedicated Deployment

Trade-off between cost and isolation.

---

# Part XXI. Disaster Recovery

## Metrics
- RTO
- RPO

## DR Strategies
- Backup & Restore
- Pilot Light
- Warm Standby
- Active-Active

---

# Part XXII. Cloud Interview Questions

1. IaaS vs PaaS vs SaaS?
2. What is a VPC?
3. Multi-AZ vs Multi-Region?
4. What is Auto Scaling?
5. EKS vs AKS vs GKE?
6. What is Serverless?
7. What is IAM?
8. How do you secure cloud workloads?
9. What is FinOps?
10. How would you design a highly available system?

---

# Cloud Architect Checklist

✅ Cloud Fundamentals
✅ Networking
✅ Storage
✅ Compute
✅ Security
✅ IAM
✅ High Availability
✅ Auto Scaling
✅ Kubernetes
✅ Service Mesh
✅ Serverless
✅ FinOps
✅ Disaster Recovery
✅ Cloud Migration
✅ Multi-Tenant Architecture
✅ Interview Preparation
