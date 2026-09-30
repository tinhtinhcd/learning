# Chapter 21 - Docker Containerization Masterclass

## Learning Objectives

- Understand container fundamentals and Docker internals
- Containerize Spring Boot applications
- Master Dockerfile and multi-stage builds
- Configure networking, storage, and Docker Compose
- Secure and optimize container images
- Prepare applications for Kubernetes and Cloud Native platforms
- Prepare for Senior Java and Tech Lead interviews

---

# Part I. Container Fundamentals

## What is a Container?

Container:

```text
Application
 ↓
Container Runtime
 ↓
Host OS
```

Virtual Machine:

```text
Application
 ↓
Guest OS
 ↓
Hypervisor
 ↓
Host OS
```

Benefits:
- Lightweight
- Fast startup
- Portable
- Resource efficient

---

# Part II. Docker Architecture

## Components

```text
Docker Client
    ↓
Docker Daemon
    ↓
Container Runtime
```

Key Concepts:
- Image
- Container
- Registry
- Volume
- Network

---

# Part III. Linux Container Internals

## Namespaces

Isolation types:
- PID
- Network
- Mount
- IPC
- UTS
- User

## cgroups

Resource management:
- CPU
- Memory
- Disk I/O

---

# Part IV. Docker Basics

## Images

```bash
docker images
```

## Containers

```bash
docker ps -a
```

## Run Container

```bash
docker run nginx
```

## Logs

```bash
docker logs container-id
```

## Execute Command

```bash
docker exec -it container-id bash
```

---

# Part V. Dockerfile Fundamentals

## Simple Spring Boot Dockerfile

```dockerfile
FROM eclipse-temurin:21-jre
COPY target/app.jar app.jar
ENTRYPOINT ["java","-jar","app.jar"]
```

## Build Image

```bash
docker build -t user-service .
```

## Run Image

```bash
docker run -p 8080:8080 user-service
```

---

# Part VI. Multi-Stage Builds

```dockerfile
FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

FROM eclipse-temurin:21-jre
COPY --from=build /app/target/*.jar app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

Benefits:
- Smaller images
- Improved security
- Faster deployment

---

# Part VII. Spring Boot Containerization

## Packaging

```bash
mvn clean package
```

## Environment Variables

```bash
docker run -e DB_HOST=mysql -e DB_PORT=3306 user-service
```

## JVM Options

```dockerfile
ENTRYPOINT ["java","-Xms256m","-Xmx512m","-jar","app.jar"]
```

---

# Part VIII. Docker Networking

## Bridge Network
Default network.

## Host Network
Uses host network stack.

## Overlay Network
Used in distributed environments.

## Custom Network

```bash
docker network create app-network
```

---

# Part IX. Docker Volumes

## Problem

```text
Container Deleted
 ↓
Data Lost
```

## Solution

```bash
docker volume create mysql-data
```

Mount:

```bash
docker run -v mysql-data:/var/lib/mysql mysql
```

---

# Part X. Docker Compose

## Spring Boot + Redis + MySQL

```yaml
services:
  app:
    build: .

  mysql:
    image: mysql:8

  redis:
    image: redis:7
```

Run:

```bash
docker compose up -d
```

Shutdown:

```bash
docker compose down
```

---

# Part XI. Image Optimization

## Best Practices

- Use JRE not JDK
- Use multi-stage builds
- Reduce layers
- Remove build artifacts

## Distroless Images

```dockerfile
FROM gcr.io/distroless/java21
```

Benefits:
- Smaller images
- Reduced attack surface

---

# Part XII. Security Hardening

## Non-root User

```dockerfile
RUN adduser appuser
USER appuser
```

## Read Only Filesystem

## Image Scanning

Tools:
- Trivy
- Docker Scout
- Snyk

## Secrets

Never:

```dockerfile
ENV DB_PASSWORD=secret
```

Use:
- Vault
- Secrets Manager
- Kubernetes Secrets

---

# Part XIII. Monitoring and Troubleshooting

## Resource Usage

```bash
docker stats
```

## Logs

```bash
docker logs app
```

## Inspect

```bash
docker inspect container-id
```

## Health Check

```dockerfile
HEALTHCHECK CMD curl -f http://localhost:8080/actuator/health
```

---

# Part XIV. Production Case Studies

## Java API + Redis + MySQL

```text
Spring Boot
   ↓
Redis
   ↓
MySQL
```

## Microservices Platform

```text
API Gateway
 ↓
User Service
Order Service
Payment Service
 ↓
Kafka
Redis
MySQL
```

---

# Part XV. Docker and Kubernetes

Relationship:

```text
Docker
 ↓
Container
 ↓
Kubernetes
```

Docker packages applications.

Kubernetes orchestrates containers.

---

# Part XVI. Common Production Issues

## Large Image Size

Solutions:
- Multi-stage builds
- Distroless images

## Memory OOM

Solutions:
- JVM tuning
- Container limits

## Slow Startup

Solutions:
- Layer optimization
- Reduce dependencies

---

# Part XVII. Interview Questions

1. Docker vs Virtual Machine?
2. Image vs Container?
3. What are Namespaces?
4. What are cgroups?
5. Why Multi-stage Build?
6. Volume vs Bind Mount?
7. Bridge vs Host Network?
8. Docker Compose vs Kubernetes?
9. Distroless Benefits?
10. How do you reduce image size?
11. Why run as non-root?
12. How do containers achieve isolation?

---

# Tech Lead Checklist

✅ Container Fundamentals
✅ Docker Architecture
✅ Linux Namespaces
✅ cgroups
✅ Dockerfile
✅ Multi-stage Build
✅ Spring Boot Containerization
✅ Docker Compose
✅ Networking
✅ Volumes
✅ Image Optimization
✅ Distroless Images
✅ Security Hardening
✅ Monitoring
✅ Troubleshooting
✅ Kubernetes Readiness
