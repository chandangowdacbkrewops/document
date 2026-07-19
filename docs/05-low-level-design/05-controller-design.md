# 05. Controller Design

## Purpose

This chapter defines the design of the Controller layer for the KrewOps Recruitment Platform. Controllers act as the entry point to the application by exposing REST APIs, validating client requests, invoking business services, and returning standardized HTTP responses.

The Controller layer contains no business logic and delegates all processing to the Service layer.

---

# Objectives

The Controller Design aims to:

- Expose RESTful APIs.
- Accept and validate client requests.
- Delegate business operations to the Service layer.
- Return standardized API responses.
- Handle HTTP status codes.
- Support API versioning.
- Generate OpenAPI/Swagger documentation.
- Maintain thin controllers with no business logic.

---

# Controller Architecture

```text
                 Client
                    │
                    ▼
         HTTP Request (JSON)
                    │
                    ▼
        ┌─────────────────────┐
        │     Controller      │
        └─────────┬───────────┘
                  │
                  ▼
        ┌─────────────────────┐
        │      Service        │
        └─────────┬───────────┘
                  │
                  ▼
        Repository / Database
                  │
                  ▼
         HTTP Response (JSON)
```

The Controller layer is responsible only for request processing and response generation.

---

# Responsibilities

Controllers are responsible for:

- Exposing REST endpoints.
- Receiving HTTP requests.
- Parsing request bodies.
- Validating request data.
- Calling business services.
- Returning HTTP responses.
- Handling path variables.
- Handling query parameters.
- Pagination support.
- Sorting support.
- API documentation.

Controllers should never:

- Contain business logic.
- Access repositories directly.
- Execute SQL queries.
- Perform complex calculations.
- Manage transactions.

---

# Package Structure

```text
controller
│
├── AuthController
├── UserController
├── CandidateController
├── JobController
├── InterviewController
├── CompanyController
├── DashboardController
└── NotificationController
```

Each controller manages a specific business domain.

---

# Controller Naming Convention

Controllers follow the naming pattern:

```text
<Resource>NameController
```

Examples:

```text
UserController
CandidateController
JobController
InterviewController
CompanyController
```

---

# REST Endpoint Design

Each controller exposes RESTful endpoints following standard HTTP methods.

| HTTP Method | Purpose |
|--------------|----------|
| GET | Retrieve resource |
| POST | Create resource |
| PUT | Update entire resource |
| PATCH | Partial update |
| DELETE | Remove resource |

---

# Sample REST Endpoints

## UserController

```text
GET     /api/v1/users
GET     /api/v1/users/{id}
POST    /api/v1/users
PUT     /api/v1/users/{id}
DELETE  /api/v1/users/{id}
```

---

## CandidateController

```text
GET     /api/v1/candidates
GET     /api/v1/candidates/{id}
POST    /api/v1/candidates
PUT     /api/v1/candidates/{id}
DELETE  /api/v1/candidates/{id}
```

---

## JobController

```text
GET     /api/v1/jobs
GET     /api/v1/jobs/{id}
POST    /api/v1/jobs
PUT     /api/v1/jobs/{id}
DELETE  /api/v1/jobs/{id}
```

---

## InterviewController

```text
GET     /api/v1/interviews
GET     /api/v1/interviews/{id}
POST    /api/v1/interviews
PUT     /api/v1/interviews/{id}
DELETE  /api/v1/interviews/{id}
```

---

# Controller Template

```text
@RestController
@RequestMapping("/api/v1/users")
@RequiredArgsConstructor

UserController
        │
        ├── createUser()
        ├── getUser()
        ├── getUsers()
        ├── updateUser()
        └── deleteUser()
```

Every controller follows a consistent structure to improve maintainability.

---

# Request Validation

Controllers validate incoming requests using Bean Validation.

Common validation annotations include:

```text
@NotNull

@NotBlank

@Email

@Pattern

@Size

@Positive

@Min

@Max
```

Validation failures are handled by the Global Exception Handler.

---

# Request Processing Flow

```text
HTTP Request
      │
      ▼
Authentication
      │
      ▼
Validation
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
      ▼
Database
      │
      ▼
Response
```

---

# API Versioning

The platform follows URI-based versioning.

Examples:

```text
/api/v1/users

/api/v1/jobs

/api/v1/interviews
```

Future versions:

```text
/api/v2/users

/api/v3/users
```

---

# Pagination

Controllers support pagination using query parameters.

Example:

```text
GET /api/v1/jobs?page=0&size=20
```

Optional parameters include:

```text
page

size

sort

direction
```

---

# Filtering

Filtering is supported through query parameters.

Examples:

```text
GET /jobs?status=OPEN

GET /candidates?experience=5

GET /users?role=ADMIN
```

---

# Sorting

Sorting is supported using query parameters.

Example:

```text
GET /jobs?sort=createdDate,desc
```

---

# Response Structure

All APIs return a consistent response model.

Example:

```json
{
  "success": true,
  "message": "User created successfully",
  "data": {
    "id": 101,
    "name": "John Doe"
  },
  "timestamp": "2026-07-19T12:30:00Z"
}
```

---

# HTTP Status Codes

| Status | Description |
|----------|-------------|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 409 | Conflict |
| 422 | Validation Failed |
| 500 | Internal Server Error |

Controllers should return appropriate status codes based on the outcome of each request.

---

# Exception Handling

Controllers delegate exception handling to the Global Exception Handler.

Typical exceptions include:

- ValidationException
- ResourceNotFoundException
- UnauthorizedException
- BusinessException
- ConflictException

No controller should implement custom try-catch blocks for business exceptions.

---

# Security

Controller endpoints are protected using Spring Security.

Security responsibilities include:

- Authentication
- Authorization
- JWT validation
- Role-based access control
- Permission checks

Authorization is enforced before business logic execution.

---

# Swagger Documentation

Controllers are documented using OpenAPI annotations.

Documentation includes:

- Endpoint descriptions
- Request models
- Response models
- Error responses
- Authentication requirements

This enables automatic API documentation generation.

---

# Logging

Controllers should log only important request information.

Typical logs include:

- Request received
- Request completed
- Validation failure
- Authentication failure

Sensitive information such as passwords, tokens, and personal data must never be logged.

---

# Controller Best Practices

- Keep controllers lightweight.
- Delegate all business logic to services.
- Validate all incoming requests.
- Return consistent response structures.
- Use meaningful endpoint names.
- Avoid duplicate endpoints.
- Follow REST standards.
- Do not access repositories directly.
- Do not perform transaction management.
- Document every endpoint using OpenAPI.

---

# Benefits

The Controller Design provides:

- Clear separation of concerns.
- Consistent API design.
- Improved maintainability.
- Standardized request processing.
- Better validation.
- Simplified testing.
- Comprehensive API documentation.
- Secure endpoint management.

---

# Summary

The Controller Design establishes a clean and consistent API layer for the KrewOps Recruitment Platform. Controllers serve as the entry point for client applications, handling request validation, authentication, and response generation while delegating all business logic to the Service layer. This approach ensures a scalable, maintainable, secure, and well-documented REST API architecture.
