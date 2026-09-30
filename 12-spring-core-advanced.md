# Chapter 09.1 - Spring Core Advanced Internals

## Learning Objectives

After completing this chapter, you will understand:

- BeanFactory internals
- ApplicationContext startup sequence
- BeanDefinition lifecycle
- BeanFactoryPostProcessor
- BeanPostProcessor deep dive
- FactoryBean internals
- Circular dependency resolution
- Early Singleton Exposure
- CGLIB enhancement process
- Spring Context hierarchy
- Environment internals
- PropertySource resolution
- AutoConfiguration internals
- Custom Starter development
- Production startup optimization

---

# 1. Spring Container Architecture

```text
ApplicationContext
        ↓
BeanFactory
        ↓
DefaultListableBeanFactory
```

DefaultListableBeanFactory is the core engine behind most Spring applications.

---

# 2. BeanDefinition

BeanDefinition is metadata.

Contains:

- Bean Class
- Scope
- Dependencies
- Init Methods
- Destroy Methods

Spring creates objects from BeanDefinitions.

---

# 3. BeanDefinition Registry

Stores all registered BeanDefinitions.

```java
BeanDefinitionRegistry
```

Used during component scanning.

---

# 4. ApplicationContext Refresh Flow

```text
Prepare Context
 ↓
Load Bean Definitions
 ↓
Invoke BFPP
 ↓
Register BPP
 ↓
Instantiate Singletons
 ↓
Publish Events
```

Most important Spring startup flow.

---

# 5. BeanFactoryPostProcessor (BFPP)

Runs before bean creation.

Can modify:

```text
Bean Definitions
```

Example:

```java
PropertySourcesPlaceholderConfigurer
```

---

# 6. BeanPostProcessor (BPP)

Runs before and after bean initialization.

Methods:

```java
postProcessBeforeInitialization()
postProcessAfterInitialization()
```

Foundation of Spring AOP.

---

# 7. Bean Lifecycle Internal Flow

```text
Instantiate
 ↓
Populate Properties
 ↓
Aware Callbacks
 ↓
BPP Before
 ↓
@PostConstruct
 ↓
BPP After
 ↓
Ready
```

---

# 8. Aware Interfaces

Examples:

```java
BeanNameAware
ApplicationContextAware
EnvironmentAware
```

Allow beans to access Spring infrastructure.

---

# 9. FactoryBean

Special contract:

```java
FactoryBean<T>
```

Bean creates other beans.

Used by:

- MyBatis
- Feign
- Spring Proxies

---

# 10. FactoryBean vs BeanFactory

FactoryBean:

```text
Creates Bean Objects
```

BeanFactory:

```text
Container Itself
```

Common interview question.

---

# 11. Circular Dependency Problem

```text
A -> B
B -> A
```

Constructor injection cannot resolve automatically.

---

# 12. Early Singleton Exposure

Spring uses:

```text
Level 1 Cache
Level 2 Cache
Level 3 Cache
```

To resolve singleton circular references.

---

# 13. Three-Level Cache

```text
singletonObjects
earlySingletonObjects
singletonFactories
```

Critical interview topic.

---

# 14. Why Three-Level Cache Exists

Supports:

- Circular dependency resolution
- Proxy creation
- AOP integration

---

# 15. Spring Proxy Creation

Spring may replace bean:

```text
Target Bean
```

with:

```text
Proxy Bean
```

---

# 16. CGLIB Enhancement

@Configuration classes are enhanced.

Purpose:

```text
Ensure Singleton Behavior
```

---

# 17. @Configuration vs @Component

@Configuration:

```text
CGLIB Enhanced
```

@Component:

```text
No Enhancement
```

---

# 18. Environment Internals

Sources:

```text
System Variables
System Properties
application.yml
application.properties
```

---

# 19. PropertySource Resolution

Priority example:

```text
Command Line
 ↓
Environment Variable
 ↓
Application Config
```

---

# 20. Spring Profiles Internals

```java
@Profile("prod")
```

Bean created only when profile active.

---

# 21. Condition Evaluation Engine

Examples:

```java
@ConditionalOnClass
@ConditionalOnBean
@ConditionalOnProperty
```

Used heavily in Spring Boot.

---

# 22. AutoConfiguration Internals

Process:

```text
Classpath Scan
 ↓
Condition Check
 ↓
Configuration Import
 ↓
Bean Registration
```

---

# 23. AutoConfiguration.imports

Spring Boot 3 modern mechanism.

Defines auto-configurations loaded automatically.

---

# 24. Starter Architecture

Starter contains:

```text
Dependencies
Auto Configuration
Conditions
```

---

# 25. Custom Starter Development

Typical modules:

```text
starter
autoconfigure
```

Benefits:

- Reusable configuration
- Enterprise standardization

---

# 26. Spring Context Hierarchy

```text
Parent Context
      ↓
Child Context
```

Common in:

- Servlet Containers
- Spring MVC

---

# 27. Event Infrastructure

Components:

```text
Publisher
Event
Listener
```

Supports decoupled communication.

---

# 28. Startup Performance Optimization

Recommendations:

- Reduce component scanning
- Minimize reflection work
- Lazy initialization when needed
- Avoid unnecessary auto-configurations

---

# 29. Production Troubleshooting

## Slow Startup

Check:

- Bean Count
- AutoConfigurations
- Classpath Size

---

## Bean Creation Failure

Check:

- Missing dependency
- Wrong profile
- Circular references

---

## Memory Usage Growth

Check:

- Singleton caches
- Application context leaks

---

# 30. Real Production Cases

## Large Spring Boot Application

Problem:

```text
20+ second startup
```

Root Cause:

Excessive component scanning.

---

## Circular Dependency

Problem:

Application startup failure.

Root Cause:

Constructor injection cycle.

---

# Senior Interview Questions

1. What is DefaultListableBeanFactory?
2. What is BeanDefinition?
3. BFPP vs BPP?
4. FactoryBean vs BeanFactory?
5. Explain ApplicationContext refresh.
6. How Spring resolves circular dependencies?
7. Why three-level cache?
8. Why does @Configuration use CGLIB?
9. How auto-configuration works?
10. What is AutoConfiguration.imports?
11. How profiles work internally?
12. How property resolution works?
13. What causes slow startup?
14. What are Aware interfaces?
15. How Spring AOP relies on BPP?

---

# Chapter Summary

✅ DefaultListableBeanFactory
✅ BeanDefinition
✅ BeanDefinitionRegistry
✅ ApplicationContext Refresh
✅ BeanFactoryPostProcessor
✅ BeanPostProcessor
✅ FactoryBean
✅ Circular Dependency
✅ Three-Level Cache
✅ Early Singleton Exposure
✅ CGLIB Enhancement
✅ Environment Internals
✅ Property Resolution
✅ Profiles
✅ Conditional Engine
✅ AutoConfiguration
✅ AutoConfiguration.imports
✅ Starter Development
✅ Context Hierarchy
✅ Startup Optimization
✅ Production Troubleshooting
✅ Senior Interview Questions
