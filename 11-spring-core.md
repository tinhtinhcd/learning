# Chapter 9 - Spring Core (Complete Senior Edition)

## Learning Objectives

After completing this chapter, you will be able to:

- Understand Spring Framework architecture
- Master IoC and Dependency Injection
- Understand Bean Lifecycle
- Understand Bean Scopes
- Understand Configuration approaches
- Understand Component Scanning
- Understand Spring Container internals
- Understand Dependency Resolution
- Understand Circular Dependencies
- Understand Spring Events
- Understand Profiles and Environment
- Understand Spring AOP foundations
- Understand Spring Boot auto-configuration basics
- Answer Senior Spring interview questions

---

# 1. What is Spring?

Spring is a lightweight Java framework that provides:

- Dependency Injection
- Inversion of Control
- AOP
- Transaction Management
- Integration Support

Goals:

```text
Loose Coupling
Testability
Maintainability
```

---

# 2. Spring Architecture

```text
Spring Core
Spring AOP
Spring Data
Spring MVC
Spring Security
Spring Boot
```

Spring Core is the foundation.

---

# 3. Inversion of Control (IoC)

Traditional:

```java
UserService service = new UserService();
```

Spring:

```text
Container creates objects.
```

Benefits:

- Decoupling
- Easier testing

---

# 4. Dependency Injection (DI)

Dependencies are provided externally.

Example:

```java
@Service
class UserService {
  private final UserRepository repo;
}
```

---

# 5. Types of Dependency Injection

## Constructor Injection

Recommended.

```java
public UserService(UserRepository repo)
```

Benefits:

- Immutable dependencies
- Easy testing

---

## Setter Injection

Optional dependencies.

---

## Field Injection

```java
@Autowired
```

Generally discouraged.

---

# 6. Spring Container

Core containers:

```text
BeanFactory
ApplicationContext
```

---

# 7. BeanFactory vs ApplicationContext

BeanFactory:

- Basic container

ApplicationContext:

- Events
- AOP integration
- Internationalization

Most applications use ApplicationContext.

---

# 8. Bean Definition

Bean metadata includes:

- Class
- Scope
- Dependencies
- Lifecycle callbacks

---

# 9. Bean Creation Lifecycle

```text
Instantiate
 ↓
Populate Dependencies
 ↓
@PostConstruct
 ↓
Ready
 ↓
@PreDestroy
```

Interview favorite.

---

# 10. Bean Scopes

## Singleton

Default scope.

One bean per container.

---

## Prototype

New instance each request.

---

## Request

One bean per HTTP request.

---

## Session

One bean per user session.

---

# 11. Component Stereotypes

```java
@Component
@Service
@Repository
@Controller
```

All become Spring Beans.

---

# 12. Component Scanning

```java
@ComponentScan
```

Spring scans packages and registers beans.

---

# 13. Java Configuration

```java
@Configuration
```

```java
@Bean
```

Modern preferred approach.

---

# 14. XML Configuration

Legacy style.

Still appears in enterprise systems.

---

# 15. Autowiring

Modes:

```text
By Type
By Name
Qualifier
Primary
```

---

# 16. @Qualifier

Used when multiple beans exist.

```java
@Qualifier("mysqlRepository")
```

---

# 17. @Primary

Marks preferred bean candidate.

```java
@Primary
```

---

# 18. Circular Dependency

Example:

```text
A -> B
B -> A
```

Constructor injection exposes issues quickly.

---

# 19. Spring Bean Post Processor

Allows bean customization.

Interfaces:

```java
BeanPostProcessor
```

Used heavily by Spring.

---

# 20. Spring Events

Publisher:

```java
ApplicationEventPublisher
```

Listener:

```java
@EventListener
```

---

# 21. Environment & Profiles

Profiles:

```java
@Profile("dev")
```

Examples:

```text
dev
qa
prod
```

---

# 22. Externalized Configuration

```properties
application.properties
```

```yaml
application.yml
```

---

# 23. @Value

```java
@Value("${app.name}")
```

Injects configuration values.

---

# 24. ConfigurationProperties

Preferred for large configs.

```java
@ConfigurationProperties
```

Type-safe configuration.

---

# 25. Lazy Initialization

```java
@Lazy
```

Bean created when needed.

---

# 26. Spring AOP Foundation

Concept:

```text
Cross Cutting Concerns
```

Examples:

- Logging
- Security
- Transactions

---

# 27. AOP Terminology

```text
Aspect
Advice
Pointcut
Join Point
Proxy
```

---

# 28. Spring Proxy Mechanism

Uses:

```text
JDK Proxy
CGLIB
```

Covered in Chapter 8.

---

# 29. Spring Boot Auto Configuration

Goal:

```text
Convention Over Configuration
```

Annotation:

```java
@SpringBootApplication
```

---

# 30. Auto Configuration Internals

```text
Classpath Detection
 ↓
Condition Evaluation
 ↓
Bean Registration
```

---

# 31. Conditional Beans

```java
@ConditionalOnClass
```

```java
@ConditionalOnProperty
```

---

# 32. Dependency Resolution Process

```text
Find Candidates
 ↓
Apply Qualifiers
 ↓
Apply Primary
 ↓
Inject Dependency
```

---

# 33. Spring Container Startup

```text
Scan Classes
 ↓
Build Bean Definitions
 ↓
Create Beans
 ↓
Resolve Dependencies
```

---

# 34. Common Production Problems

## Bean Creation Exception

Missing dependency.

---

## Circular Dependency

Improper design.

---

## Multiple Bean Candidates

Need:

```java
@Qualifier
```

---

## Configuration Mismatch

Wrong profile or property.

---

# 35. Senior Interview Questions

1. What is IoC?
2. What is DI?
3. Constructor vs Field Injection?
4. BeanFactory vs ApplicationContext?
5. Bean lifecycle?
6. What is BeanPostProcessor?
7. What is @Primary?
8. What is @Qualifier?
9. What causes circular dependency?
10. How Spring creates beans?
11. How component scanning works?
12. What is Spring AOP?
13. How profiles work?
14. ConfigurationProperties vs Value?
15. How auto-configuration works?

---

# Chapter Summary

✅ Spring Architecture
✅ IoC
✅ Dependency Injection
✅ BeanFactory
✅ ApplicationContext
✅ Bean Lifecycle
✅ Bean Scopes
✅ Component Scan
✅ Java Config
✅ Autowiring
✅ Qualifier
✅ Primary
✅ Circular Dependency
✅ BeanPostProcessor
✅ Events
✅ Profiles
✅ ConfigurationProperties
✅ Spring AOP Basics
✅ Auto Configuration
✅ Dependency Resolution
✅ Production Issues
✅ Senior Interview Questions
