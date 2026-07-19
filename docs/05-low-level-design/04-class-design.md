# 04. Class Design

## Purpose

This chapter defines the class-level design of the KrewOps Recruitment Platform. It describes the responsibilities, relationships, interactions, and implementation guidelines for classes used throughout the application. The objective is to promote maintainability, extensibility, reusability, and adherence to object-oriented design principles.

---

# Objectives

The class design aims to:

- Clearly define class responsibilities.
- Promote loose coupling and high cohesion.
- Encourage interface-driven development.
- Follow SOLID principles.
- Support unit testing.
- Enable scalable and maintainable code.

---

# Class Design Principles

The application follows these object-oriented principles:

- Single Responsibility Principle (SRP)
- Open/Closed Principle (OCP)
- Liskov Substitution Principle (LSP)
- Interface Segregation Principle (ISP)
- Dependency Inversion Principle (DIP)
- Composition over Inheritance
- Constructor-based Dependency Injection

---

# Overall Class Relationship

```text
                Client
                   │
                   ▼
        ┌────────────────────┐
        │   Controller       │
        └─────────┬──────────┘
                  │
                  ▼
        ┌────────────────────┐
        │     Service        │
        └─────────┬──────────┘
                  │
                  ▼
        ┌────────────────────┐
        │   Repository       │
        └─────────┬──────────┘
                  │
                  ▼
        ┌────────────────────┐
        │     Database       │
        └────────────────────┘
```

Supporting components such as Mappers, Validators, Security, Cache, and Kafka interact with the Service layer as required.

---

# Controller Classes

## Purpose

Controller classes expose REST APIs.

### Responsibilities

- Receive HTTP requests.
- Validate input.
- Invoke business services.
- Return HTTP responses.
- Handle request parameters.
- Generate API documentation.

### Example

```text
UserController
JobController
CandidateController
InterviewController
AuthController
```

Controllers should never implement business logic.

---

# Service Classes

## Purpose

Service classes implement business rules.

### Responsibilities

- Business processing.
- Workflow orchestration.
- Transaction management.
- Validation coordination.
- Repository interaction.
- External integrations.

### Example

```text
UserService
UserServiceImpl

JobService
JobServiceImpl
```

Services should contain the application's core business logic.

---

# Repository Classes

## Purpose

Repositories abstract database operations.

### Responsibilities

- CRUD operations.
- Search.
- Pagination.
- Custom queries.
- Data persistence.

### Example

```text
UserRepository
JobRepository
InterviewRepository
```

Repositories should not contain business logic.

---

# Entity Classes

## Purpose

Entities represent persistent domain objects.

### Responsibilities

- Database mapping.
- Relationships.
- Constraints.
- Primary keys.
- Auditing fields.

### Example

```text
User
Candidate
Job
Interview
Role
Permission
```

Entities should only model persistent data.

---

# DTO Classes

## Purpose

DTOs transfer data between application layers.

### Responsibilities

- Request payloads.
- Response payloads.
- Validation annotations.
- API serialization.

### Example

```text
CreateCandidateRequest

CandidateResponse

UpdateJobRequest

JobResponse
```

DTOs should not contain business logic.

---

# Mapper Classes

## Purpose

Map entities and DTOs.

### Responsibilities

- Entity → DTO
- DTO → Entity
- Response mapping
- Request mapping

### Example

```text
CandidateMapper
UserMapper
JobMapper
```

All conversion logic should remain inside mapper classes.

---

# Validator Classes

## Purpose

Implement reusable validation logic.

### Responsibilities

- Business validation.
- Input validation.
- Custom annotations.
- Common validation rules.

### Example

```text
EmailValidator

PasswordValidator

PhoneValidator
```

Validation logic should never be duplicated.

---

# Configuration Classes

## Purpose

Provide infrastructure configuration.

### Responsibilities

- Spring Beans
- Kafka
- Redis
- Database
- Swagger
- Security
- Scheduling

### Example

```text
KafkaConfig

RedisConfig

SecurityConfig

DatabaseConfig
```

Configuration should be centralized.

---

# Security Classes

## Purpose

Implement authentication and authorization.

### Responsibilities

- JWT validation
- Authentication
- Authorization
- UserDetailsService
- Security filters

### Example

```text
JwtAuthenticationFilter

JwtTokenProvider

SecurityConfiguration
```

Security logic should remain isolated from business logic.

---

# Kafka Classes

## Purpose

Implement asynchronous messaging.

### Responsibilities

- Event publishing.
- Event consumption.
- Topic management.
- Retry handling.
- Dead Letter Queue.

### Example

```text
CandidateProducer

InterviewConsumer

NotificationProducer
```

Messaging classes should focus only on event processing.

---

# Cache Classes

## Purpose

Provide caching functionality.

### Responsibilities

- Cache retrieval.
- Cache updates.
- Cache eviction.
- Redis interaction.

### Example

```text
UserCacheService

JobCacheService
```

Caching logic should remain independent of business logic.

---

# Scheduler Classes

## Purpose

Execute scheduled jobs.

### Responsibilities

- Cleanup.
- Notifications.
- Reports.
- Synchronization.
- Maintenance tasks.

### Example

```text
CleanupScheduler

NotificationScheduler

ReminderScheduler
```

---

# Utility Classes

## Purpose

Provide reusable helper methods.

### Responsibilities

- Date formatting.
- File operations.
- String processing.
- Common utilities.

### Example

```text
DateUtils

FileUtils

StringUtils
```

Utility classes should be stateless.

---

# Exception Classes

## Purpose

Represent application-specific exceptions.

### Responsibilities

- Business exceptions.
- Validation exceptions.
- Resource exceptions.
- Authentication exceptions.

### Example

```text
BusinessException

ValidationException

ResourceNotFoundException

UnauthorizedException
```

Exception classes should represent a single error type.

---

# Class Dependency Guidelines

Allowed dependency flow:

```text
Controller
      │
      ▼
Service
      │
      ▼
Repository
      │
      ▼
Database
```

Supporting classes:

```text
Controller
      │
      ├── DTO
      └── Validation

Service
      ├── Repository
      ├── Mapper
      ├── Cache
      ├── Kafka
      ├── Security
      └── Utility

Repository
      └── Entity
```

Lower layers must never depend on higher layers.

---

# Dependency Injection Strategy

The application uses Constructor Injection.

Benefits:

- Easier testing.
- Immutable dependencies.
- Better readability.
- No hidden dependencies.
- Improved maintainability.

Example:

```java
@Service
public class UserServiceImpl implements UserService {

    private final UserRepository repository;

    public UserServiceImpl(UserRepository repository) {
        this.repository = repository;
    }
}
```

---

# Class Naming Conventions

| Component | Convention |
|------------|------------|
| Controller | UserController |
| Service | UserService |
| Implementation | UserServiceImpl |
| Repository | UserRepository |
| Entity | User |
| DTO | UserRequest, UserResponse |
| Mapper | UserMapper |
| Validator | EmailValidator |
| Config | KafkaConfig |
| Utility | DateUtils |
| Exception | UserNotFoundException |

---

# Design Best Practices

- One responsibility per class.
- Keep classes small and focused.
- Prefer composition over inheritance.
- Depend on interfaces.
- Avoid cyclic dependencies.
- Minimize mutable state.
- Keep utility classes stateless.
- Favor constructor injection.
- Write unit-testable classes.
- Follow clean code practices.

---

# Benefits

This class design provides:

- Better maintainability.
- High cohesion.
- Loose coupling.
- Easier testing.
- Improved scalability.
- Reusable components.
- Cleaner architecture.
- Simplified debugging.

---

# Summary

The Class Design defines the implementation blueprint for the KrewOps Recruitment Platform by assigning clear responsibilities to each class type and enforcing object-oriented design principles. Following layered architecture, SOLID principles, dependency injection, and consistent naming conventions ensures that the application remains modular, maintainable, scalable, and easy to extend as business requirements evolve.
