# 03. User API

## Purpose

This document defines the User Management APIs for the KrewOps Recruitment Platform. These APIs enable administrators and authorized users to create, retrieve, update, deactivate, activate, and manage user accounts within the platform.

The User API follows RESTful principles and supports pagination, filtering, sorting, searching, and role-based access control.

---

# Base URL

```text
/api/v1/users
```

---

# User Lifecycle

```text
Create User
      │
      ▼
Email Verification
      │
      ▼
Account Activated
      │
      ▼
Profile Updated
      │
      ▼
Role Assigned
      │
      ▼
Active User
      │
      ▼
Deactivate
      │
      ▼
Archive/Delete
```

---

# User APIs

| Method | Endpoint | Description |
|----------|---------------------------|-------------------------|
| POST | /users | Create User |
| GET | /users | Get All Users |
| GET | /users/{id} | Get User By ID |
| PUT | /users/{id} | Update User |
| PATCH | /users/{id}/status | Activate/Deactivate User |
| PATCH | /users/{id}/roles | Update User Roles |
| DELETE | /users/{id} | Delete User |
| GET | /users/search | Search Users |

---

# Create User

## Endpoint

```http
POST /api/v1/users
```

---

## Authorization

```text
ADMIN
HR_MANAGER
```

---

## Request Headers

```http
Authorization: Bearer JWT

Content-Type: application/json
```

---

## Request Body

```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@example.com",
  "phoneNumber": "9876543210",
  "department": "Engineering",
  "designation": "Senior Developer",
  "companyId": 101,
  "roles": [
    "RECRUITER"
  ]
}
```

---

## Validation Rules

| Field | Validation |
|---------|------------|
| firstName | Required |
| lastName | Required |
| email | Required, Valid Email |
| phoneNumber | 10 Digits |
| companyId | Required |
| roles | Minimum One Role |

---

## Success Response

```http
201 Created
```

```json
{
  "success": true,
  "message": "User created successfully.",
  "data": {
    "id": 1001
  }
}
```

---

# Get All Users

## Endpoint

```http
GET /api/v1/users
```

---

## Query Parameters

```text
page=0

size=20

sort=createdDate,desc

status=ACTIVE

department=Engineering
```

---

## Success Response

```json
{
  "content": [
    {
      "id": 1001,
      "name": "John Doe",
      "email": "john@example.com",
      "status": "ACTIVE"
    }
  ],
  "page": 0,
  "size": 20,
  "totalElements": 50,
  "totalPages": 3
}
```

---

# Get User By ID

## Endpoint

```http
GET /api/v1/users/{id}
```

---

## Path Parameter

```text
id
```

---

## Success Response

```json
{
  "id": 1001,
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@example.com",
  "department": "Engineering",
  "designation": "Senior Developer",
  "roles": [
    "RECRUITER"
  ],
  "status": "ACTIVE"
}
```

---

# Update User

## Endpoint

```http
PUT /api/v1/users/{id}
```

---

## Request

```json
{
  "firstName": "John",
  "lastName": "Smith",
  "department": "Platform",
  "designation": "Tech Lead"
}
```

---

## Response

```http
200 OK
```

```json
{
  "success": true,
  "message": "User updated successfully."
}
```

---

# Update User Status

## Endpoint

```http
PATCH /api/v1/users/{id}/status
```

---

## Request

```json
{
  "status": "INACTIVE"
}
```

Supported values

```text
ACTIVE

INACTIVE

LOCKED

SUSPENDED
```

---

# Assign Roles

## Endpoint

```http
PATCH /api/v1/users/{id}/roles
```

---

## Request

```json
{
  "roles": [
    "ADMIN",
    "RECRUITER"
  ]
}
```

---

## Response

```json
{
  "success": true,
  "message": "Roles updated successfully."
}
```

---

# Delete User

## Endpoint

```http
DELETE /api/v1/users/{id}
```

---

## Success Response

```http
204 No Content
```

---

# Search Users

## Endpoint

```http
GET /api/v1/users/search
```

---

## Query Parameters

```text
keyword=John

department=Engineering

status=ACTIVE

companyId=100

page=0

size=20
```

---

# User Object

```json
{
  "id": 1001,
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@example.com",
  "phoneNumber": "9876543210",
  "department": "Engineering",
  "designation": "Senior Developer",
  "status": "ACTIVE",
  "companyId": 101,
  "roles": [
    "RECRUITER"
  ],
  "createdDate": "2026-08-01T10:00:00Z"
}
```

---

# Business Rules

- Email address must be unique.
- Every user belongs to one company.
- A user can have multiple roles.
- Users cannot delete themselves.
- Only administrators can assign admin roles.
- Locked users cannot authenticate.
- Inactive users cannot access protected APIs.

---

# Error Responses

| HTTP Code | Description |
|------------|-------------|
| 400 | Validation Failed |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | User Not Found |
| 409 | Email Already Exists |
| 422 | Business Validation Failed |
| 500 | Internal Server Error |

---

# Sequence Diagram

```text
Client
   │
POST /users
   │
   ▼
User Controller
   │
   ▼
User Service
   │
Validate Request
   │
Check Duplicate Email
   │
Save User
   │
Assign Roles
   │
Publish UserCreated Event
   │
Return Response
```

---

# Security

All User APIs implement:

- JWT Authentication
- RBAC Authorization
- Input Validation
- Audit Logging
- Rate Limiting
- HTTPS
- SQL Injection Protection
- XSS Protection

---

# Best Practices

- Use pagination for listing users.
- Never expose passwords.
- Validate email uniqueness.
- Log administrative operations.
- Restrict role assignment to authorized users.
- Implement soft delete where required.
- Use optimistic locking for concurrent updates.
- Return standardized API responses.

---

# Summary

The User API provides comprehensive user lifecycle management for the KrewOps Recruitment Platform. It enables secure creation, retrieval, updating, searching, activation, deactivation, role assignment, and deletion of users while enforcing validation, role-based access control, audit logging, and enterprise security standards.
