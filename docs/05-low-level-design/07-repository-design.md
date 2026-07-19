# 07. Repository Design

## Purpose

This chapter defines the Repository layer of the KrewOps Recruitment Platform. The Repository layer abstracts all database interactions and provides a clean interface for performing CRUD operations, custom queries, pagination, filtering, and data persistence. It isolates persistence logic from the business layer, allowing services to focus solely on business rules.

---

# Objectives

The Repository Design aims to:

- Encapsulate database operations.
- Separate persistence logic from business logic.
- Simplify CRUD operations.
- Support custom database queries.
- Enable pagination and sorting.
- Improve maintainability.
- Facilitate unit and integration testing.
- Support future database changes with minimal impact.

---

# Repository Layer Architecture

```text
          Controller
               │
               ▼
          Service Layer
               │
               ▼
      Repository Interface
               │
               ▼
 Spring Data JPA Repository
               │
               ▼
          PostgreSQL
```

Repositories provide a clean abstraction over the persistence layer.

---

# Responsibilities

The Repository layer is responsible for:

- CRUD operations.
- Entity persistence.
- Custom JPQL queries.
- Native SQL queries.
- Pagination.
- Sorting.
- Filtering.
- Optimistic locking support.
- Batch operations.
- Data retrieval.

Repositories should **not**:

- Implement business logic.
- Perform request validation.
- Manage transactions.
- Generate HTTP responses.
- Publish Kafka events.

---

# Package Structure

```text
repository
│
├── UserRepository
├── CandidateRepository
├── CompanyRepository
├── JobRepository
├── InterviewRepository
├── RoleRepository
├── PermissionRepository
└── NotificationRepository
```

Each repository corresponds to a primary domain entity.

---

# Repository Pattern

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

The Service layer communicates only with Repository interfaces.

---

# Repository Interface Design

Repositories extend Spring Data JPA interfaces.

Example:

```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {

}
```

Benefits include:

- Built-in CRUD operations.
- Paging support.
- Sorting support.
- Dynamic query generation.
- Reduced boilerplate code.

---

# Standard CRUD Operations

Every repository supports standard operations such as:

```text
save()

saveAll()

findById()

findAll()

existsById()

count()

delete()

deleteById()

deleteAll()
```

These operations are inherited from the base repository interface.

---

# Custom Query Methods

Spring Data JPA derives queries directly from method names.

Examples:

```java
findByEmail(String email)

findByStatus(String status)

findByCompanyId(Long companyId)

findByUsername(String username)

existsByEmail(String email)
```

Method names should clearly describe the intended query.

---

# JPQL Queries

Complex queries can be implemented using JPQL.

Example:

```java
@Query("SELECT j FROM Job j WHERE j.status = :status")
List<Job> findActiveJobs(String status);
```

JPQL operates on entities rather than database tables.

---

# Native SQL Queries

Native SQL is used only when JPQL cannot satisfy performance or functionality requirements.

Example:

```java
@Query(value = "SELECT * FROM jobs WHERE salary > :salary",
       nativeQuery = true)
List<Job> findJobsBySalary(Double salary);
```

Native queries should be minimized for portability.

---

# Pagination

Repositories support pagination through Spring Data.

Example:

```java
Page<Job> findAll(Pageable pageable);
```

Benefits include:

- Reduced database load.
- Improved API performance.
- Efficient handling of large datasets.

---

# Sorting

Sorting is supported using the `Sort` abstraction.

Example:

```java
findAll(Sort.by("createdDate").descending());
```

Multiple sort fields can also be combined.

---

# Filtering

Repositories support filtering using derived methods or custom queries.

Examples:

```java
findByStatus()

findByDepartment()

findByExperienceGreaterThan()

findByCreatedDateBetween()

findByCompanyName()
```

---

# Batch Operations

Repositories support batch persistence.

Examples:

```java
saveAll()

deleteAll()

deleteAllById()
```

Batch operations reduce database round trips and improve performance.

---

# Entity Relationships

Repositories manage entities with relationships such as:

```text
Company
    │
    ├── Jobs
    ├── Users
    └── Interviews

Candidate
    │
    ├── Skills
    ├── Applications
    └── Interviews
```

Relationship management is handled through JPA mappings.

---

# Transaction Support

Repositories participate in transactions managed by the Service layer.

```text
Controller
      │
      ▼
Service (@Transactional)
      │
      ▼
Repository
      │
      ▼
Database
```

Repositories should not define transaction boundaries unless specifically required.

---

# Exception Handling

Repository exceptions include:

- DataIntegrityViolationException
- EmptyResultDataAccessException
- OptimisticLockException
- ConstraintViolationException

These exceptions are translated into business exceptions within the Service layer.

---

# Performance Considerations

Repository implementations should:

- Use indexes efficiently.
- Fetch only required columns.
- Avoid unnecessary joins.
- Minimize N+1 query issues.
- Use pagination for large datasets.
- Optimize custom queries.
- Leverage caching where appropriate.

---

# Naming Conventions

| Component | Convention |
|------------|------------|
| Repository | UserRepository |
| Finder Method | findByEmail() |
| Exists Method | existsByUsername() |
| Count Method | countByStatus() |
| Delete Method | deleteById() |
| Custom Query | findActiveCandidates() |

---

# Repository Best Practices

- Keep repositories focused on persistence.
- Avoid business logic.
- Prefer derived query methods where possible.
- Use JPQL before native SQL.
- Return Optional for nullable single results.
- Implement pagination for list APIs.
- Keep query methods readable.
- Optimize queries for performance.
- Use projections when only partial data is required.

---

# Benefits

The Repository Design provides:

- Clean separation of persistence logic.
- Reduced boilerplate code.
- Easier maintenance.
- Better database abstraction.
- Improved scalability.
- Simplified testing.
- Consistent data access patterns.
- Enhanced performance through optimized queries.

---

# Summary

The Repository Design establishes a robust persistence layer for the KrewOps Recruitment Platform by encapsulating all database interactions within dedicated repository interfaces. Leveraging Spring Data JPA, derived queries, JPQL, native SQL where necessary, pagination, and optimized data access patterns, the Repository layer provides a scalable, maintainable, and efficient foundation for all application persistence requirements while maintaining a clear separation from business logic.
