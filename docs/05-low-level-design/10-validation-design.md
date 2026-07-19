# 10. Validation Design

## Purpose

This chapter defines the Validation Design for the KrewOps Recruitment Platform. Validation ensures that all incoming requests satisfy business and data integrity requirements before they are processed by the application. A consistent validation strategy improves application reliability, security, and user experience.

---

# Objectives

The Validation Design aims to:

- Validate incoming API requests.
- Prevent invalid data from entering the system.
- Improve application security.
- Enforce business rules.
- Reduce runtime errors.
- Provide consistent validation responses.
- Improve API usability.

---

# Validation Architecture

```text
              Client
                 │
                 ▼
           HTTP Request
                 │
                 ▼
            Controller
                 │
          @Valid Annotation
                 │
                 ▼
      Bean Validation Engine
                 │
        Validation Successful?
          │               │
         Yes             No
          │               │
          ▼               ▼
      Service Layer   Validation Error
          │               │
          ▼               ▼
      Business Logic  Error Response
```

---

# Validation Layers

Validation is performed at multiple levels.

| Layer | Responsibility |
|--------|----------------|
| Client | Basic input validation |
| Controller | Request validation |
| Service | Business validation |
| Database | Constraint validation |

---

# Request Validation

All request DTOs use Jakarta Bean Validation annotations.

Example:

```java
public class CreateUserRequest {

    @NotBlank
    private String firstName;

    @NotBlank
    private String lastName;

    @Email
    private String email;

    @Pattern(regexp = "^[0-9]{10}$")
    private String phoneNumber;
}
```

Validation is triggered automatically using the `@Valid` annotation.

---

# Common Validation Annotations

| Annotation | Purpose |
|------------|---------|
| @NotNull | Value cannot be null |
| @NotBlank | String cannot be blank |
| @NotEmpty | Collection or String cannot be empty |
| @Email | Valid email format |
| @Pattern | Regular expression validation |
| @Size | Length validation |
| @Min | Minimum numeric value |
| @Max | Maximum numeric value |
| @Positive | Positive numbers only |
| @PositiveOrZero | Positive or zero |
| @Past | Date must be in the past |
| @Future | Date must be in the future |

---

# Controller Validation

Controllers validate incoming requests before invoking business logic.

Example:

```java
@PostMapping
public ResponseEntity<UserResponse> createUser(
        @Valid @RequestBody CreateUserRequest request) {

    return ResponseEntity.ok(userService.createUser(request));
}
```

If validation fails, the request never reaches the Service layer.

---

# Service-Level Validation

Business rules that cannot be expressed using annotations are validated in the Service layer.

Examples:

- Email address must be unique.
- Candidate cannot apply for the same job twice.
- Closed jobs cannot accept applications.
- Interview time must not overlap.
- Company subscription must be active.
- User account must be enabled.

---

# Database Validation

The database provides an additional layer of validation through constraints.

Typical constraints include:

- Primary Keys
- Foreign Keys
- Unique Constraints
- Check Constraints
- NOT NULL Constraints

Example:

```sql
email VARCHAR(255) UNIQUE NOT NULL
```

---

# Validation Flow

```text
Client Request
      │
      ▼
DTO Validation
      │
      ▼
Controller
      │
      ▼
Business Validation
      │
      ▼
Repository
      │
      ▼
Database Constraints
```

Each stage validates data before proceeding to the next.

---

# Custom Validators

Complex business rules can be implemented using custom validators.

Examples:

- UniqueEmailValidator
- PasswordStrengthValidator
- InterviewScheduleValidator
- CompanySubscriptionValidator
- DuplicateApplicationValidator

Custom validators encapsulate reusable validation logic.

---

# Cross-Field Validation

Some validations depend on multiple fields.

Examples:

- Start Date must be before End Date.
- Minimum Salary must not exceed Maximum Salary.
- Interview End Time must be after Start Time.
- Notice Period cannot exceed Experience.

These rules are implemented using custom validation logic.

---

# Error Handling

Validation failures return standardized error responses.

Example:

```json
{
  "success": false,
  "message": "Validation failed",
  "errors": [
    "Email is required",
    "Phone number is invalid",
    "Password must contain at least one special character"
  ],
  "timestamp": "2026-07-19T11:00:00Z"
}
```

---

# Validation Categories

## Required Field Validation

Examples:

- First Name
- Last Name
- Email
- Password
- Job Title

---

## Format Validation

Examples:

- Email format
- Phone number format
- URL format
- Date format

---

## Length Validation

Examples:

- Username length
- Password length
- Job description length

---

## Range Validation

Examples:

- Experience years
- Salary
- Notice period
- Interview duration

---

## Business Validation

Examples:

- Duplicate email addresses.
- Candidate already applied.
- Company subscription expired.
- Interview schedule conflict.
- Invalid role assignment.

---

# Validation Sequence

```text
Required Fields
       │
       ▼
Data Format
       │
       ▼
Length & Range
       │
       ▼
Business Rules
       │
       ▼
Database Constraints
```

Validations are executed from the simplest to the most expensive checks.

---

# Security Considerations

Validation helps protect the application against:

- Invalid input
- SQL Injection
- Cross-Site Scripting (XSS)
- Malformed JSON payloads
- Buffer overflow attempts
- Data corruption

Validation complements, but does not replace, security controls.

---

# Best Practices

- Validate all external input.
- Use DTO validation instead of entity validation for API requests.
- Keep business validation in the Service layer.
- Return clear and actionable error messages.
- Avoid exposing internal implementation details.
- Reuse validation logic through custom validators.
- Validate data at every system boundary.
- Combine application validation with database constraints.

---

# Benefits

The Validation Design provides:

- Improved data quality.
- Better application security.
- Consistent API behavior.
- Reduced runtime failures.
- Stronger business rule enforcement.
- Better user experience.
- Easier maintenance.
- Improved system reliability.

---

# Summary

The Validation Design establishes a comprehensive strategy for validating all incoming data within the KrewOps Recruitment Platform. By combining Bean Validation, business rule validation, database constraints, and standardized error handling, the application ensures data integrity, enhances security, and delivers a consistent and reliable API experience.
