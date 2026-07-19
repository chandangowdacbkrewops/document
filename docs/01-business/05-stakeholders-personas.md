# 05. Stakeholders & User Personas

---

# 1. Introduction

KrewOps serves multiple stakeholders across the hiring ecosystem. Unlike traditional recruitment platforms that optimize only for recruiters, KrewOps is designed as a collaborative platform where employers, recruiters, hiring managers, interviewers, candidates, and administrators each have clearly defined responsibilities and experiences.

Understanding these stakeholders is essential for defining product functionality, security boundaries, workflow ownership, and future feature development.

---

# 2. Stakeholder Overview

| Stakeholder | Primary Goal | Interaction Level |
|-------------|--------------|------------------|
| Organization | Hire quality talent efficiently | High |
| HR Administrator | Configure organization and users | High |
| Recruiter | Source and manage candidates | Very High |
| Hiring Manager | Evaluate candidates and make hiring decisions | High |
| Interviewer | Conduct interviews and submit feedback | Medium |
| Candidate | Apply for jobs and track application status | High |
| Platform Administrator | Manage platform operations | High |
| Support Team | Resolve customer issues | Medium |
| Finance Team | Subscription and billing management | Medium |
| Executive Leadership | Analytics and hiring insights | Medium |

---

# 3. Organization

## Description

Organizations subscribe to KrewOps to streamline recruitment operations across departments.

### Responsibilities

- Manage company profile
- Purchase subscriptions
- Invite recruiters
- Configure hiring workflows
- Define interview processes
- View organization analytics
- Manage compliance
- Configure permissions
- Maintain hiring policies

### Goals

- Reduce hiring time
- Improve candidate quality
- Standardize recruitment
- Increase recruiter productivity
- Improve employer branding

---

# 4. HR Administrator Persona

## Profile

The HR Administrator is responsible for configuring and maintaining the recruitment platform within the organization.

### Responsibilities

- Create users
- Assign roles
- Configure permissions
- Manage departments
- Configure hiring stages
- Maintain interview templates
- Manage job approval workflows
- Configure notifications

### Pain Points

- Manual configuration
- Multiple disconnected systems
- Inconsistent hiring process
- Permission management complexity

### Success Metrics

- Faster onboarding
- Reduced administrative effort
- Standardized workflows
- Secure access management

---

# 5. Recruiter Persona

## Profile

Recruiters spend most of their time sourcing, screening, communicating, and coordinating interviews.

### Responsibilities

- Create job openings
- Publish jobs
- Search candidates
- Review resumes
- Schedule interviews
- Communicate with candidates
- Coordinate interviewers
- Update application status
- Generate offers

### Goals

- Hire faster
- Improve candidate quality
- Reduce manual work
- Better collaboration
- Increase offer acceptance

### Pain Points

- Resume overload
- Scheduling conflicts
- Poor communication
- Manual status updates
- Tracking candidate history

### KPIs

- Time to hire
- Time to shortlist
- Offer acceptance rate
- Candidate response rate
- Recruiter productivity

---

# 6. Hiring Manager Persona

## Profile

Hiring Managers own the final hiring decision.

### Responsibilities

- Approve job requests
- Review shortlisted candidates
- Participate in interviews
- Submit interview decisions
- Approve offers
- Monitor hiring progress

### Goals

- Hire skilled employees
- Reduce hiring delays
- Improve interview quality
- Better collaboration with recruiters

### Pain Points

- Lack of candidate visibility
- Delayed interview feedback
- Poor interview coordination
- Long hiring cycles

---

# 7. Interviewer Persona

## Profile

Interviewers evaluate candidate skills and submit structured feedback.

### Responsibilities

- Accept interview invitations
- Conduct interviews
- Submit scorecards
- Recommend hiring decisions
- Provide technical assessments

### Goals

- Consistent evaluations
- Objective feedback
- Efficient interview process

### Pain Points

- Missing candidate information
- Manual feedback forms
- Scheduling issues

---

# 8. Candidate Persona

## Profile

Candidates interact with KrewOps throughout the recruitment lifecycle.

### Responsibilities

- Create profile
- Upload resume
- Apply for jobs
- Schedule interviews
- Attend interviews
- Receive updates
- Accept offers

### Goals

- Easy application process
- Transparent communication
- Quick feedback
- Professional experience

### Pain Points

- No status visibility
- Delayed responses
- Repeated data entry
- Poor interview scheduling

### Candidate Journey

1. Register
2. Complete profile
3. Upload resume
4. Search jobs
5. Apply
6. Screening
7. Interview
8. Offer
9. Join organization

---

# 9. Platform Administrator Persona

## Responsibilities

- Tenant management
- User management
- Subscription management
- Security monitoring
- System configuration
- Feature enablement
- Platform analytics
- Audit management

### Goals

- Platform stability
- Customer satisfaction
- Security compliance
- Operational excellence

---

# 10. Support Team Persona

### Responsibilities

- Resolve customer issues
- Manage tickets
- Monitor incidents
- Escalate technical problems
- Provide onboarding assistance

### Success Metrics

- Resolution time
- Customer satisfaction
- First response time

---

# 11. Finance Persona

### Responsibilities

- Subscription billing
- Invoice management
- Payment reconciliation
- Financial reporting
- Refund processing

---

# 12. Executive Leadership Persona

### Responsibilities

- Review hiring performance
- Analyze recruitment metrics
- Workforce planning
- Budget monitoring
- Strategic hiring decisions

### Key Dashboards

- Hiring velocity
- Recruitment cost
- Offer acceptance rate
- Recruiter productivity
- Department hiring status

---

# 13. Stakeholder Interaction Matrix

| Stakeholder | Jobs | Candidates | Interviews | Offers | Reports |
|-------------|------|------------|------------|--------|----------|
| Organization | ✓ | ✓ | ✓ | ✓ | ✓ |
| HR Admin | ✓ | ✓ | ✓ | ✓ | ✓ |
| Recruiter | ✓ | ✓ | ✓ | ✓ | ✓ |
| Hiring Manager | ✓ | ✓ | ✓ | ✓ | ✓ |
| Interviewer | | ✓ | ✓ | | |
| Candidate | ✓ | ✓ | ✓ | ✓ | |
| Platform Admin | ✓ | ✓ | ✓ | ✓ | ✓ |

---

# 14. Permission Boundaries

Each stakeholder must only access information required for their role.

Examples include:

- Recruiters cannot access another organization's data.
- Interviewers can only view candidates assigned to them.
- Candidates can only view their own applications.
- Hiring Managers can only access jobs within their departments.
- HR Administrators manage users only within their organization.
- Platform Administrators manage global platform settings.

Role-Based Access Control (RBAC) combined with fine-grained authorization ensures secure separation of responsibilities across the platform.

---

# 15. Summary

Clearly defined stakeholders and user personas ensure that KrewOps delivers tailored experiences for every participant in the recruitment lifecycle. By understanding the goals, responsibilities, challenges, and success metrics of each persona, the platform can provide intuitive workflows, secure access controls, and efficient collaboration that collectively improve hiring outcomes.
