# 08. DTO Design

## Purpose

This chapter defines the Data Transfer Object (DTO) design for the KrewOps Recruitment Platform. DTOs are used to transfer data between the client and server while ensuring that internal domain entities remain isolated from external consumers. They improve security, maintainability, validation, and API consistency.

---

# Objectives

The DTO Design aims to:

- Separate API models from database entities.
- Prevent direct exposure of internal objects.
- Simplify request and response handling.
- Support validation.
- Improve API maintainability.
- Reduce payload size.
- Enable versioning without affecting entities.

---

# DTO Layer Architecture

```text
                Client
                   │
                   ▼
          Request DTO
                   │
                   ▼
             Controller
                   │
                   ▼
             Service Layer
                   │
                   ▼
                Mapper
                   │
                   ▼
                Entity
                   │
                   ▼
             Repository
                   │
                   ▼
              Database
                   │
                   ▼
                Entity
                   │
                   ▼
                Mapper
                   │
                   ▼
           Response DTO
                   │
                   ▼
                Client
```

DTOs act as the communication model between clients and the application.

---

# Responsibilities

DTOs are responsible for:

- Representing API requests.
- Representing API responses.
- Input validation.
- Output serialization.
- Encapsulating API contracts.
- Preventing entity exposure.

DTOs should **not**:

- Contain business logic.
- Access the database.
- Implement persistence.
- Perform calculations.
- Contain framework-specific business behavior.

---

# Package Structure

```text
dto
│
├── request
│   ├── CreateUserRequest
│   ├── UpdateUserRequest
│   ├── CreateJobRequest
│   ├── CreateCandidateRequest
│   └── ScheduleInterviewRequest
│
├── response
│   ├── UserResponse
│   ├── JobResponse
│   ├── CandidateResponse
│   ├── InterviewResponse
│   └── CompanyResponse
│
└── common
    ├── ApiResponse
    ├── PageResponse
    └── ErrorResponse
```

Request and response models are separated for clarity and maintainability.

---

# Request DTOs

Request DTOs capture input data submitted by API consumers.

Examples:

```text
CreateUserRequest

UpdateUserRequest

CreateCandidateRequest

UpdateCandidateRequest

CreateJobRequest

ScheduleInterviewRequest
```

Request DTOs include validation annotations to ensure data integrity before business processing.

---

# Response DTOs

Response DTOs define the data returned to clients.

Examples:

```text
UserResponse

CandidateResponse

JobResponse

InterviewResponse

CompanyResponse
```

Only required information should be exposed through response DTOs.

---

# Common Response Model

A standardized response wrapper ensures consistency across all APIs.

Example:

```json
{
  "success": true,
  "message": "Candidate created successfully",
  "data": {
    "id": 101,
    "name": "John Doe"
  },
  "timestamp": "2026-07-19T10:30:00Z"
}
```

---

# Validation

DTOs leverage Bean Validation annotations.

Common annotations include:

```java
@NotNull

@NotBlank

@NotEmpty

@Email

@Pattern

@Size

@Positive

@Min

@Max

@Past

@Future
```

Validation is automatically triggered in the Controller layer using `@Valid`.

---

# DTO Mapping

Entities and DTOs are converted using dedicated Mapper classes.

```text
Request DTO
      │
      ▼
Mapper
      │
      ▼
Entity
      │
      ▼
Repository
```

```text
Entity
      │
      ▼
Mapper
      │
      ▼
Response DTO
```

Mapping logic must not be implemented inside Controllers or Services.

---

# Example Mapping Flow

```text
CreateCandidateRequest
          │
          ▼
CandidateMapper
          │
          ▼
Candidate Entity
          │
          ▼
Database
          │
          ▼
Candidate Entity
          │
          ▼
CandidateMapper
          │
          ▼
CandidateResponse
```

---

# Nested DTOs

Complex resources may contain nested DTOs.

Example:

```text
CandidateResponse
│
├── Basic Information
├── Skills
├── Education
├── Experience
└── Certifications
```

Nested DTOs improve readability and maintain structured API responses.

---

# Pagination DTO

List APIs return paginated responses.

Example:

```json
{
  "content": [],
  "page": 0,
  "size": 20,
  "totalElements": 150,
  "totalPages": 8,
  "last": false
}
```

This standard format simplifies client-side pagination.

---

# Error Response DTO

Errors are returned using a common structure.

Example:

```json
{
  "success": false,
  "message": "Validation failed",
  "errors": [
    "Email is required",
    "Phone number is invalid"
  ],
  "timestamp": "2026-07-19T10:35:00Z"
}
```

A consistent error format improves API usability.

---

# Serialization

DTOs are serialized to JSON before being sent to clients.

Serialization guidelines:

- Exclude sensitive fields.
- Ignore null values where appropriate.
- Format dates consistently.
- Use meaningful property names.

---

# Sensitive Data Handling

DTOs must never expose:

- Passwords
- Authentication tokens
- Internal IDs (when unnecessary)
- Security credentials
- Audit metadata (unless required)
- Database-specific fields

Only information required by the client should be returned.

---

# Naming Conventions

| Component | Convention |
|------------|------------|
| Request DTO | CreateUserRequest |
| Update DTO | UpdateUserRequest |
| Response DTO | UserResponse |
| Common Response | ApiResponse |
| Error Response | ErrorResponse |
| Pagination Response | PageResponse |

---

# DTO Design Best Practices

- Keep DTOs immutable where possible.
- Separate request and response models.
- Avoid exposing entities.
- Use validation annotations.
- Keep DTOs lightweight.
- Avoid nested objects unless necessary.
- Reuse common response models.
- Keep API contracts stable.
- Document DTOs using OpenAPI annotations.

---

# Benefits

The DTO Design provides:

- Better API security.
- Loose coupling between layers.
- Cleaner architecture.
- Easier API evolution.
- Simplified validation.
- Improved maintainability.
- Consistent request and response structures.
- Better client integration.

---

# Summary

The DTO Design provides a structured and secure mechanism for transferring data between clients and the KrewOps Recruitment Platform. By separating API contracts from persistence models, incorporating validation, supporting standardized responses, and preventing exposure of internal entities, the DTO layer ensures a clean, maintainable, and scalable API architecture.
