# 02. Project Structure

## Purpose

This chapter defines the logical and physical organization of the KrewOps Recruitment Platform source code. A well-defined project structure improves maintainability, scalability, readability, collaboration, and consistency across development teams.

---

# Objectives

The project structure aims to:

- Organize source code into logical modules.
- Enforce separation of concerns.
- Improve code maintainability.
- Support scalable application development.
- Enable easier onboarding for developers.
- Promote reusable and modular components.
- Simplify testing and deployment.

---

# Architecture Style

The application follows a layered architecture with clear separation between presentation, business logic, persistence, and infrastructure layers.

```text
┌──────────────────────────────┐
│      Client Applications     │
│ (Web, Mobile, External APIs) │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│      Controller Layer        │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│        Service Layer         │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│      Repository Layer        │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│        PostgreSQL DB         │
└──────────────────────────────┘
```

---

# High-Level Project Layout

```text
krewops-recruitment-platform
│
├── src
│   ├── main
│   │   ├── java
│   │   └── resources
│   │
│   └── test
│       ├── java
│       └── resources
│
├── docs
├── docker
├── scripts
├── helm
├── .github
├── pom.xml
└── README.md
```

---

# Source Code Organization

```text
src/main/java
└── com
    └── krewops
        └── recruitment
```

The base package contains all application components following a layered package organization.

---

# Package Organization

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
├── mapper
├── security
├── kafka
├── cache
├── scheduler
├── exception
├── util
├── validation
└── constants
```

Each package has a single, well-defined responsibility.

---

# Layer Responsibilities

## Controller Layer

Responsibilities:

- REST endpoints
- Request validation
- Response generation
- Authentication checks
- API documentation

Controllers should not contain business logic.

---

## Service Layer

Responsibilities:

- Business rules
- Workflow orchestration
- Transaction management
- Integration with repositories
- External service coordination

The service layer acts as the core of the application.

---

## Repository Layer

Responsibilities:

- Database operations
- CRUD functionality
- Custom database queries
- Pagination
- Data persistence

Repositories interact directly with the database.

---

## Entity Layer

Responsibilities:

- Database table mapping
- ORM configuration
- Entity relationships
- Primary keys
- Constraints

Entities represent persistent domain objects.

---

## DTO Layer

Responsibilities:

- API request models
- API response models
- Data transfer
- Validation support

DTOs prevent direct exposure of entities.

---

## Mapper Layer

Responsibilities:

- Entity to DTO conversion
- DTO to Entity conversion
- Model transformation
- Object mapping

Mapping logic remains isolated from business logic.

---

## Security Layer

Responsibilities:

- Authentication
- Authorization
- JWT validation
- Security filters
- Role management

All security-related implementations reside within this package.

---

## Configuration Layer

Responsibilities:

- Spring Beans
- Kafka configuration
- Redis configuration
- Security configuration
- Swagger/OpenAPI configuration
- Database configuration

Configuration classes centralize infrastructure settings.

---

# Resource Structure

```text
src/main/resources
│
├── application.yml
├── application-dev.yml
├── application-test.yml
├── application-prod.yml
├── db
│   └── migration
├── static
├── templates
└── logback.xml
```

The resources directory stores application configuration, logging, database migrations, and static assets.

---

# Test Structure

```text
src/test/java
│
├── controller
├── service
├── repository
├── integration
└── util
```

Tests follow the same package hierarchy as production code to improve maintainability and traceability.

---

# Build Structure

The project uses Maven for dependency management and build automation.

Key build responsibilities include:

- Dependency management
- Compilation
- Unit testing
- Integration testing
- Packaging
- Code quality checks
- Artifact generation

---

# Configuration Management

Environment-specific configuration is separated using Spring Profiles.

Examples:

- Development
- Testing
- Staging
- Production

Sensitive information such as passwords and API keys must never be stored in source code.

---

# Dependency Flow

The application follows a unidirectional dependency model.

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

Lower layers should never depend on higher layers.

---

# Naming Conventions

The project follows consistent naming standards.

Examples:

| Component | Naming Convention |
|-----------|-------------------|
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

---

# Development Guidelines

The project follows the following principles:

- Single Responsibility Principle
- Separation of Concerns
- Dependency Injection
- Constructor Injection
- Interface-based programming
- Immutable DTOs where possible
- Reusable utility components
- Consistent package organization
- Clean code practices
- Comprehensive unit testing

---

# Benefits of the Project Structure

This structure provides:

- Improved maintainability
- Better readability
- Easier scalability
- Clear ownership of components
- Simplified testing
- Modular development
- Faster onboarding
- Consistent coding practices

---

# Summary

The Project Structure defines the overall organization of the KrewOps Recruitment Platform, ensuring a modular, maintainable, and scalable codebase. By enforcing layered architecture, clear package responsibilities, standardized naming conventions, and consistent development practices, the project structure establishes a solid foundation for efficient software development and long-term maintainability.
