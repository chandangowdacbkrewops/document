# 05. Job API

## Purpose

This document defines the Job Management APIs for the KrewOps Recruitment Platform. These APIs enable recruiters and hiring managers to create, publish, update, search, close, and manage job postings throughout the recruitment lifecycle.

The Job API follows RESTful principles and supports CRUD operations, pagination, filtering, searching, sorting, and role-based authorization.

---

# Base URL

```text
/api/v1/jobs
```

---

# Job Lifecycle

```text
Create Job
      │
      ▼
Draft
      │
      ▼
Review
      │
      ▼
Published
      │
      ▼
Applications Received
      │
      ▼
Interview Process
      │
      ▼
Position Filled
      │
      ▼
Closed
```

---

# Job APIs

| Method | Endpoint | Description |
|----------|-------------------------------|----------------------------|
| POST | /jobs | Create Job |
| GET | /jobs | Get All Jobs |
| GET | /jobs/{id} | Get Job By ID |
| PUT | /jobs/{id} | Update Job |
| PATCH | /jobs/{id}/status | Update Job Status |
| DELETE | /jobs/{id} | Delete Job |
| GET | /jobs/search | Search Jobs |
| GET | /jobs/company/{companyId} | Jobs By Company |
| GET | /jobs/{id}/applications | Applications For Job |

---

# Create Job

## Endpoint

```http
POST /api/v1/jobs
```

---

## Authorization

```text
ADMIN

RECRUITER

HIRING_MANAGER
```

---

## Headers

```http
Authorization: Bearer JWT

Content-Type: application/json
```

---

## Request Body

```json
{
  "title": "Senior Java Developer",
  "department": "Engineering",
  "location": "Bangalore",
  "employmentType": "FULL_TIME",
  "experience": 5,
  "salaryMin": 1200000,
  "salaryMax": 1800000,
  "vacancies": 3,
  "description": "Java, Spring Boot, Kafka",
  "companyId": 101
}
```

---

## Validation Rules

| Field | Validation |
|---------|------------|
| title | Required |
| department | Required |
| experience | >=0 |
| salaryMin | Positive |
| salaryMax | Greater than salaryMin |
| vacancies | Minimum 1 |
| companyId | Required |

---

## Success Response

```http
201 Created
```

```json
{
  "success": true,
  "message": "Job created successfully.",
  "data": {
    "jobId": 501
  }
}
```

---

# Get All Jobs

## Endpoint

```http
GET /api/v1/jobs
```

---

## Query Parameters

```text
page=0

size=20

sort=createdDate,desc

status=PUBLISHED

department=Engineering

location=Bangalore
```

---

## Response

```json
{
  "content": [
    {
      "id": 501,
      "title": "Senior Java Developer",
      "department": "Engineering",
      "location": "Bangalore",
      "status": "PUBLISHED"
    }
  ],
  "page": 0,
  "size": 20,
  "totalElements": 250,
  "totalPages": 13
}
```

---

# Get Job By ID

## Endpoint

```http
GET /api/v1/jobs/{id}
```

---

## Response

```json
{
  "id": 501,
  "title": "Senior Java Developer",
  "department": "Engineering",
  "location": "Bangalore",
  "employmentType": "FULL_TIME",
  "experience": 5,
  "salaryMin": 1200000,
  "salaryMax": 1800000,
  "vacancies": 3,
  "status": "PUBLISHED",
  "companyId": 101
}
```

---

# Update Job

## Endpoint

```http
PUT /api/v1/jobs/{id}
```

---

## Request

```json
{
  "title": "Lead Java Developer",
  "experience": 6,
  "salaryMax": 2200000,
  "vacancies": 2
}
```

---

## Response

```json
{
  "success": true,
  "message": "Job updated successfully."
}
```

---

# Update Job Status

## Endpoint

```http
PATCH /api/v1/jobs/{id}/status
```

---

## Request

```json
{
  "status": "CLOSED"
}
```

---

## Supported Status

```text
DRAFT

REVIEW

PUBLISHED

ON_HOLD

FILLED

CLOSED
```

---

# Delete Job

## Endpoint

```http
DELETE /api/v1/jobs/{id}
```

---

## Response

```http
204 No Content
```

---

# Search Jobs

## Endpoint

```http
GET /api/v1/jobs/search
```

---

## Query Parameters

```text
keyword=Java

experience=5

location=Bangalore

employmentType=FULL_TIME

salaryMin=1000000

salaryMax=2000000

page=0

size=20
```

---

# Jobs By Company

## Endpoint

```http
GET /api/v1/jobs/company/{companyId}
```

Returns all jobs belonging to the specified company.

---

# Applications For Job

## Endpoint

```http
GET /api/v1/jobs/{id}/applications
```

Returns all applications submitted for the specified job.

---

# Job Object

```json
{
  "id": 501,
  "title": "Senior Java Developer",
  "department": "Engineering",
  "location": "Bangalore",
  "employmentType": "FULL_TIME",
  "experience": 5,
  "salaryMin": 1200000,
  "salaryMax": 1800000,
  "vacancies": 3,
  "status": "PUBLISHED",
  "companyId": 101,
  "createdDate": "2026-08-01T10:00:00Z"
}
```

---

# Business Rules

- Every job belongs to one company.
- Closed jobs cannot receive new applications.
- Filled jobs cannot be published again.
- Salary range must be valid.
- Recruiters can only manage jobs within their own company.
- Only authorized users can publish jobs.

---

# Error Responses

| HTTP Code | Description |
|------------|-------------|
| 400 | Validation Failed |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Job Not Found |
| 409 | Duplicate Job |
| 422 | Business Rule Violation |
| 500 | Internal Server Error |

---

# Sequence Diagram

```text
Client
   │
POST /jobs
   │
   ▼
Job Controller
   │
   ▼
Job Service
   │
Validate Request
   │
Validate Company
   │
Persist Job
   │
Publish JobCreated Event
   │
Return Response
```

---

# Security

All Job APIs implement:

- JWT Authentication
- Role-Based Access Control (RBAC)
- HTTPS
- Input Validation
- Audit Logging
- Rate Limiting
- SQL Injection Protection
- Cross-Site Scripting (XSS) Protection

---

# Best Practices

- Use pagination for list endpoints.
- Publish job lifecycle events to Kafka.
- Soft delete jobs whenever possible.
- Validate salary ranges.
- Maintain audit logs for job modifications.
- Restrict job updates to authorized recruiters.
- Return standardized API responses.

---

# Related APIs

- Company API
- Candidate API
- Application API
- Interview API
- Notification API

---

# Summary

The Job API provides comprehensive job lifecycle management for the KrewOps Recruitment Platform. It enables recruiters and hiring managers to create, publish, update, search, and close job postings while enforcing business rules, secure access control, standardized responses, validation, and event-driven integration with downstream services such as applications, interviews, and notifications.
