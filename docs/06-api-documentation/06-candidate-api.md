# 06. Candidate API

## Purpose

This document defines the Candidate Management APIs for the KrewOps Recruitment Platform. These APIs enable recruiters to create, manage, search, update, and track candidates throughout the recruitment lifecycle.

The Candidate API follows RESTful principles and supports CRUD operations, resume upload, searching, pagination, filtering, and role-based authorization.

---

# Base URL

```text
/api/v1/candidates
```

---

# Candidate Lifecycle

```text
Candidate Created
        │
        ▼
Resume Uploaded
        │
        ▼
Applied For Job
        │
        ▼
Shortlisted
        │
        ▼
Interview Scheduled
        │
        ▼
Interview Completed
        │
        ▼
Offer Released
        │
        ▼
Hired / Rejected
```

---

# Candidate APIs

| Method | Endpoint | Description |
|----------|-------------------------------|------------------------------|
| POST | /candidates | Create Candidate |
| GET | /candidates | Get All Candidates |
| GET | /candidates/{id} | Get Candidate By ID |
| PUT | /candidates/{id} | Update Candidate |
| PATCH | /candidates/{id}/status | Update Candidate Status |
| DELETE | /candidates/{id} | Delete Candidate |
| GET | /candidates/search | Search Candidates |
| POST | /candidates/{id}/resume | Upload Resume |
| GET | /candidates/{id}/resume | Download Resume |
| GET | /candidates/{id}/applications | Candidate Applications |

---

# Create Candidate

## Endpoint

```http
POST /api/v1/candidates
```

---

## Authorization

```text
ADMIN

RECRUITER
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
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@gmail.com",
  "phoneNumber": "9876543210",
  "experience": 5,
  "skills": [
    "Java",
    "Spring Boot",
    "Kafka"
  ],
  "currentLocation": "Bangalore",
  "currentCompany": "ABC Technologies"
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
| experience | >=0 |
| skills | At least one skill |

---

## Success Response

```http
201 Created
```

```json
{
  "success": true,
  "message": "Candidate created successfully.",
  "data": {
    "candidateId": 1001
  }
}
```

---

# Get All Candidates

## Endpoint

```http
GET /api/v1/candidates
```

---

## Query Parameters

```text
page=0

size=20

sort=createdDate,desc

status=ACTIVE

experience=5

location=Bangalore
```

---

## Success Response

```json
{
  "content": [
    {
      "id": 1001,
      "name": "John Doe",
      "experience": 5,
      "status": "ACTIVE"
    }
  ],
  "page": 0,
  "size": 20,
  "totalElements": 250,
  "totalPages": 13
}
```

---

# Get Candidate By ID

## Endpoint

```http
GET /api/v1/candidates/{id}
```

---

## Response

```json
{
  "id": 1001,
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@gmail.com",
  "phoneNumber": "9876543210",
  "experience": 5,
  "skills": [
    "Java",
    "Spring Boot",
    "Kafka"
  ],
  "currentCompany": "ABC Technologies",
  "status": "ACTIVE"
}
```

---

# Update Candidate

## Endpoint

```http
PUT /api/v1/candidates/{id}
```

---

## Request

```json
{
  "experience": 6,
  "currentCompany": "Waymore Technologies",
  "currentLocation": "Bangalore"
}
```

---

## Success Response

```json
{
  "success": true,
  "message": "Candidate updated successfully."
}
```

---

# Update Candidate Status

## Endpoint

```http
PATCH /api/v1/candidates/{id}/status
```

---

## Request

```json
{
  "status": "SHORTLISTED"
}
```

---

## Supported Status

```text
ACTIVE

SHORTLISTED

INTERVIEW_SCHEDULED

OFFERED

HIRED

REJECTED
```

---

# Upload Resume

## Endpoint

```http
POST /api/v1/candidates/{id}/resume
```

---

## Content-Type

```http
multipart/form-data
```

---

## Request

```text
resume.pdf
```

---

## Response

```json
{
  "success": true,
  "message": "Resume uploaded successfully."
}
```

---

# Download Resume

## Endpoint

```http
GET /api/v1/candidates/{id}/resume
```

Returns the candidate's latest uploaded resume.

---

# Candidate Applications

## Endpoint

```http
GET /api/v1/candidates/{id}/applications
```

Returns all applications submitted by the candidate.

---

# Search Candidates

## Endpoint

```http
GET /api/v1/candidates/search
```

---

## Query Parameters

```text
keyword=Java

experience=5

location=Bangalore

skill=Kafka

status=ACTIVE

page=0

size=20
```

---

# Candidate Object

```json
{
  "id": 1001,
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@gmail.com",
  "phoneNumber": "9876543210",
  "experience": 5,
  "skills": [
    "Java",
    "Spring Boot",
    "Kafka"
  ],
  "currentCompany": "ABC Technologies",
  "currentLocation": "Bangalore",
  "status": "ACTIVE",
  "createdDate": "2026-08-01T10:00:00Z"
}
```

---

# Business Rules

- Email address must be unique.
- Phone number must be unique.
- Resume upload is optional during candidate creation.
- One candidate can apply for multiple jobs.
- Duplicate applications for the same job are not allowed.
- Recruiters can only access candidates belonging to their company.

---

# Error Responses

| HTTP Code | Description |
|------------|-------------|
| 400 | Validation Failed |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Candidate Not Found |
| 409 | Candidate Already Exists |
| 413 | File Too Large |
| 415 | Unsupported File Type |
| 422 | Business Rule Violation |
| 500 | Internal Server Error |

---

# Sequence Diagram

```text
Client
   │
POST /candidates
   │
   ▼
Candidate Controller
   │
   ▼
Candidate Service
   │
Validate Request
   │
Check Duplicate Email
   │
Persist Candidate
   │
Publish CandidateCreated Event
   │
Return Response
```

---

# Security

All Candidate APIs implement:

- JWT Authentication
- Role-Based Access Control (RBAC)
- HTTPS
- Multipart File Validation
- Input Validation
- Audit Logging
- Rate Limiting
- SQL Injection Protection
- XSS Protection

---

# Best Practices

- Validate uploaded file types.
- Restrict maximum resume size.
- Store resumes in object storage (Amazon S3, Azure Blob, or MinIO).
- Publish candidate events using Kafka.
- Use pagination for listing candidates.
- Audit all profile updates.
- Never expose confidential candidate information.

---

# Related APIs

- Job API
- Application API
- Interview API
- Notification API

---

# Summary

The Candidate API provides complete candidate lifecycle management for the KrewOps Recruitment Platform. It supports candidate registration, profile management, resume upload, searching, application tracking, and recruitment status updates while ensuring secure access, robust validation, standardized responses, and seamless integration with jobs, interviews, and notifications through an event-driven architecture.
