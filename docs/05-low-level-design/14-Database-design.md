# 15. Database Design

## Purpose

This chapter defines the Database Design for the KrewOps Recruitment Platform. The database layer is responsible for storing, managing, and retrieving application data while ensuring consistency, integrity, scalability, and high performance. PostgreSQL serves as the primary relational database for the platform.

---

# Objectives

The Database Design aims to:

- Store application data securely.
- Maintain referential integrity.
- Support transactional consistency.
- Optimize query performance.
- Ensure scalability.
- Minimize data redundancy.
- Enable efficient reporting and analytics.

---

# Database Architecture

```text
            Application
                 │
                 ▼
        Spring Data JPA
                 │
                 ▼
          Repository Layer
                 │
                 ▼
            PostgreSQL
                 │
                 ▼
          Persistent Storage
```

The Repository layer abstracts all database interactions.

---

# Database Technology

| Component | Technology |
|------------|------------|
| Database | PostgreSQL |
| ORM | Spring Data JPA |
| Migration | Flyway |
| Connection Pool | HikariCP |
| SQL Dialect | PostgreSQL SQL |

---

# High-Level Data Model

```text
Company
   │
   ├──────────────┐
   │              │
   ▼              ▼
User            Job
   │              │
   │              ▼
   │        Application
   │              ▲
   ▼              │
Role         Candidate
   │              │
   ▼              ▼
Permission   Interview
                     │
                     ▼
              Notification
```

---

# Core Tables

The primary database tables include:

- companies
- users
- roles
- permissions
- user_roles
- role_permissions
- candidates
- jobs
- applications
- interviews
- notifications

---

# Entity Relationships

| Parent | Child | Relationship |
|----------|---------|--------------|
| Company | Users | One-to-Many |
| Company | Jobs | One-to-Many |
| Company | Candidates | One-to-Many |
| Candidate | Applications | One-to-Many |
| Job | Applications | One-to-Many |
| Candidate | Interviews | One-to-Many |
| Job | Interviews | One-to-Many |
| User | Roles | Many-to-Many |
| Role | Permissions | Many-to-Many |

---

# Primary Keys

Every table contains a unique primary key.

Example:

```text
id BIGSERIAL PRIMARY KEY
```

Primary keys uniquely identify each record and support indexing.

---

# Foreign Keys

Foreign keys maintain referential integrity.

Examples:

```text
company_id

candidate_id

job_id

user_id

role_id
```

Foreign key constraints prevent orphaned records.

---

# Index Strategy

Indexes improve query performance.

Recommended indexes:

| Table | Indexed Columns |
|---------|----------------|
| users | email |
| users | company_id |
| candidates | email |
| jobs | company_id |
| applications | candidate_id |
| applications | job_id |
| interviews | candidate_id |
| notifications | user_id |

Composite indexes may be created for frequently filtered queries.

---

# Constraints

Database constraints enforce data integrity.

Examples:

- PRIMARY KEY
- FOREIGN KEY
- UNIQUE
- NOT NULL
- CHECK

Example:

```sql
email VARCHAR(255) UNIQUE NOT NULL
```

---

# Normalization

The schema follows Third Normal Form (3NF).

Benefits include:

- Reduced redundancy.
- Improved consistency.
- Easier maintenance.
- Better update performance.

---

# Transactions

All critical business operations execute within database transactions.

Examples:

- Candidate Registration
- Job Creation
- Interview Scheduling
- Role Assignment
- Notification Creation

Transactions ensure atomicity and consistency.

---

# Connection Pooling

The application uses HikariCP for efficient database connections.

Benefits:

- Faster request processing.
- Reduced connection overhead.
- Better resource utilization.
- High concurrency support.

---

# Database Migration

Flyway manages schema evolution.

Migration workflow:

```text
Application Startup
        │
        ▼
Check Migration History
        │
        ▼
Execute Pending Scripts
        │
        ▼
Update Schema Version
```

Migration scripts are version controlled.

---

# Soft Delete Strategy

Business records are retained using logical deletion where appropriate.

Example:

```text
status = INACTIVE

deleted = true

deleted_at = timestamp
```

This preserves historical information.

---

# Audit Columns

Every major table includes standard audit fields.

```text
created_by

created_date

updated_by

updated_date
```

These fields support traceability and compliance.

---

# Performance Optimization

Database optimization techniques include:

- Proper indexing.
- Query optimization.
- Pagination.
- Batch operations.
- Prepared statements.
- Connection pooling.
- Efficient joins.
- Avoiding N+1 queries.

---

# Backup Strategy

Database backups include:

- Daily full backups.
- Incremental backups.
- Transaction log backups.
- Backup verification.
- Disaster recovery procedures.

---

# Security

Database security measures include:

- TLS encryption.
- Least privilege access.
- Strong authentication.
- Encrypted backups.
- Parameterized queries.
- Audit logging.

Sensitive information should never be stored in plain text.

---

# Monitoring

Key database metrics include:

- Active connections.
- Slow queries.
- Query execution time.
- CPU usage.
- Memory usage.
- Deadlocks.
- Lock contention.
- Storage utilization.

Continuous monitoring helps maintain database performance.

---

# Best Practices

- Use normalized schemas.
- Define proper foreign keys.
- Create appropriate indexes.
- Keep transactions short.
- Use parameterized queries.
- Apply migrations through Flyway.
- Monitor database performance.
- Archive historical data when appropriate.
- Regularly verify backup and recovery procedures.

---

# Benefits

The Database Design provides:

- High data integrity.
- Strong consistency.
- Efficient querying.
- Improved scalability.
- Better maintainability.
- Reliable transactions.
- Simplified schema evolution.
- Enterprise-grade persistence.

---

# Summary

The Database Design establishes PostgreSQL as the reliable and scalable persistence layer for the KrewOps Recruitment Platform. By combining normalized schemas, referential integrity, indexing strategies, transactional consistency, migration management, and performance optimization techniques, the database layer provides a robust foundation for secure, efficient, and maintainable enterprise application development.
