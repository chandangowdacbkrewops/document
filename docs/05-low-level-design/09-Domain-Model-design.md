# 09. Domain Model Design

## Purpose

This chapter defines the Domain Model for the KrewOps Recruitment Platform. The Domain Model represents the core business entities, their attributes, relationships, and business concepts that drive the application's functionality. It serves as the foundation for persistence, business logic, and API interactions.

---

# Objectives

The Domain Model Design aims to:

- Represent real-world business concepts.
- Model relationships between business entities.
- Define ownership of business data.
- Support scalable application architecture.
- Maintain data integrity.
- Promote object-oriented design.
- Enable efficient persistence and querying.

---

# Domain Model Overview

The Recruitment Platform revolves around the following core business domains:

- User Management
- Company Management
- Candidate Management
- Job Management
- Interview Management
- Application Management
- Role & Permission Management
- Notification Management

---

# High-Level Domain Model

```text
                    Company
                       │
         ┌─────────────┼─────────────┐
         │             │             │
         ▼             ▼             ▼
      User           Job        Interview
         │             │             │
         └─────────────┼─────────────┘
                       │
                       ▼
                 Candidate
                       │
                       ▼
                 Application
                       │
                       ▼
                Notification
```

---

# Core Domain Entities

| Entity | Description |
|----------|-------------|
| User | Platform user responsible for system operations |
| Company | Organization using the recruitment platform |
| Candidate | Applicant applying for jobs |
| Job | Open job position |
| Interview | Candidate interview schedule |
| Application | Candidate job application |
| Role | User authorization role |
| Permission | System permissions |
| Notification | User notifications |

---

# User Entity

## Responsibilities

- Authentication
- Authorization
- Profile Management
- User Preferences

### Attributes

```text
id
firstName
lastName
email
phoneNumber
password
status
createdDate
updatedDate
```

### Relationships

```text
User
 │
 ├── belongs to Company
 ├── assigned Roles
 └── receives Notifications
```

---

# Company Entity

## Responsibilities

- Organization Information
- User Ownership
- Job Ownership
- Subscription Details

### Attributes

```text
id
companyName
industry
website
email
phone
status
createdDate
```

### Relationships

```text
Company
 │
 ├── Users
 ├── Jobs
 ├── Interviews
 └── Candidates
```

---

# Candidate Entity

## Responsibilities

- Personal Information
- Resume
- Skills
- Experience
- Education

### Attributes

```text
id
firstName
lastName
email
phone
experience
noticePeriod
resumeUrl
status
createdDate
```

### Relationships

```text
Candidate
 │
 ├── Applications
 ├── Interviews
 └── Company
```

---

# Job Entity

## Responsibilities

- Job Posting
- Hiring Requirements
- Salary Details
- Candidate Matching

### Attributes

```text
id
title
description
location
experience
salary
employmentType
status
createdDate
```

### Relationships

```text
Job
 │
 ├── Company
 ├── Applications
 └── Interviews
```

---

# Application Entity

## Responsibilities

- Candidate Job Mapping
- Hiring Status
- Application Tracking

### Attributes

```text
id
candidateId
jobId
applicationDate
status
remarks
```

### Relationships

```text
Application
 │
 ├── Candidate
 └── Job
```

---

# Interview Entity

## Responsibilities

- Interview Scheduling
- Feedback
- Result Tracking

### Attributes

```text
id
candidateId
jobId
interviewer
scheduledDate
status
feedback
```

### Relationships

```text
Interview
 │
 ├── Candidate
 ├── Job
 └── User
```

---

# Role Entity

## Responsibilities

- Authorization
- Access Management

### Attributes

```text
id
roleName
description
```

### Relationships

```text
Role
 │
 ├── Users
 └── Permissions
```

---

# Permission Entity

## Responsibilities

- Fine-grained Access Control

### Attributes

```text
id
permissionName
description
module
```

### Relationships

```text
Permission
 │
 └── Roles
```

---

# Notification Entity

## Responsibilities

- User Notifications
- Email Events
- System Alerts

### Attributes

```text
id
userId
title
message
type
status
createdDate
```

---

# Entity Relationships

## One-to-Many

```text
Company
   │
   ├── Users
   ├── Jobs
   ├── Candidates
   └── Interviews
```

---

## Many-to-One

```text
Job
 │
 ▼
Company
```

---

## Many-to-Many

```text
User
 │
 ├──────────────┐
 │              │
 ▼              ▼
Role ------ Permission
```

---

# Relationship Summary

| Parent | Child | Relationship |
|----------|---------|--------------|
| Company | User | One-to-Many |
| Company | Job | One-to-Many |
| Company | Candidate | One-to-Many |
| Candidate | Application | One-to-Many |
| Job | Application | One-to-Many |
| Candidate | Interview | One-to-Many |
| Job | Interview | One-to-Many |
| User | Role | Many-to-Many |
| Role | Permission | Many-to-Many |

---

# Aggregate Boundaries

The domain is organized into aggregates to maintain consistency.

```text
Company Aggregate
│
├── Company
├── Users
└── Jobs
```

```text
Candidate Aggregate
│
├── Candidate
├── Applications
└── Interviews
```

```text
Security Aggregate
│
├── User
├── Role
└── Permission
```

---

# Business Rules

Examples of domain rules include:

- A Company can own multiple Jobs.
- A Candidate may apply for multiple Jobs.
- A Job can receive multiple Applications.
- An Interview must reference one Candidate and one Job.
- Users may have multiple Roles.
- Roles may contain multiple Permissions.
- Deleted Companies cannot create new Jobs.
- Closed Jobs cannot accept Applications.

---

# Entity Lifecycle

```text
Create
   │
   ▼
Validate
   │
   ▼
Persist
   │
   ▼
Update
   │
   ▼
Archive/Delete
```

Every entity follows a consistent lifecycle managed by the Service layer.

---

# Domain Model Guidelines

- Model real business concepts.
- Keep entities focused on business state.
- Avoid persistence logic in entities.
- Maintain referential integrity.
- Use meaningful relationships.
- Avoid cyclic dependencies.
- Prefer composition over inheritance.
- Keep aggregates small and cohesive.

---

# Benefits

The Domain Model provides:

- Clear representation of business concepts.
- Improved maintainability.
- Better scalability.
- Consistent business rules.
- Simplified persistence.
- Strong object-oriented design.
- Easier future enhancements.
- Improved collaboration between developers and business stakeholders.

---

# Summary

The Domain Model Design defines the core business entities and their relationships within the KrewOps Recruitment Platform. By organizing the application around well-defined domain concepts, aggregate boundaries, and business rules, the domain model establishes a robust foundation for implementing scalable, maintainable, and business-driven software while preserving data integrity and supporting future system evolution.
