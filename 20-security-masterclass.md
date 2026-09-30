# Chapter 16 - Security Masterclass (Advanced Tech Lead Edition)

## Learning Objectives

After completing this chapter, you will:

- Understand modern application security principles
- Master Spring Security and JWT authentication
- Design OAuth2 and OpenID Connect architectures
- Implement OAuth2 Resource Server in Spring Boot
- Understand Refresh Token Rotation and Token Reuse Detection
- Secure microservices and APIs
- Apply OWASP Top 10 mitigations
- Prepare for Senior Java and Tech Lead interviews

---

# Part I. Security Fundamentals

## CIA Triad

### Confidentiality
Protect data from unauthorized access.

Examples:
- Encryption
- Access Control
- Data Classification

### Integrity
Protect data from unauthorized modification.

Examples:
- Checksums
- Hashing
- Digital Signatures

### Availability
Ensure systems remain accessible.

Examples:
- Failover
- Replication
- Load Balancing

---

# Part II. Authentication vs Authorization

## Authentication
Who are you?

Methods:
- Password
- OTP
- MFA
- Biometric

## Authorization
What are you allowed to do?

Examples:
- USER
- ADMIN
- MANAGER

---

# Part III. Password Security

## BCrypt

```java
@Bean
PasswordEncoder passwordEncoder() {
    return new BCryptPasswordEncoder();
}
```

## Argon2

Recommended modern password hashing algorithm.

Best Practices:
- Never store plain text passwords
- Use password hashing only
- Enable MFA for sensitive systems

---

# Part IV. JWT Authentication

## JWT Structure

```text
Header.Payload.Signature
```

## Claims

Standard Claims:
- sub
- iss
- exp
- aud

Custom Claims:
- role
- department

## Generate JWT

```java
String token = Jwts.builder()
    .subject(username)
    .claim("role", "ADMIN")
    .signWith(secretKey)
    .compact();
```

## Validate JWT

```java
String user = Jwts.parser()
    .verifyWith(secretKey)
    .build()
    .parseSignedClaims(token)
    .getPayload()
    .getSubject();
```

## JWT Best Practices

- HTTPS only
- Short expiration
- Use refresh tokens
- Do not store secrets in claims

---

# Part V. Spring Security Deep Dive

## Security Filter Chain

```text
Request
 ↓
Filter Chain
 ↓
Authentication
 ↓
Authorization
 ↓
Controller
```

## Stateless Security

```java
.sessionCreationPolicy(
    SessionCreationPolicy.STATELESS
)
```

## UserDetailsService

```java
@Service
public class CustomUserDetailsService
implements UserDetailsService {
}
```

## Method Security

```java
@EnableMethodSecurity
```

## Role Protection

```java
@PreAuthorize("hasRole('ADMIN')")
```

---

# Part VI. RBAC

## Role Based Access Control

Roles:
- ADMIN
- MANAGER
- USER

Benefits:
- Simple
- Easy governance

---

# Part VII. ABAC

## Attribute Based Access Control

Based on:
- Role
- Department
- Ownership
- Location
- Time

Example:

```text
ROLE = MANAGER
AND
DEPARTMENT = FINANCE
```

---

# Part VIII. OAuth2

## OAuth2 Actors

- Resource Owner
- Client
- Resource Server
- Authorization Server

## Authorization Code Flow

```text
User
 ↓
Authorization Server
 ↓
Authorization Code
 ↓
Access Token
```

## Client Credentials Flow

```text
Service
 ↔
 Service
```

## PKCE

Recommended for SPA and Mobile applications.

---

# Part IX. OpenID Connect (OIDC)

OIDC extends OAuth2 with authentication.

Additional Token:

```text
ID Token
```

Contains identity information.

---

# Part X. Keycloak

## Core Concepts

### Realm
Security domain.

### Client
Application.

### User
User identity.

### Role
Permission grouping.

## Typical Architecture

```text
User
 ↓
Keycloak
 ↓
JWT
 ↓
Spring Boot API
```

---

# Part XI. OAuth2 Resource Server

## Why Resource Server?

Avoid manually parsing JWT in every service.

## Dependency

```xml
<dependency>
 <artifactId>spring-boot-starter-oauth2-resource-server</artifactId>
</dependency>
```

## Configuration

```yaml
spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          issuer-uri: http://localhost:8080/realms/demo
```

## Security Configuration

```java
.oauth2ResourceServer(oauth2 -> oauth2.jwt())
```

## JWT Validation Flow

```text
Bearer Token
 ↓
Validate Signature
 ↓
Validate Expiration
 ↓
Validate Issuer
 ↓
Authorize Request
```

## Reading JWT Claims

```java
@GetMapping("/me")
public String me(@AuthenticationPrincipal Jwt jwt) {
    return jwt.getSubject();
}
```

## Advantages

- Standards compliant
- Less custom code
- Better Keycloak integration

---

# Part XII. Refresh Token Rotation

## Problem

Traditional refresh tokens remain valid for long periods.

Risk:

```text
Token Theft
 ↓
Unlimited Refresh Requests
```

## Rotation Concept

```text
RT1
 ↓
RT2
 ↓
RT3
```

Each refresh invalidates the previous token.

## Token Family

```text
RT1
 ↓
RT2
 ↓
RT3
 ↓
RT4
```

## Token Reuse Detection

If RT2 is reused after RT3 issuance:

```text
Security Alert
 ↓
Revoke Token Family
```

## Entity Example

```java
@Entity
class RefreshToken {
  String token;
  boolean revoked;
}
```

## Best Practice

Access Token:
- 15 minutes

Refresh Token:
- 7 to 30 days

---

# Part XIII. OWASP Top 10

## SQL Injection
Use prepared statements.

## XSS
Validate and encode output.

## CSRF
Use tokens and same-site cookies.

## SSRF
Validate outbound destinations.

## Broken Access Control
Validate permissions server-side.

---

# Part XIV. API Security

## API Key

```http
X-API-KEY
```

## JWT Authentication

```http
Authorization: Bearer token
```

## Rate Limiting

Protect APIs against abuse.

---

# Part XV. HTTPS and TLS

## HTTPS

```text
HTTP + TLS
```

## TLS Handshake

```text
Client
 ↓
Certificate Validation
 ↓
Key Exchange
 ↓
Encrypted Channel
```

---

# Part XVI. Mutual TLS (mTLS)

## Concept

```text
Client Certificate
+
Server Certificate
```

Use Cases:
- Banking
- Internal Microservices
- B2B APIs

---

# Part XVII. Secrets Management

Solutions:
- HashiCorp Vault
- AWS Secrets Manager
- Azure Key Vault

Never hardcode passwords.

---

# Part XVIII. Zero Trust

Principles:
- Never Trust
- Always Verify
- Least Privilege
- Assume Breach

---

# Part XIX. Security Monitoring

Monitor:
- Failed Logins
- Access Denied Events
- Token Reuse Events
- API Abuse

Tools:
- SIEM
- ELK
- Grafana

---

# Part XX. Incident Response

```text
Detect
 ↓
Contain
 ↓
Eradicate
 ↓
Recover
 ↓
Postmortem
```

---

# Part XXI. Microservices Security

Architecture:

```text
Client
 ↓
API Gateway
 ↓
JWT Validation
 ↓
Microservices
```

Service-to-Service Security:
- OAuth2 Client Credentials
- JWT
- mTLS

---

# Part XXII. Security Testing

## SAST
Static Analysis.

## DAST
Dynamic Analysis.

## Dependency Scanning

Tools:
- OWASP Dependency Check
- Snyk
- Trivy

---

# Part XXIII. Production Security Checklist

✅ MFA
✅ HTTPS
✅ JWT
✅ Refresh Token Rotation
✅ RBAC
✅ Audit Logs
✅ Vault
✅ Rate Limiting
✅ Security Monitoring
✅ Incident Response

---

# Part XXIV. Interview Questions

1. JWT vs Session?
2. OAuth2 vs OIDC?
3. What is Resource Server?
4. Why Refresh Token Rotation?
5. RBAC vs ABAC?
6. What is CSRF?
7. What is XSS?
8. Why HTTPS?
9. What is mTLS?
10. How would you secure Spring Boot Microservices?

---

# Tech Lead Checklist

✅ Spring Security
✅ JWT
✅ OAuth2
✅ OIDC
✅ Keycloak
✅ OAuth2 Resource Server
✅ Refresh Token Rotation
✅ OWASP Top 10
✅ API Security
✅ TLS and mTLS
✅ Secrets Management
✅ Zero Trust
✅ Security Monitoring
✅ Incident Response
✅ Microservices Security
