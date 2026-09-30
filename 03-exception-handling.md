# Chapter 3 - Exception Handling

## Learning Objectives

After completing this chapter, you will be able to:

- Understand Java Exception hierarchy
- Distinguish Error, Exception, Checked Exception, and Unchecked Exception
- Use try-catch-finally correctly
- Use throw and throws appropriately
- Create Custom Exceptions
- Implement exception handling in Spring Boot
- Design Global Exception Handling using @ControllerAdvice
- Apply exception handling best practices
- Avoid common exception anti-patterns
- Answer Senior Java interview questions confidently

---

# 1. Why Exception Handling Matters

Exception handling allows applications to gracefully respond to unexpected situations.

Goals:

- Prevent application crashes
- Provide meaningful error messages
- Maintain system stability
- Improve debugging and monitoring

Example:

```java
int result = 10 / 0;
```

Without exception handling:

```text
ArithmeticException
```

Application may terminate unexpectedly.

---

# 2. Exception Hierarchy

```text
Object
 └─ Throwable
     ├─ Error
     │   ├─ OutOfMemoryError
     │   ├─ StackOverflowError
     │   └─ VirtualMachineError
     │
     └─ Exception
         ├─ RuntimeException
         │   ├─ NullPointerException
         │   ├─ IllegalArgumentException
         │   ├─ IndexOutOfBoundsException
         │   └─ ClassCastException
         │
         └─ Checked Exception
             ├─ IOException
             ├─ SQLException
             └─ ParseException
```

---

# 3. Error vs Exception

## Error

Represents serious system-level problems.

Examples:

```java
OutOfMemoryError
StackOverflowError
```

Characteristics:

- Usually unrecoverable
- Application should not try to handle them

### Interview Question

Can we catch Error?

Answer:

Technically yes, but it is generally a bad practice because Errors indicate serious JVM-level problems.

---

## Exception

Represents recoverable problems.

Examples:

```java
IOException
SQLException
```

Should usually be handled or propagated.

---

# 4. Checked vs Unchecked Exceptions

## Checked Exception

Compiler forces handling.

Example:

```java
FileInputStream file =
    new FileInputStream("test.txt");
```

Must:

```java
try-catch
```

or

```java
throws
```

### Examples

```java
IOException
SQLException
ParseException
```

---

## Unchecked Exception

Extends:

```java
RuntimeException
```

Compiler does not force handling.

### Examples

```java
NullPointerException
IllegalArgumentException
NumberFormatException
```

### Interview Question

Checked vs Unchecked Exception?

Answer:

Checked exceptions are validated at compile time.
Unchecked exceptions occur at runtime and usually indicate programming errors.

---

# 5. try-catch-finally

## Basic Example

```java
try {
    int result = 10 / 0;
}
catch (ArithmeticException ex) {
    System.out.println(ex.getMessage());
}
finally {
    System.out.println("Cleanup");
}
```

Execution Flow:

1. try
2. catch (if exception occurs)
3. finally

---

## finally Block

Always executes.

Typical usage:

- Close resources
- Cleanup tasks

### Interview Question

Will finally always execute?

Answer:

Almost always.
Exceptions include JVM crash or System.exit().

---

# 6. throw vs throws

## throw

Used to explicitly create an exception.

```java
throw new IllegalArgumentException(
        "Invalid amount");
```

---

## throws

Declares potential exceptions.

```java
public void process()
        throws IOException {
}
```

---

## Interview Question

throw vs throws?

Answer:

throw is used to actually raise an exception.
throws declares that a method may produce an exception.

---

# 7. Multi-Catch

```java
try {
}
catch (IOException | SQLException ex) {
}
```

Benefits:

- Less duplication
- Cleaner code

---

# 8. try-with-resources

Introduced in Java 7.

Automatically closes resources.

```java
try (BufferedReader reader =
        new BufferedReader(...)) {

}
```

Equivalent to automatic cleanup.

Benefits:

- Prevent resource leaks
- Cleaner code

### Interview Question

Why prefer try-with-resources?

Answer:

Because it automatically closes resources and reduces the chance of resource leaks.

---

# 9. Custom Exceptions

## Why Create Custom Exceptions?

Provide domain-specific error information.

Example:

```java
public class InsufficientBalanceException
        extends RuntimeException {

    public InsufficientBalanceException(
            String message) {
        super(message);
    }
}
```

Usage:

```java
throw new InsufficientBalanceException(
        "Balance too low");
```

---

# 10. Exception Wrapping

Example:

```java
try {
}
catch (SQLException ex) {
    throw new ApplicationException(
            "Database error", ex);
}
```

Benefits:

- Preserve root cause
- Abstract implementation details

---

# 11. Best Practices

## Catch Specific Exceptions

Good:

```java
catch (IOException ex)
```

Avoid:

```java
catch (Exception ex)
```

unless truly necessary.

---

## Preserve Root Cause

Good:

```java
throw new ServiceException(
        "Failure", ex);
```

---

## Don't Swallow Exceptions

Bad:

```java
catch(Exception ex) {
}
```

Problem:

- Hidden failures
- Difficult debugging

---

## Log Exceptions Properly

Good:

```java
log.error("Failed", ex);
```

Avoid:

```java
log.error(ex.getMessage());
```

Stack trace lost.

---

# 12. Common Anti-Patterns

## Empty Catch Block

```java
catch(Exception ex) {
}
```

Bad practice.

---

## Overusing Checked Exceptions

Can make code harder to read and maintain.

---

## Catching Throwable

```java
catch(Throwable ex)
```

Almost always incorrect.

---

## Logging and Rethrowing Repeatedly

May create duplicate log entries.

---

# 13. Spring Boot Exception Handling

## Traditional Controller

```java
@GetMapping("/{id}")
public User getUser(Long id) {
    return service.find(id);
}
```

Problem:

Unhandled exceptions become generic 500 errors.

---

# 14. @ExceptionHandler

```java
@ExceptionHandler(
    UserNotFoundException.class)
public ResponseEntity<?> handle(
    UserNotFoundException ex) {

    return ResponseEntity
            .status(404)
            .body(ex.getMessage());
}
```

---

# 15. Global Exception Handling

## @ControllerAdvice

```java
@ControllerAdvice
public class GlobalExceptionHandler {
}
```

Benefits:

- Centralized handling
- Reusable responses
- Cleaner controllers

### Example

```java
@ExceptionHandler(
   UserNotFoundException.class)
```

Return:

```json
{
  "error":"USER_NOT_FOUND"
}
```

---

# 16. REST Error Response Design

Recommended Structure:

```json
{
  "timestamp":"2026-01-01",
  "errorCode":"USER_NOT_FOUND",
  "message":"User not found",
  "path":"/users/1"
}
```

Benefits:

- Standardized
- Easy client integration
- Easier debugging

---

# 17. Business Exception vs Technical Exception

## Business Exception

Examples:

```text
Insufficient Balance
Invalid Order State
```

Expected scenarios.

---

## Technical Exception

Examples:

```text
Database Connection Failed
OutOfMemoryError
Network Timeout
```

Infrastructure failures.

---

# 18. Interview Questions

## Q1. Checked vs Unchecked Exception?

Answer:

Checked exceptions are enforced by the compiler.
Unchecked exceptions extend RuntimeException and are not enforced.

---

## Q2. Exception vs Error?

Answer:

Exceptions are recoverable.
Errors indicate serious JVM-level problems.

---

## Q3. throw vs throws?

Answer:

throw raises an exception.
throws declares potential exceptions.

---

## Q4. Why use Custom Exceptions?

Answer:

To model domain-specific failures and improve readability.

---

## Q5. Why is @ControllerAdvice useful?

Answer:

It provides centralized exception handling and consistent API responses.

---

## Q6. Should services catch Exception?

Answer:

Generally no.
Catch only when recovery, transformation, or additional context is required.

---

## Q7. Why avoid catch(Exception)?

Answer:

It may hide important problems and make debugging difficult.

---

# 19. Exercises

## Exercise 1

Create a custom exception:

```java
UserNotFoundException
```

---

## Exercise 2

Create GlobalExceptionHandler using:

```java
@ControllerAdvice
```

---

## Exercise 3

Refactor file handling using:

```java
try-with-resources
```

---

## Exercise 4

Design standard API error response structure.

---

# Chapter Summary

✅ Throwable Hierarchy
✅ Error vs Exception
✅ Checked vs Unchecked
✅ try-catch-finally
✅ throw vs throws
✅ Multi-Catch
✅ try-with-resources
✅ Custom Exceptions
✅ Exception Wrapping
✅ Best Practices
✅ Anti-Patterns
✅ Spring Exception Handling
✅ @ExceptionHandler
✅ @ControllerAdvice
✅ REST Error Design
✅ Business vs Technical Exceptions
✅ Senior Interview Questions
