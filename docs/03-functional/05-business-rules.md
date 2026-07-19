# 05. Business Rules

## Purpose

This chapter defines the business rules governing the KrewOps Recruitment Platform.

## Core Business Rules

### Organization
- Every user belongs to exactly one organization.
- Organization administrators manage only their own organization.

### Users
- Email addresses must be unique within an organization.
- Only active users may access the system.

### Jobs
- A job must be approved before publishing.
- Closed jobs cannot accept new applications.

### Candidates
- A candidate may apply to multiple jobs.
- Duplicate candidates should be detected using configurable matching criteria.

### Resume Processing
- Supported file types are validated before parsing.
- Parsing failures must not discard uploaded resumes.

### AI Matching
- Match scores are recommendations and do not automatically reject candidates.

### Interviews
- Interview feedback is required before a hiring decision.

### Offers
- Offers require configured approvals before release.
- Accepted offers cannot be modified.

### Onboarding
- Onboarding begins only after offer acceptance.

### Notifications
- Critical workflow events generate notifications.

### Audit
- All security-sensitive actions must be audited.

## Summary

These business rules ensure consistent execution of recruitment workflows across all organizations while supporting configurable policies where required.