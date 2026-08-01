# 02. Authentication API

## Purpose

This document defines the Authentication APIs for the KrewOps Recruitment Platform. Authentication is responsible for verifying user identity, issuing JWT access tokens, refreshing expired tokens, managing user sessions, and supporting secure password management.

The platform uses **JWT-based stateless authentication** with **OAuth 2.0** principles and **Spring Security**.

---

# Base URL

```text
/api/v1/auth
```

---

# Authentication Flow

```text
              User
                │
                ▼
      POST /auth/login
                │
                ▼
      Authentication Manager
                │
      Username + Password
                │
                ▼
         User Validation
                │
                ▼
        Generate JWT Token
                │
                ▼
       Return Access Token
                │
                ▼
      Client Stores Token
                │
                ▼
Authorization: Bearer JWT
                │
                ▼
         Protected APIs
```

---

# Authentication APIs

| Method | Endpoint | Description |
|----------|-------------------------|----------------------------|
| POST | /login | User Login |
| POST | /logout | User Logout |
| POST | /refresh | Refresh Access Token |
| POST | /register | Register New User |
| POST | /forgot-password | Forgot Password |
| POST | /reset-password | Reset Password |
| POST | /change-password | Change Password |
| GET | /profile | Logged-in User Profile |

---

# Login API

## Endpoint

```http
POST /api/v1/auth/login
```

---

## Description

Authenticates a user using email and password.

Returns

- JWT Access Token
- Refresh Token
- User Information

---

## Request Headers

```http
Content-Type: application/json
```

---

## Request Body

```json
{
  "email": "john@example.com",
  "password": "Password@123"
}
```

---

## Validation Rules

| Field | Validation |
|---------|------------|
| email | Required, Valid Email |
| password | Required |

---

## Success Response

HTTP

```text
200 OK
```

Response

```json
{
  "success": true,
  "message": "Login successful",
  "data": {
    "accessToken": "<JWT>",
    "refreshToken": "<REFRESH>",
    "expiresIn": 3600,
    "user": {
      "id": 1001,
      "name": "John Doe",
      "email": "john@example.com",
      "roles": [
        "ADMIN"
      ]
    }
  }
}
```

---

## Error Responses

```text
400 Bad Request

401 Unauthorized

423 Locked

500 Internal Server Error
```

---

# Logout API

## Endpoint

```http
POST /api/v1/auth/logout
```

---

## Headers

```http
Authorization: Bearer JWT
```

---

## Success Response

```json
{
  "success": true,
  "message": "Logout successful"
}
```

---

# Refresh Token API

## Endpoint

```http
POST /api/v1/auth/refresh
```

---

## Request

```json
{
  "refreshToken": "<REFRESH_TOKEN>"
}
```

---

## Response

```json
{
  "accessToken": "<NEW_ACCESS_TOKEN>",
  "refreshToken": "<NEW_REFRESH_TOKEN>"
}
```

---

# Register API

## Endpoint

```http
POST /api/v1/auth/register
```

---

## Request

```json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john@example.com",
  "password": "Password@123",
  "phoneNumber": "9876543210"
}
```

---

## Success Response

```text
201 Created
```

```json
{
  "success": true,
  "message": "User registered successfully"
}
```

---

# Forgot Password API

## Endpoint

```http
POST /api/v1/auth/forgot-password
```

---

## Request

```json
{
  "email": "john@example.com"
}
```

---

## Process

```text
Validate Email
      │
      ▼
Generate Reset Token
      │
      ▼
Store Token
      │
      ▼
Send Email
```

---

# Reset Password API

## Endpoint

```http
POST /api/v1/auth/reset-password
```

---

## Request

```json
{
  "token": "reset-token",
  "newPassword": "Password@123"
}
```

---

# Change Password API

## Endpoint

```http
POST /api/v1/auth/change-password
```

---

## Headers

```http
Authorization: Bearer JWT
```

---

## Request

```json
{
  "oldPassword": "OldPassword",
  "newPassword": "NewPassword@123"
}
```

---

# Profile API

## Endpoint

```http
GET /api/v1/auth/profile
```

---

## Headers

```http
Authorization: Bearer JWT
```

---

## Response

```json
{
  "id": 1001,
  "name": "John Doe",
  "email": "john@example.com",
  "roles": [
    "ADMIN"
  ],
  "company": "Waymore"
}
```

---

# JWT Structure

```text
Header

Payload

Signature
```

Claims

- User ID
- Email
- Roles
- Expiration Time
- Issued Time

---

# Security

Authentication APIs implement:

- BCrypt Password Encoding
- JWT Authentication
- HTTPS
- Account Lockout
- Password Policy
- Refresh Tokens
- Audit Logging
- Rate Limiting

---

# HTTP Status Codes

| Code | Description |
|--------|-------------|
| 200 | Login Successful |
| 201 | Registration Successful |
| 400 | Validation Failed |
| 401 | Invalid Credentials |
| 403 | Access Denied |
| 404 | User Not Found |
| 409 | Email Already Exists |
| 423 | Account Locked |
| 429 | Too Many Requests |
| 500 | Internal Server Error |

---

# Sequence Diagram

```text
User
 │
 │ POST /login
 ▼
Controller
 │
 ▼
Authentication Service
 │
 ▼
Authentication Manager
 │
 ▼
User Details Service
 │
 ▼
Password Validation
 │
 ▼
Generate JWT
 │
 ▼
Return Access Token
```

---

# Best Practices

- Always use HTTPS.
- Never store passwords in plain text.
- Use BCrypt hashing.
- Keep JWT expiration short.
- Rotate refresh tokens.
- Enable account lockout.
- Log authentication events.
- Never expose sensitive information in API responses.

---

# Summary

The Authentication API provides secure access to the KrewOps Recruitment Platform using JWT-based authentication and Spring Security. It supports login, logout, user registration, password management, token refresh, and profile retrieval while enforcing enterprise-grade security practices such as password hashing, token-based authentication, HTTPS communication, audit logging, and role-based authorization.
