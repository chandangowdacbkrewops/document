# 01. API Design Guidelines

## Purpose

This document establishes the API design standards for the KrewOps Recruitment Platform. These guidelines ensure that all REST APIs follow consistent naming conventions, request and response formats, security practices, versioning strategies, and error-handling mechanisms across all services.

---

# Objectives

The API Guidelines aim to:

- Standardize REST API design.
- Improve API consistency.
- Simplify frontend integration.
- Support future API evolution.
- Enhance security.
- Improve maintainability.
- Reduce integration errors.

---

# REST Principles

The KrewOps Recruitment Platform follows RESTful architectural principles.

Core principles include:

- Resource-oriented APIs
- Stateless communication
- Client-server architecture
- Uniform interface
- Cacheable responses
- Layered system
- Standard HTTP methods

---

# API Base URL

Development

```text
http://localhost:8080/api/v1
```

QA

```text
https://qa-api.krewops.com/api/v1
```

Production

```text
https://api.krewops.com/api/v1
```

---

# URI Naming Convention

Guidelines

- Use nouns instead of verbs.
- Use lowercase letters.
- Use plural resource names.
- Use hyphens where necessary.
- Avoid underscores.
- Avoid file extensions.
- Keep URLs predictable.

Correct

```text
/users

/jobs

/candidates

/interviews

/companies
```

Incorrect

```text
/getUsers

/createJob

/deleteCandidate

/updateInterview
```

---

# Resource Hierarchy

Examples

```text
GET /companies

GET /companies/{companyId}

GET /companies/{companyId}/users

GET /jobs/{jobId}

GET /candidates/{candidateId}/applications
```

---

# HTTP Methods

| Method | Purpose | Idempotent |
|---------|----------|------------|
| GET | Retrieve resource | Yes |
| POST | Create resource | No |
| PUT | Replace resource | Yes |
| PATCH | Partial update | No |
| DELETE | Delete resource | Yes |

---

# HTTP Status Codes

| Status | Meaning |
|----------|----------|
| 200 | Success |
| 201 | Created |
| 202 | Accepted |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 405 | Method Not Allowed |
| 409 | Conflict |
| 422 | Validation Failed |
| 429 | Too Many Requests |
| 500 | Internal Server Error |
| 503 | Service Unavailable |

---

# Request Headers

Common request headers

```http
Authorization: Bearer <JWT>

Content-Type: application/json

Accept: application/json

Accept-Language: en-US

Correlation-Id: <UUID>
```

---

# Response Headers

Examples

```http
Content-Type: application/json

Cache-Control: no-cache

X-Request-Id

X-Correlation-Id

ETag
```

---

# Request Body Standards

All request payloads use JSON.

Example

```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@example.com"
}
```

---

# Response Body Standards

Success Response

```json
{
  "success": true,
  "message": "Candidate created successfully.",
  "data": {},
  "timestamp": "2026-08-01T10:00:00Z"
}
```

Error Response

```json
{
  "success": false,
  "message": "Validation failed.",
  "errors": [
    "Email is required."
  ],
  "timestamp": "2026-08-01T10:00:00Z"
}
```

---

# Naming Conventions

Resources

```text
/users

/jobs

/candidates

/interviews

/companies
```

Path Variables

```text
/users/{userId}

/jobs/{jobId}
```

Query Parameters

```text
?page=0

&size=20

&sort=createdDate

&status=ACTIVE
```

---

# Query Parameters

Filtering

```text
GET /jobs?status=OPEN
```

Searching

```text
GET /jobs?keyword=Java
```

Pagination

```text
GET /users?page=0&size=20
```

Sorting

```text
GET /users?sort=createdDate,desc
```

---

# Pagination Standard

Response Example

```json
{
  "content": [],
  "page": 0,
  "size": 20,
  "totalElements": 500,
  "totalPages": 25,
  "last": false
}
```

---

# Versioning

URI Versioning is adopted.

Examples

```text
/api/v1/users

/api/v2/users
```

Breaking changes require a new API version.

---

# Authentication

Protected APIs require JWT authentication.

```http
Authorization: Bearer eyJhbGci...
```

Public APIs

- Login
- Register
- Forgot Password
- Reset Password

---

# Authorization

Authorization follows Role-Based Access Control (RBAC).

Example roles

- Admin
- Recruiter
- Hiring Manager
- Interviewer
- Candidate

Permissions are evaluated before executing business logic.

---

# Idempotency

Operations that should be idempotent include:

```text
GET

PUT

DELETE
```

POST requests are generally non-idempotent unless an idempotency key is implemented.

---

# Validation Rules

Every request should validate:

- Required fields
- Data types
- Length
- Format
- Business rules
- Authorization
- Referential integrity

Validation failures return **400 Bad Request** or **422 Unprocessable Entity** depending on the validation stage.

---

# Error Handling

Standard error categories

- Validation Error
- Authentication Error
- Authorization Error
- Resource Not Found
- Business Exception
- Conflict
- Internal Server Error

Every error should include:

- Error Code
- Error Message
- Timestamp
- Correlation ID
- Request Path

---

# Security Guidelines

All APIs should:

- Use HTTPS.
- Require JWT authentication for protected resources.
- Validate all input.
- Prevent SQL Injection.
- Prevent Cross-Site Scripting (XSS).
- Sanitize request data.
- Log security events.
- Never expose sensitive information.

---

# Rate Limiting

Example limits

| API Type | Limit |
|----------|-------|
| Public APIs | 100 requests/minute |
| Authenticated APIs | 1000 requests/minute |
| Admin APIs | Configurable |

Exceeded limits return:

```http
429 Too Many Requests
```

---

# API Documentation Standards

Every endpoint should include:

- Endpoint URL
- HTTP Method
- Description
- Authentication
- Request Headers
- Request Parameters
- Request Body
- Response Body
- Success Codes
- Error Codes
- Validation Rules
- Example Request
- Example Response

---

# Logging Guidelines

Every request should log:

- Request ID
- Correlation ID
- HTTP Method
- Endpoint
- Execution Time
- Response Status

Sensitive information such as passwords and tokens must never be logged.

---

# API Lifecycle

```text
Design
   │
   ▼
Development
   │
   ▼
Testing
   │
   ▼
Documentation
   │
   ▼
Deployment
   │
   ▼
Monitoring
   │
   ▼
Versioning
```

---

# Best Practices

- Keep APIs resource-oriented.
- Use meaningful resource names.
- Follow standard HTTP semantics.
- Return appropriate status codes.
- Use pagination for large datasets.
- Validate all client input.
- Keep APIs backward compatible whenever possible.
- Maintain comprehensive API documentation.
- Secure every endpoint by default.

---

# Related Documents

- Software Architecture Document (SAD)
- Technical Design Document (TDD)
- Low-Level Design (LLD)
- Security Design
- API Documentation README

---

# Summary

These API Design Guidelines establish a consistent, secure, and maintainable approach for designing REST APIs within the KrewOps Recruitment Platform. By adhering to standardized URI conventions, HTTP semantics, authentication mechanisms, response formats, validation rules, and security best practices, the platform provides predictable and developer-friendly APIs that support long-term scalability and seamless integration.
