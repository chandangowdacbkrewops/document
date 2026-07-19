# 11. Exception Handling Design

## Purpose

This chapter defines the Exception Handling Design for the KrewOps Recruitment Platform. A centralized exception handling mechanism ensures that application errors are captured, logged, translated into meaningful responses, and returned to clients in a consistent format while preventing leakage of internal implementation details.

---

# Objectives

The Exception Handling Design aims to:

- Handle application errors consistently.
- Improve API reliability.
- Provide meaningful error responses.
- Separate business exceptions from system exceptions.
- Prevent exposure of sensitive information.
- Simplify debugging and monitoring.
- Improve maintainability.

---

# Exception Handling Architecture

```text
               Client
                  │
                  ▼
             HTTP Request
                  │
                  ▼
             Controller
                  │
                  ▼
             Service Layer
                  │
                  ▼
           Repository Layer
                  │
                  ▼
             Exception Thrown
                  │
                  ▼
      Global Exception Handler
                  │
                  ▼
        Standard Error Response
                  │
                  ▼
                Client
```

---

# Exception Categories

The application classifies exceptions into the following categories:

| Category | Description |
|----------|-------------|
| Validation Exception | Invalid request data |
| Business Exception | Business rule violations |
| Authentication Exception | Invalid credentials |
| Authorization Exception | Access denied |
| Resource Not Found | Requested resource unavailable |
| Conflict Exception | Duplicate or conflicting data |
| Database Exception | Persistence failures |
| External Service Exception | Third-party integration failures |
| System Exception | Unexpected application errors |

---

# Exception Flow

```text
Request
   │
   ▼
Controller
   │
   ▼
Service
   │
   ▼
Repository
   │
 Exception
   │
   ▼
Global Exception Handler
   │
   ▼
HTTP Response
```

All unhandled exceptions are processed by a centralized exception handler.

---

# Global Exception Handler

The application uses a global exception handler to process all uncaught exceptions.

Example:

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

}
```

Responsibilities include:

- Capturing exceptions.
- Logging errors.
- Mapping exceptions to HTTP status codes.
- Returning standardized responses.

---

# Standard Error Response

Every API error follows a common response format.

Example:

```json
{
  "success": false,
  "status": 400,
  "error": "Validation Error",
  "message": "Email address is invalid",
  "path": "/api/v1/users",
  "timestamp": "2026-07-19T11:30:00Z"
}
```

---

# Validation Exceptions

Validation failures occur before business processing.

Examples:

- Missing required fields.
- Invalid email format.
- Invalid phone number.
- Invalid date.
- Negative salary.

HTTP Status:

```text
400 Bad Request
```

---

# Resource Not Found Exception

Thrown when requested resources do not exist.

Examples:

- User not found.
- Candidate not found.
- Company not found.
- Interview not found.
- Job not found.

HTTP Status:

```text
404 Not Found
```

---

# Business Exceptions

Business exceptions occur when domain rules are violated.

Examples:

- Candidate already applied.
- Interview already scheduled.
- Company subscription expired.
- Job is already closed.
- Duplicate email address.

HTTP Status:

```text
409 Conflict
```

---

# Authentication Exceptions

Authentication failures include:

- Invalid username.
- Invalid password.
- Expired token.
- Invalid JWT.
- Missing authentication credentials.

HTTP Status:

```text
401 Unauthorized
```

---

# Authorization Exceptions

Authorization failures occur when authenticated users lack permissions.

Examples:

- Insufficient privileges.
- Missing required role.
- Access denied.
- Restricted resource.

HTTP Status:

```text
403 Forbidden
```

---

# Database Exceptions

Database-related exceptions include:

- Constraint violations.
- Foreign key violations.
- Unique constraint failures.
- Transaction rollback.
- Optimistic locking failures.

HTTP Status:

```text
500 Internal Server Error
```

or

```text
409 Conflict
```

depending on the failure type.

---

# External Service Exceptions

Failures originating from external integrations.

Examples:

- Email service unavailable.
- SMS gateway failure.
- Payment provider timeout.
- Identity provider unavailable.

HTTP Status:

```text
503 Service Unavailable
```

---

# Generic System Exceptions

Unexpected runtime failures.

Examples:

- NullPointerException
- IllegalStateException
- RuntimeException
- Unknown errors

HTTP Status:

```text
500 Internal Server Error
```

Internal implementation details must never be exposed to clients.

---

# Exception Hierarchy

```text
RuntimeException
        │
        ├── ValidationException
        ├── BusinessException
        ├── ResourceNotFoundException
        ├── ConflictException
        ├── AuthenticationException
        ├── AuthorizationException
        ├── ExternalServiceException
        └── DatabaseException
```

A structured hierarchy simplifies exception management and promotes consistency.

---

# Logging Strategy

Every exception should be logged appropriately.

| Level | Usage |
|--------|-------|
| INFO | Expected business events |
| WARN | Recoverable validation failures |
| ERROR | Unexpected system failures |

Sensitive information such as passwords, authentication tokens, and personal data must never be written to logs.

---

# HTTP Status Mapping

| Exception | HTTP Status |
|-----------|-------------|
| ValidationException | 400 Bad Request |
| AuthenticationException | 401 Unauthorized |
| AuthorizationException | 403 Forbidden |
| ResourceNotFoundException | 404 Not Found |
| ConflictException | 409 Conflict |
| BusinessException | 409 Conflict |
| ExternalServiceException | 503 Service Unavailable |
| DatabaseException | 500 Internal Server Error |
| RuntimeException | 500 Internal Server Error |

---

# Error Handling Flow

```text
Exception
    │
    ▼
Log Error
    │
    ▼
Determine Exception Type
    │
    ▼
Map HTTP Status
    │
    ▼
Build Standard Error Response
    │
    ▼
Return Response
```

---

# Best Practices

- Use centralized exception handling.
- Create custom exceptions for business scenarios.
- Never expose stack traces to clients.
- Log unexpected exceptions.
- Return meaningful error messages.
- Map exceptions to appropriate HTTP status codes.
- Use standardized error response models.
- Keep exception messages concise and user-friendly.

---

# Benefits

The Exception Handling Design provides:

- Consistent API responses.
- Improved debugging.
- Better application reliability.
- Enhanced security.
- Cleaner business logic.
- Simplified maintenance.
- Better client experience.
- Easier production monitoring.

---

# Summary

The Exception Handling Design establishes a centralized and standardized approach to error management within the KrewOps Recruitment Platform. By categorizing exceptions, mapping them to appropriate HTTP status codes, logging failures consistently, and returning structured error responses, the application improves reliability, security, maintainability, and the overall API experience while protecting internal implementation details.
