# API Documentation

**Project:** KrewOps Recruitment Platform

**Version:** 1.0

**Document Version:** 1.0

**Last Updated:** August 2026

---

# Purpose

This document provides the complete REST API specification for the KrewOps Recruitment Platform. It serves as the primary reference for frontend developers, backend developers, QA engineers, mobile application developers, DevOps engineers, and third-party integrators.

The API follows REST architectural principles and communicates using JSON over HTTPS.

---

# Scope

The API documentation covers:

- Authentication APIs
- User Management APIs
- Company Management APIs
- Job Management APIs
- Candidate Management APIs
- Application APIs
- Interview APIs
- Notification APIs
- Dashboard APIs
- Administration APIs
- Error Handling
- Pagination
- Filtering
- Sorting
- Rate Limiting
- API Versioning

---

# API Architecture

```text
                 Client
                    │
            HTTPS / REST
                    │
                    ▼
             API Gateway
                    │
                    ▼
          Spring Boot REST API
                    │
     ┌──────────────┼──────────────┐
     ▼              ▼              ▼
 Authentication  Business      Repository
     │            Services          │
     ▼              ▼              ▼
 Security        Kafka         PostgreSQL
                    │
                    ▼
                 Redis Cache
```

---

# Base URL

Development

```text
http://localhost:8080/api/v1
```

Testing

```text
https://qa-api.krewops.com/api/v1
```

Production

```text
https://api.krewops.com/api/v1
```

---

# API Versioning

Current Version

```text
v1
```

Example

```text
GET /api/v1/users
```

Future versions will be introduced as:

```text
/api/v2
/api/v3
```

Older versions will be supported according to the platform's API lifecycle policy.

---

# Authentication

All secured APIs require a JWT Bearer Token.

Example

```http
Authorization: Bearer <JWT_TOKEN>
```

Public APIs do not require authentication.

Examples include:

- Login
- Register
- Forgot Password
- Reset Password

---

# Content Type

Request

```http
Content-Type: application/json
```

Response

```http
Content-Type: application/json
```

---

# HTTP Methods

| Method | Purpose |
|----------|----------|
| GET | Retrieve data |
| POST | Create resources |
| PUT | Replace existing resource |
| PATCH | Partial update |
| DELETE | Remove resource |

---

# Standard Response Format

Success Response

```json
{
  "success": true,
  "message": "Operation completed successfully.",
  "data": {},
  "timestamp": "2026-08-01T10:00:00Z"
}
```

---

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
| 503 | Service Unavailable |

---

# Authentication Flow

```text
Client
   │
POST /auth/login
   │
   ▼
Authentication Service
   │
   ▼
JWT Token
   │
   ▼
Client Stores Token
   │
   ▼
Authorization Header
   │
   ▼
Protected APIs
```

---

# API Modules

The API is organized into the following modules.

| Module | Description |
|---------|-------------|
| Authentication | Login, Logout, Registration |
| Users | User Management |
| Companies | Company Management |
| Jobs | Job Management |
| Candidates | Candidate Management |
| Applications | Job Applications |
| Interviews | Interview Scheduling |
| Notifications | Email & System Notifications |
| Dashboard | Dashboard Metrics |
| Administration | Administrative Operations |

---

# Pagination

List APIs support pagination.

Example

```text
GET /users?page=0&size=20
```

Response

```json
{
  "content": [],
  "page": 0,
  "size": 20,
  "totalElements": 500,
  "totalPages": 25
}
```

---

# Sorting

Example

```text
GET /users?sort=createdDate,desc
```

Multiple sorting fields are supported.

---

# Filtering

Example

```text
GET /jobs?status=OPEN

GET /candidates?experience=5

GET /users?department=Engineering
```

---

# Search

Example

```text
GET /jobs/search?keyword=Java

GET /candidates/search?name=John
```

---

# Rate Limiting

To protect the platform against abuse, API requests are rate limited.

Typical limits:

- Anonymous APIs: 100 requests/minute
- Authenticated APIs: 1000 requests/minute
- Administrative APIs: Configurable

When limits are exceeded:

```http
429 Too Many Requests
```

---

# Security

The APIs implement:

- HTTPS
- JWT Authentication
- Role-Based Access Control (RBAC)
- Input Validation
- SQL Injection Prevention
- Cross-Site Scripting (XSS) Protection
- Secure Password Hashing
- Audit Logging

---

# Error Handling

All APIs return standardized error responses.

Categories include:

- Validation Errors
- Authentication Errors
- Authorization Errors
- Business Errors
- Resource Not Found
- Internal Server Errors

---

# Documentation Structure

```text
06-api-documentation/
│
├── README.md
├── 01-api-guidelines.md
├── 02-authentication-api.md
├── 03-user-api.md
├── 04-company-api.md
├── 05-job-api.md
├── 06-candidate-api.md
├── 07-application-api.md
├── 08-interview-api.md
├── 09-notification-api.md
├── 10-dashboard-api.md
├── 11-admin-api.md
├── 12-common-response.md
├── 13-error-codes.md
├── 14-pagination-filtering.md
├── 15-rate-limiting.md
├── 16-api-versioning.md
├── 17-openapi-swagger.md
└── 18-appendix.md
```

---

# Best Practices

- Use HTTPS for all communications.
- Authenticate before accessing protected APIs.
- Validate all request payloads.
- Use pagination for list endpoints.
- Handle API errors gracefully.
- Use idempotent HTTP methods where applicable.
- Follow semantic versioning.
- Log API requests and responses responsibly.
- Never expose sensitive information in responses.

---

# Related Documents

- Software Architecture Document (SAD)
- Technical Design Document (TDD)
- Low-Level Design (LLD)
- Deployment Guide
- Security Design
- Database Design

---

# Summary

This document serves as the central reference for all REST APIs exposed by the KrewOps Recruitment Platform. It defines API conventions, authentication mechanisms, response formats, security standards, and module-specific documentation to ensure consistent integration across frontend applications, mobile clients, and third-party systems. Subsequent chapters provide detailed specifications for each API module, including request/response models, validation rules, error codes, and usage examples.
