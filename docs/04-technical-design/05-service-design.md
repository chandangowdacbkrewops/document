# 05. Service Design

## Purpose

This chapter defines the internal design of each microservice, including responsibilities, owned data, APIs, dependencies, events, and scalability considerations.

---

# Service Inventory

| Service | Primary Responsibility |
|---|---|
| Authentication Service | User authentication and authorization |
| Organization Service | Tenant and organization management |
| Job Service | Job lifecycle management |
| Candidate Service | Candidate profiles and applications |
| Interview Service | Interview scheduling and feedback |
| AI Service | Resume parsing and candidate recommendations |
| Notification Service | Email, SMS and in-app notifications |
| Reporting Service | Analytics and report generation |

---

# Standard Service Responsibilities

Every service shall:

- Expose REST APIs.
- Validate incoming requests.
- Enforce authorization.
- Own its business data.
- Publish domain events.
- Consume relevant events.
- Produce audit logs.
- Emit metrics and logs.

---

# Service Contract

Each service defines:

- Public REST endpoints
- Request and response models
- Validation rules
- Business rules
- Error responses
- Event contracts

---

# Data Ownership

Each business entity shall have a single owning service. Cross-service communication shall occur through REST APIs or published events rather than direct database access.

---

# Event Communication

Services publish and consume domain events using Kafka to support asynchronous workflows, notifications, reporting, and AI processing.

Typical events include:

- JobCreated
- CandidateApplied
- InterviewScheduled
- OfferGenerated
- NotificationRequested

---

# Security

All services shall:

- Validate JWT access tokens
- Enforce RBAC
- Validate input
- Log security events
- Protect sensitive information

---

# Scalability

Services are designed to be:

- Stateless
- Independently deployable
- Horizontally scalable
- Fault tolerant

---

# Summary

The service design establishes clear ownership, interfaces, communication patterns, and operational expectations for every microservice, enabling independent development, deployment, and scaling across the KrewOps platform.