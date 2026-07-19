# 03. Package Design

## Purpose

This chapter defines the package organization for the KrewOps Recruitment Platform. The package structure follows a layered architecture with clearly separated responsibilities, enabling modular development, maintainability, scalability, and ease of testing.

---

# Objectives

The package design aims to:

- Organize code into logical modules.
- Enforce separation of concerns.
- Improve maintainability.
- Encourage code reuse.
- Simplify navigation.
- Support scalable application development.
- Reduce coupling between components.

---

# Package Design Principles

The package organization follows these principles:

- Single Responsibility Principle (SRP)
- High Cohesion
- Low Coupling
- Layered Architecture
- Interface-driven Design
- Dependency Injection
- Clean Architecture practices

---

# Base Package

```text
com.krewops.recruitment
```

All application packages are organized under the common root package.

---

# Package Hierarchy

```text
com.krewops.recruitment
│
├── config
├── controller
├── service
│   └── impl
├── repository
├── entity
├── dto
│   ├── request
│   └── response
├── mapper
├── validation
├── exception
├── security
├── kafka
│   ├── producer
│   ├── consumer
│   └── config
├── cache
├── scheduler
├── integration
├── util
├── constants
└── common
```

Each package has a well-defined responsibility to avoid overlapping concerns.

---

# Package Responsibilities

## config

### Purpose

Contains all application configuration classes.

### Responsibilities

- Spring configuration
- Bean definitions
- Kafka configuration
- Redis configuration
- Database configuration
- Security configuration
- Swagger/OpenAPI configuration
- Cache configuration

### Example Classes

```text
KafkaConfig
RedisConfig
SwaggerConfig
SecurityConfig
DatabaseConfig
CacheConfig
```

---

## controller

### Purpose

Exposes REST APIs to client applications.

### Responsibilities

- API endpoints
- Request validation
- Response generation
- HTTP status handling
- API documentation

Controllers should never contain business logic.

### Example Classes

```text
UserController
JobController
CandidateController
InterviewController
AuthenticationController
```

---

## service

### Purpose

Contains business interfaces.

### Responsibilities

- Business contracts
- Service abstraction
- Workflow definition

### Example Interfaces

```text
UserService
JobService
CandidateService
InterviewService
```

---

## service.impl

### Purpose

Contains implementation of business services.

### Responsibilities

- Business rules
- Transaction management
- External integrations
- Repository coordination

### Example Classes

```text
UserServiceImpl
JobServiceImpl
InterviewServiceImpl
```

---

## repository

### Purpose

Handles persistence operations.

### Responsibilities

- CRUD operations
- Database queries
- Pagination
- Filtering
- Custom queries

### Example Interfaces

```text
UserRepository
JobRepository
InterviewRepository
```

---

## entity

### Purpose

Represents database entities.

### Responsibilities

- Table mapping
- Relationships
- Constraints
- ORM annotations

### Example Classes

```text
User
Job
Candidate
Interview
Role
Permission
```

---

## dto

### Purpose

Contains request and response objects.

### Responsibilities

- API request models
- API response models
- Data transfer
- Validation support

### Structure

```text
dto
│
├── request
└── response
```

### Example Classes

```text
CreateUserRequest
UpdateJobRequest
UserResponse
JobResponse
```

---

## mapper

### Purpose

Converts objects between different layers.

### Responsibilities

- Entity → DTO
- DTO → Entity
- Response mapping
- Request mapping

### Example Classes

```text
UserMapper
CandidateMapper
JobMapper
```

---

## validation

### Purpose

Contains reusable validation logic.

### Responsibilities

- Custom validators
- Annotation validators
- Business validation rules

### Example Classes

```text
EmailValidator
PasswordValidator
PhoneValidator
```

---

## exception

### Purpose

Provides centralized exception handling.

### Responsibilities

- Custom exceptions
- Global exception handler
- Error response generation

### Example Classes

```text
BusinessException
ResourceNotFoundException
ValidationException
UnauthorizedException
GlobalExceptionHandler
```

---

## security

### Purpose

Implements application security.

### Responsibilities

- Authentication
- Authorization
- JWT validation
- Role verification
- Security filters

### Example Classes

```text
JwtAuthenticationFilter
JwtTokenProvider
UserDetailsServiceImpl
SecurityConfiguration
```

---

## kafka

### Purpose

Handles asynchronous messaging.

### Structure

```text
kafka
│
├── producer
├── consumer
└── config
```

### Responsibilities

- Event publishing
- Event consumption
- Topic configuration
- Retry handling
- Dead Letter Queue (DLQ)

### Example Classes

```text
CandidateProducer
InterviewConsumer
KafkaProducerConfig
KafkaConsumerConfig
```

---

## cache

### Purpose

Provides caching support.

### Responsibilities

- Redis integration
- Cache eviction
- Cache population
- Cache configuration

### Example Classes

```text
UserCacheService
JobCacheService
CacheConfiguration
```

---

## scheduler

### Purpose

Executes scheduled background jobs.

### Responsibilities

- Cron jobs
- Cleanup jobs
- Notification scheduling
- Report generation

### Example Classes

```text
NotificationScheduler
CleanupScheduler
ReminderScheduler
```

---

## integration

### Purpose

Contains external service integrations.

### Responsibilities

- Email integration
- SMS integration
- Payment integration
- Third-party APIs

### Example Classes

```text
EmailClient
SmsClient
PaymentGatewayClient
```

---

## util

### Purpose

Provides reusable helper classes.

### Responsibilities

- Date utilities
- String utilities
- File utilities
- Common helper methods

### Example Classes

```text
DateUtils
StringUtils
FileUtils
CommonUtils
```

---

## constants

### Purpose

Stores application-wide constants.

### Responsibilities

- Error codes
- API constants
- Security constants
- Kafka topics
- Cache names

### Example Classes

```text
ApplicationConstants
KafkaTopics
ErrorCodes
SecurityConstants
```

---

## common

### Purpose

Contains reusable components shared across the application.

### Responsibilities

- Base classes
- Shared models
- Generic responses
- Pagination models
- Utility interfaces

---

# Package Dependency Rules

The dependency flow follows a strict layered architecture.

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

Supporting packages such as `config`, `security`, `mapper`, `validation`, `cache`, and `kafka` are consumed where appropriate but should not introduce cyclic dependencies.

---

# Package Naming Conventions

| Component | Naming Convention |
|------------|-------------------|
| Controller | UserController |
| Service | UserService |
| Service Implementation | UserServiceImpl |
| Repository | UserRepository |
| Entity | User |
| DTO | UserRequest, UserResponse |
| Mapper | UserMapper |
| Exception | UserNotFoundException |
| Configuration | KafkaConfig |
| Utility | DateUtils |
| Scheduler | CleanupScheduler |

---

# Best Practices

- Keep packages cohesive.
- Avoid cyclic dependencies.
- Follow one responsibility per package.
- Separate interfaces from implementations.
- Reuse common components.
- Keep utility classes stateless.
- Avoid placing unrelated classes in the same package.
- Use constructor-based dependency injection.
- Maintain consistent package naming across all modules.

---

# Benefits

The package design provides:

- Better maintainability
- Improved modularity
- Clear ownership of responsibilities
- Easier navigation
- Scalable architecture
- Simplified testing
- Consistent project organization
- Better collaboration among development teams

---

# Summary

The Package Design establishes a clear and maintainable organization for the KrewOps Recruitment Platform. By separating concerns into well-defined packages, enforcing dependency rules, and following consistent naming conventions, the design promotes modular development, scalability, code reuse, and long-term maintainability.
