# Chapter 13 - Spring AOP

## Learning Objectives

After completing this chapter, you will be able to:

- Understand AOP fundamentals
- Understand Spring Proxy architecture
- Master Pointcut expressions
- Understand Advice types
- Understand Advisor and Interceptor chains
- Understand Transaction AOP internals
- Diagnose Self Invocation issues
- Understand Proxy performance implications
- Troubleshoot AOP in production
- Answer Senior Spring interview questions

---

# 1. What is AOP?

AOP (Aspect Oriented Programming) separates:

```text
Business Logic
from
Cross-Cutting Concerns
```

Examples:

- Logging
- Security
- Transactions
- Audit
- Metrics

---

# 2. Why AOP Exists

Without AOP:

```java
log();
security();
transaction();
business();
```

repeated everywhere.

Benefits:

- Reusability
- Maintainability
- Separation of concerns

---

# 3. AOP Terminology

```text
Aspect
Advice
Join Point
Pointcut
Advisor
Proxy
Target
```

---

# 4. Join Point

A Join Point is a location where AOP can apply.

Spring AOP supports:

```text
Method Execution
```

only.

---

# 5. Pointcut

Defines where advice runs.

Example:

```java
execution(* com.app.service.*.*(..))
```

---

# 6. Advice

Defines what happens.

Examples:

```text
Before
After
Around
```

---

# 7. Aspect

Combination of:

```text
Pointcut + Advice
```

Example:

```java
@Aspect
@Component
```

---

# 8. Spring AOP Architecture

```text
Target Bean
    ↓
Proxy
    ↓
Advice Chain
```

---

# 9. Proxy Pattern

Spring AOP is Proxy-based.

Client talks to Proxy.

Proxy decides:

```text
Invoke Advice
Invoke Target
```

---

# 10. JDK Dynamic Proxy

Requirements:

```text
Interface Required
```

Uses:

```java
InvocationHandler
```

---

# 11. CGLIB Proxy

Works using subclass generation.

Advantages:

```text
No Interface Needed
```

Cannot proxy:

```text
final class
final method
```

---

# 12. Spring Proxy Selection

Rule:

```text
Interface -> JDK Proxy
No Interface -> CGLIB
```

---

# 13. Before Advice

Executes before method.

```java
@Before
```

---

# 14. After Advice

Executes after method completion.

```java
@After
```

---

# 15. After Returning

Runs only when successful.

```java
@AfterReturning
```

---

# 16. After Throwing

Runs when exception occurs.

```java
@AfterThrowing
```

---

# 17. Around Advice

Most powerful advice.

```java
@Around
```

Can:

- Continue execution
- Modify arguments
- Modify return value
- Stop execution

---

# 18. ProceedingJoinPoint

```java
joinPoint.proceed();
```

Controls target execution.

---

# 19. Pointcut Expressions

Examples:

```java
execution(* *(..))
```

```java
within(com.app..*)
```

```java
@annotation(Loggable)
```

---

# 20. Advisor

Combines:

```text
Advice + Pointcut
```

Spring internally builds Advisors.

---

# 21. MethodInterceptor

Core Spring AOP contract.

```java
MethodInterceptor
```

Foundation of many AOP features.

---

# 22. Interceptor Chain

Flow:

```text
Logging
  ↓
Security
  ↓
Transaction
  ↓
Business Method
```

---

# 23. Transaction AOP

@Transactional uses AOP.

Flow:

```text
Open Transaction
 ↓
Invoke Method
 ↓
Commit/Rollback
```

---

# 24. Transaction Proxy Internals

Actually executes:

```text
Client
 ↓
Proxy
 ↓
Transaction Advice
 ↓
Target
```

---

# 25. Self Invocation Problem

Example:

```java
this.save();
```

Problem:

```text
Bypasses Proxy
```

AOP will not trigger.

Interview favorite.

---

# 26. Common Self Invocation Solutions

- Refactor service
- Inject self proxy
- Use AspectJ

---

# 27. AOP and Exception Handling

Exceptions propagate through advice chain.

Useful for:

- Logging
- Metrics
- Audit

---

# 28. AOP and Security

Spring Security uses similar interception concepts.

Authorization checks happen before execution.

---

# 29. AOP and Caching

Example:

```java
@Cacheable
```

Implemented using proxy interception.

---

# 30. AOP and Validation

Example:

```java
@Validated
```

Intercepts method invocation.

---

# 31. Performance Considerations

Proxy overhead exists.

Usually small.

Impact grows with:

- Deep proxy chains
- Heavy reflection

---

# 32. Spring AOP vs AspectJ

Spring AOP:

```text
Proxy Based
Method Execution Only
```

AspectJ:

```text
Bytecode Weaving
More Powerful
```

---

# 33. Compile-Time Weaving

Aspect woven during build.

```text
ajc compiler
```

---

# 34. Load-Time Weaving

Aspect woven during class loading.

```text
javaagent
```

---

# 35. Production Issues

## AOP Not Triggered

Causes:

- Self invocation
- Private method
- Final method

---

## Transaction Not Working

Causes:

- Missing proxy
- Wrong bean access path

---

## Multiple Advice Execution

Check:

```text
Advisor Ordering
```

---

# 36. Debugging AOP

Useful checks:

```java
AopUtils.isAopProxy(bean)
```

```java
AopUtils.isJdkDynamicProxy(bean)
```

---

# 37. Real Production Cases

## Logging Aspect

Centralized audit logs.

## Performance Monitoring Aspect

Execution-time measurement.

## Transaction Aspect

Database consistency.

## Security Aspect

Authorization enforcement.

---

# Senior Interview Questions

1. What is AOP?
2. Why use AOP?
3. JoinPoint vs Pointcut?
4. Advice types?
5. Around advice vs Before advice?
6. JDK Proxy vs CGLIB?
7. How @Transactional works?
8. What is Self Invocation problem?
9. Advisor vs Advice?
10. MethodInterceptor role?
11. Spring AOP vs AspectJ?
12. Why final methods cannot be proxied?
13. How interceptor chain works?
14. How Spring chooses a proxy type?
15. How debug proxy issues?

---

# Chapter Summary

✅ AOP Fundamentals
✅ Proxy Pattern
✅ Join Point
✅ Pointcut
✅ Advice Types
✅ Aspect
✅ JDK Proxy
✅ CGLIB
✅ Advisor
✅ MethodInterceptor
✅ Interceptor Chain
✅ Transaction AOP
✅ Self Invocation
✅ Caching & Validation AOP
✅ Spring AOP vs AspectJ
✅ Weaving
✅ Production Troubleshooting
✅ Senior Interview Questions
