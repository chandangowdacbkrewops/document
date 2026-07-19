# 13. Messaging Design (Kafka)

## Purpose

This chapter defines the Messaging Design for the KrewOps Recruitment Platform. Apache Kafka is used as the event streaming platform to enable asynchronous communication between microservices, improve scalability, decouple services, and provide reliable event delivery for business processes.

---

# Objectives

The Messaging Design aims to:

- Enable asynchronous communication.
- Decouple microservices.
- Improve system scalability.
- Increase application resilience.
- Support event-driven architecture.
- Ensure reliable message delivery.
- Enable audit and event replay.

---

# Messaging Architecture

```text
                REST API
                    │
                    ▼
              Service Layer
                    │
        Business Event Created
                    │
                    ▼
            Kafka Producer
                    │
                    ▼
              Kafka Cluster
        ┌───────────┼────────────┐
        │           │            │
        ▼           ▼            ▼
 Candidate     Notification    Audit
 Consumer       Consumer      Consumer
        │           │            │
        ▼           ▼            ▼
 PostgreSQL    Email Service   Audit DB
```

Kafka acts as the central event streaming platform between producers and consumers.

---

# Messaging Components

| Component | Responsibility |
|------------|----------------|
| Producer | Publishes events |
| Topic | Stores ordered events |
| Partition | Enables parallel processing |
| Broker | Stores and serves events |
| Consumer | Processes events |
| Consumer Group | Supports horizontal scaling |

---

# Event Flow

```text
User Action
      │
      ▼
Controller
      │
      ▼
Service
      │
      ▼
Save Database
      │
      ▼
Publish Event
      │
      ▼
Kafka Topic
      │
      ▼
Consumers
      │
      ▼
Business Processing
```

Events are published only after successful business processing.

---

# Producer Design

Responsibilities include:

- Publish domain events.
- Serialize event payloads.
- Set message keys.
- Handle retries.
- Log publishing failures.

Typical producer events:

- CandidateCreated
- JobCreated
- InterviewScheduled
- UserRegistered
- NotificationRequested

---

# Consumer Design

Consumers subscribe to Kafka topics and process events asynchronously.

Responsibilities:

- Deserialize messages.
- Validate events.
- Execute business logic.
- Handle retries.
- Commit offsets.

Consumers should remain idempotent.

---

# Topic Design

| Topic | Purpose |
|---------|---------|
| candidate-events | Candidate lifecycle events |
| job-events | Job lifecycle events |
| interview-events | Interview scheduling events |
| notification-events | Notification processing |
| audit-events | Audit logging |
| user-events | User management events |

---

# Event Structure

Every event follows a standardized structure.

Example:

```json
{
  "eventId": "7d45a1f9",
  "eventType": "CandidateCreated",
  "timestamp": "2026-07-19T12:00:00Z",
  "source": "candidate-service",
  "payload": {
    "candidateId": 101,
    "name": "John Doe"
  }
}
```

---

# Message Keys

Kafka message keys ensure ordering for related events.

Examples:

```text
Candidate ID

Job ID

Interview ID

Company ID

User ID
```

Messages with the same key are delivered to the same partition.

---

# Partition Strategy

```text
Topic
 │
 ├── Partition 0
 ├── Partition 1
 ├── Partition 2
 └── Partition N
```

Benefits:

- Parallel processing
- Higher throughput
- Better scalability

---

# Consumer Groups

```text
Topic
 │
 ▼
Consumer Group
 │
 ├── Consumer 1
 ├── Consumer 2
 ├── Consumer 3
 └── Consumer N
```

Each partition is consumed by only one consumer within a group.

---

# Delivery Guarantees

The platform targets:

- At-Least-Once Delivery

Duplicate event handling is managed through idempotent consumers.

---

# Offset Management

Consumers commit offsets only after successful event processing.

Benefits:

- Prevents message loss.
- Supports restart recovery.
- Enables replay.

---

# Retry Strategy

Retry flow:

```text
Receive Event
      │
      ▼
Processing Failed
      │
      ▼
Retry
      │
      ▼
Retry Limit Reached
      │
      ▼
Dead Letter Topic
```

Retries use configurable backoff intervals.

---

# Dead Letter Topic (DLT)

Messages that cannot be processed after multiple retries are sent to a dedicated Dead Letter Topic.

Benefits:

- Prevents blocking consumers.
- Enables manual investigation.
- Supports message replay.

---

# Error Handling

Typical failures include:

- Invalid payload.
- Serialization errors.
- Database failures.
- Network issues.
- Downstream service failures.

Consumers log failures and apply retry policies.

---

# Idempotency

Consumers should safely process duplicate events.

Techniques include:

- Unique event identifiers.
- Database constraints.
- Processed event tracking.
- Optimistic locking.

---

# Monitoring

Important Kafka metrics:

- Consumer Lag
- Message Throughput
- Failed Events
- Retry Count
- Dead Letter Queue Size
- Processing Latency

Monitoring supports proactive issue detection.

---

# Security

Kafka communication should be secured using:

- TLS Encryption
- SASL Authentication
- ACL-based Authorization
- Secure Credentials
- Encrypted Network Communication

---

# Best Practices

- Publish events only after successful transactions.
- Keep event payloads immutable.
- Design idempotent consumers.
- Use meaningful topic names.
- Keep messages lightweight.
- Avoid large payloads.
- Monitor consumer lag.
- Configure retries and dead-letter topics.
- Maintain backward-compatible event schemas.

---

# Benefits

The Messaging Design provides:

- Loose coupling between services.
- Improved scalability.
- Reliable asynchronous communication.
- Better fault tolerance.
- Event replay capability.
- High throughput.
- Horizontal scalability.
- Easier integration with future services.

---

# Summary

The Messaging Design establishes Apache Kafka as the event backbone of the KrewOps Recruitment Platform. By adopting an event-driven architecture with reliable producers, scalable consumers, structured event schemas, retry mechanisms, dead-letter topics, and secure messaging practices, the platform achieves high scalability, resilience, and maintainability while enabling efficient asynchronous processing across distributed services.
