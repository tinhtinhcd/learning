# Chapter 14 - Spring MVC REST

## Learning Objectives

After completing this chapter, you will be able to:

- Understand Spring MVC architecture
- Master DispatcherServlet workflow
- Understand HandlerMapping and HandlerAdapter
- Build RESTful APIs correctly
- Understand HttpMessageConverter and Jackson
- Implement validation and exception handling
- Understand Filters and Interceptors
- Understand asynchronous request processing
- Design production-grade REST APIs
- Troubleshoot Spring MVC applications

---

# 1. What is Spring MVC?

Spring MVC is Spring's web framework.

Responsibilities:

- Request handling
- Routing
- Validation
- Serialization
- Response generation

---

# 2. MVC Pattern

```text
Model
View
Controller
```

Controller receives request.

Model contains business data.

View renders output.

---

# 3. Spring MVC Architecture

```text
Client
  ↓
DispatcherServlet
  ↓
HandlerMapping
  ↓
Controller
  ↓
Service
  ↓
Repository
```

---

# 4. DispatcherServlet

Front Controller of Spring MVC.

All requests pass through it.

Responsibilities:

- Route requests
- Execute handlers
- Build responses

---

# 5. Request Lifecycle

```text
Request
 ↓
DispatcherServlet
 ↓
HandlerMapping
 ↓
HandlerAdapter
 ↓
Controller
 ↓
Response
```

---

# 6. HandlerMapping

Responsibility:

```text
Find Matching Controller
```

Example:

```java
@GetMapping("/users")
```

---

# 7. HandlerAdapter

Invokes controller method.

Adapts framework request into Java method calls.

---

# 8. @Controller

Returns:

```text
View Name
```

Example:

```java
@Controller
```

---

# 9. @RestController

Equivalent to:

```java
@Controller
@ResponseBody
```

Returns JSON directly.

---

# 10. REST Principles

REST emphasizes:

- Statelessness
- Resource orientation
- Standard HTTP methods
- Uniform API design

---

# 11. REST Resource Design

Good:

```http
GET /users
GET /users/1
```

Avoid:

```http
GET /getUser
```

---

# 12. HTTP Methods

```text
GET
POST
PUT
PATCH
DELETE
```

---

# 13. GET

Used for retrieval.

Must not modify state.

---

# 14. POST

Used for creation.

Example:

```http
POST /users
```

---

# 15. PUT vs PATCH

PUT:

```text
Full Update
```

PATCH:

```text
Partial Update
```

---

# 16. Request Mapping

```java
@RequestMapping
@GetMapping
@PostMapping
@PutMapping
@DeleteMapping
```

---

# 17. Path Variables

```java
@GetMapping("/{id}")
```

```java
@PathVariable
```

---

# 18. Query Parameters

```java
@RequestParam
```

Example:

```http
/users?page=1
```

---

# 19. Request Body

```java
@RequestBody
```

Automatically converts JSON to objects.

---

# 20. Response Body

```java
@ResponseBody
```

Converts object to JSON.

---

# 21. HttpMessageConverter

Responsible for:

```text
JSON ↔ Java Object
```

---

# 22. Jackson Integration

Default JSON library.

Responsibilities:

- Serialization
- Deserialization

---

# 23. Common Jackson Annotations

```java
@JsonProperty
@JsonIgnore
@JsonFormat
```

---

# 24. ResponseEntity

Provides full HTTP control.

```java
ResponseEntity.ok()
```

---

# 25. Validation

```java
@Valid
```

Bean Validation annotations:

```java
@NotNull
@Size
@Email
```

---

# 26. Global Exception Handling

```java
@RestControllerAdvice
```

Centralized exception management.

---

# 27. Exception Handler

```java
@ExceptionHandler
```

Converts exceptions into responses.

---

# 28. Filter

Servlet-level component.

Execution order:

```text
Before Spring MVC
```

---

# 29. Interceptor

Spring MVC component.

Methods:

```java
preHandle()
postHandle()
afterCompletion()
```

---

# 30. Filter vs Interceptor

Filter:
- Servlet based
- Earlier execution

Interceptor:
- Spring aware
- Controller focused

---

# 31. Async Processing

```java
@Async
```

or

```java
Callable
CompletableFuture
```

---

# 32. DeferredResult

Allows asynchronous HTTP processing.

Useful for long operations.

---

# 33. Server Sent Events (SSE)

```text
Server → Client Streaming
```

Useful for notifications.

---

# 34. File Upload

```java
MultipartFile
```

Common interview topic.

---

# 35. File Download

Return:

```java
Resource
ResponseEntity
```

---

# 36. API Versioning

Strategies:

```text
URI Versioning
Header Versioning
Query Versioning
```

---

# 37. Pagination

Example:

```http
/users?page=1&size=20
```

---

# 38. REST Error Response Design

Typical fields:

```json
{
  "code":"USER_NOT_FOUND",
  "message":"User not found"
}
```

---

# 39. REST Best Practices

- Use nouns
- Proper HTTP status codes
- Consistent response formats
- Pagination support
- Validation
- Global exception handling

---

# 40. Common HTTP Status Codes

```text
200 OK
201 Created
400 Bad Request
401 Unauthorized
403 Forbidden
404 Not Found
500 Internal Server Error
```

---

# 41. Production Troubleshooting

## 404 Error

Possible causes:

- Wrong mapping
- Context path issue

---

## 415 Unsupported Media Type

Wrong Content-Type.

---

## 400 Bad Request

Validation or binding issues.

---

## JSON Serialization Error

Check Jackson annotations.

---

# 42. Performance Optimization

- Enable compression
- Use pagination
- Avoid over-fetching
- Cache responses
- Use async processing when needed

---

# 43. Senior Interview Questions

1. How DispatcherServlet works?
2. HandlerMapping vs HandlerAdapter?
3. @Controller vs @RestController?
4. PUT vs PATCH?
5. Filter vs Interceptor?
6. How Jackson works?
7. What is HttpMessageConverter?
8. How validation works?
9. How exception handling works?
10. How async requests work?
11. How implement API versioning?
12. How design REST APIs?
13. How troubleshoot 404 errors?
14. Why use ResponseEntity?
15. How Spring converts JSON?

---

# Chapter Summary

✅ Spring MVC Architecture
✅ DispatcherServlet
✅ HandlerMapping
✅ HandlerAdapter
✅ Controller vs RestController
✅ REST Principles
✅ HTTP Methods
✅ Request Mapping
✅ Path Variables
✅ RequestBody
✅ ResponseBody
✅ HttpMessageConverter
✅ Jackson
✅ Validation
✅ Exception Handling
✅ Filter
✅ Interceptor
✅ Async Processing
✅ SSE
✅ File Upload/Download
✅ API Versioning
✅ REST Best Practices
✅ Production Troubleshooting
✅ Senior Interview Questions
