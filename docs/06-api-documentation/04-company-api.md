# 04. Company API

## Purpose

This document defines the Company Management APIs for the KrewOps Recruitment Platform. These APIs enable administrators and recruiters to create, manage, retrieve, update, and deactivate companies. A company acts as the tenant for users, jobs, candidates, interviews, and recruitment activities.

The Company API follows RESTful principles and supports CRUD operations, pagination, filtering, sorting, and search.

---

# Base URL

```text
/api/v1/companies
```

---

# Company Lifecycle

```text
Create Company
       │
       ▼
Assign Subscription
       │
       ▼
Create Users
       │
       ▼
Create Jobs
       │
       ▼
Manage Candidates
       │
       ▼
Deactivate Company
```

---

# Company APIs

| Method | Endpoint | Description |
|----------|-----------------------------|---------------------------|
| POST | /companies | Create Company |
| GET | /companies | Get All Companies |
| GET | /companies/{id} | Get Company By ID |
| PUT | /companies/{id} | Update Company |
| PATCH | /companies/{id}/status | Activate / Deactivate Company |
| DELETE | /companies/{id} | Delete Company |
| GET | /companies/search | Search Companies |
| GET | /companies/{id}/users | Get Company Users |
| GET | /companies/{id}/jobs | Get Company Jobs |

---

# Create Company

## Endpoint

```http
POST /api/v1/companies
```

---

## Authorization

```text
ADMIN
SUPER_ADMIN
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
  "companyName": "Waymore Technologies",
  "industry": "Software",
  "website": "https://waymore.io",
  "email": "info@waymore.io",
  "phone": "9876543210",
  "address": "Bangalore",
  "subscriptionPlan": "ENTERPRISE"
}
```

---

## Validation Rules

| Field | Validation |
|---------|------------|
| companyName | Required |
| email | Valid Email |
| website | Valid URL |
| subscriptionPlan | Required |

---

## Success Response

```http
201 Created
```

```json
{
  "success": true,
  "message": "Company created successfully.",
  "data": {
    "id": 101
  }
}
```

---

# Get All Companies

## Endpoint

```http
GET /api/v1/companies
```

---

## Query Parameters

```text
page=0

size=20

sort=companyName

status=ACTIVE

industry=Software
```

---

## Response

```json
{
  "content": [
    {
      "id": 101,
      "companyName": "Waymore Technologies",
      "industry": "Software",
      "status": "ACTIVE"
    }
  ],
  "page": 0,
  "size": 20,
  "totalElements": 100,
  "totalPages": 5
}
```

---

# Get Company By ID

## Endpoint

```http
GET /api/v1/companies/{id}
```

---

## Response

```json
{
  "id": 101,
  "companyName": "Waymore Technologies",
  "industry": "Software",
  "website": "https://waymore.io",
  "email": "info@waymore.io",
  "phone": "9876543210",
  "address": "Bangalore",
  "subscriptionPlan": "ENTERPRISE",
  "status": "ACTIVE"
}
```

---

# Update Company

## Endpoint

```http
PUT /api/v1/companies/{id}
```

---

## Request

```json
{
  "companyName": "Waymore Solutions",
  "industry": "Software",
  "website": "https://waymore.io",
  "phone": "9988776655"
}
```

---

## Response

```json
{
  "success": true,
  "message": "Company updated successfully."
}
```

---

# Update Company Status

## Endpoint

```http
PATCH /api/v1/companies/{id}/status
```

---

## Request

```json
{
  "status": "INACTIVE"
}
```

Supported Status

```text
ACTIVE

INACTIVE

SUSPENDED
```

---

# Delete Company

## Endpoint

```http
DELETE /api/v1/companies/{id}
```

---

## Response

```http
204 No Content
```

---

# Search Companies

## Endpoint

```http
GET /api/v1/companies/search
```

---

## Query Parameters

```text
keyword=Waymore

industry=Software

status=ACTIVE

page=0

size=20
```

---

# Get Company Users

## Endpoint

```http
GET /api/v1/companies/{id}/users
```

Returns all users belonging to the specified company.

---

# Get Company Jobs

## Endpoint

```http
GET /api/v1/companies/{id}/jobs
```

Returns all job postings created by the specified company.

---

# Company Object

```json
{
  "id": 101,
  "companyName": "Waymore Technologies",
  "industry": "Software",
  "website": "https://waymore.io",
  "email": "info@waymore.io",
  "phone": "9876543210",
  "address": "Bangalore",
  "subscriptionPlan": "ENTERPRISE",
  "status": "ACTIVE",
  "createdDate": "2026-08-01T10:00:00Z"
}
```

---

# Business Rules

- Company name must be unique.
- Company email must be unique.
- One company can have multiple users.
- One company can create multiple jobs.
- Suspended companies cannot create new jobs.
- Deleting a company requires all active users and jobs to be handled according to business policy (soft delete or archival).

---

# Error Responses

| HTTP Code | Description |
|------------|-------------|
| 400 | Validation Failed |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Company Not Found |
| 409 | Company Already Exists |
| 422 | Business Rule Violation |
| 500 | Internal Server Error |

---

# Sequence Diagram

```text
Client
   │
POST /companies
   │
   ▼
Company Controller
   │
   ▼
Company Service
   │
Validate Request
   │
Check Duplicate Company
   │
Persist Company
   │
Publish CompanyCreated Event
   │
Return Response
```

---

# Security

All Company APIs implement:

- JWT Authentication
- Role-Based Access Control (RBAC)
- Input Validation
- HTTPS
- Audit Logging
- Rate Limiting
- SQL Injection Protection
- XSS Protection

---

# Best Practices

- Use pagination for list APIs.
- Validate company uniqueness.
- Soft delete companies instead of physical deletion where possible.
- Publish company lifecycle events through Kafka.
- Protect administrative endpoints using RBAC.
- Return consistent API responses.
- Audit all create, update, and delete operations.

---

# Summary

The Company API provides complete tenant management capabilities for the KrewOps Recruitment Platform. It enables secure creation, retrieval, modification, activation, deactivation, and administration of companies while enforcing validation, role-based access control, standardized API responses, and enterprise-grade security practices.
