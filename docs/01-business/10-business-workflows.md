# 10. Business Workflows

---

# 1. Introduction

Business workflows describe the sequence of activities performed by users and the system to achieve business objectives. These workflows ensure consistent execution of recruitment processes, improve collaboration between stakeholders, and provide a clear understanding of how KrewOps supports the complete hiring lifecycle.

The workflows documented in this chapter represent the logical business processes independent of technical implementation.

---

# 2. End-to-End Recruitment Workflow

```mermaid
flowchart TD

A[Recruiter Creates Job]
B[Job Approval]
C[Publish Job]
D[Candidate Applies]
E[Resume Screening]
F[Shortlist Candidate]
G[Interview Scheduling]
H[Conduct Interviews]
I[Collect Feedback]
J[Hiring Decision]
K[Generate Offer]
L[Candidate Response]
M[Employee Onboarding]

A --> B
B --> C
C --> D
D --> E
E --> F
F --> G
G --> H
H --> I
I --> J
J --> K
K --> L
L --> M
```

---

# 3. Job Creation Workflow

## Objective

Create and publish an approved job opening.

```mermaid
flowchart LR

Recruiter --> CreateJob
CreateJob --> SaveDraft
SaveDraft --> SubmitApproval
SubmitApproval --> HiringManager
HiringManager --> Approved
Approved --> Publish
Publish --> CareerPortal
```

### Actors

- Recruiter
- Hiring Manager
- HR Administrator

### Outcome

Approved job becomes available for applications.

---

# 4. Candidate Application Workflow

```mermaid
flowchart TD

Candidate --> Register
Register --> CompleteProfile
CompleteProfile --> UploadResume
UploadResume --> SearchJobs
SearchJobs --> ApplyJob
ApplyJob --> Confirmation
```

### Outcome

Application enters recruitment pipeline.

---

# 5. Resume Screening Workflow

```mermaid
flowchart TD

Application --> ResumeReview
ResumeReview --> SkillEvaluation
SkillEvaluation --> ExperienceEvaluation
ExperienceEvaluation --> ScreeningDecision

ScreeningDecision --> Shortlisted
ScreeningDecision --> Rejected
```

### Business Rules

- Duplicate applications prevented
- Mandatory qualifications validated
- Recruiter comments recorded

---

# 6. Interview Scheduling Workflow

```mermaid
flowchart TD

Shortlisted --> SelectInterviewers
SelectInterviewers --> CheckAvailability
CheckAvailability --> ScheduleInterview
ScheduleInterview --> SendInvitations
SendInvitations --> CandidateConfirmation
```

### System Actions

- Calendar invitation
- Email notification
- Reminder scheduling
- Audit logging

---

# 7. Interview Execution Workflow

```mermaid
flowchart TD

InterviewScheduled --> ConductInterview
ConductInterview --> CompleteScorecard
CompleteScorecard --> SubmitFeedback
SubmitFeedback --> HiringRecommendation
```

### Participants

- Candidate
- Interviewers
- Hiring Manager

---

# 8. Hiring Decision Workflow

```mermaid
flowchart TD

InterviewFeedback --> RecruiterReview
RecruiterReview --> HiringManagerReview
HiringManagerReview --> FinalDecision

FinalDecision --> Hire
FinalDecision --> Hold
FinalDecision --> Reject
```

### Decision Criteria

- Technical score
- Behavioral evaluation
- Experience
- Budget
- Team fit

---

# 9. Offer Approval Workflow

```mermaid
flowchart TD

OfferDraft --> RecruiterApproval
RecruiterApproval --> HRApproval
HRApproval --> FinanceApproval
FinanceApproval --> ExecutiveApproval
ExecutiveApproval --> OfferReleased
```

Organizations may configure approval levels based on internal policies.

---

# 10. Offer Acceptance Workflow

```mermaid
flowchart TD

OfferReleased --> CandidateReceivesOffer
CandidateReceivesOffer --> CandidateDecision

CandidateDecision --> Accept
CandidateDecision --> Reject
CandidateDecision --> Negotiate

Accept --> Onboarding
Reject --> CloseApplication
Negotiate --> RevisedOffer
```

---

# 11. User Provisioning Workflow

```mermaid
flowchart TD

Administrator --> InviteUser
InviteUser --> EmailInvitation
EmailInvitation --> Registration
Registration --> EmailVerification
EmailVerification --> ActivateAccount
```

---

# 12. Authentication Workflow

```mermaid
flowchart TD

Login --> ValidateCredentials
ValidateCredentials --> MFA
MFA --> GenerateSession
GenerateSession --> Dashboard
```

Failed authentication attempts shall be logged and handled according to organizational security policies.

---

# 13. Approval Workflow

```mermaid
flowchart TD

BusinessRequest --> SubmitApproval
SubmitApproval --> Reviewer

Reviewer --> Approve
Reviewer --> Reject
Reviewer --> RequestChanges

Approve --> NextApproval
Reject --> End
RequestChanges --> SubmitApproval
```

This workflow is reusable for jobs, offers, and administrative requests.

---

# 14. Notification Workflow

```mermaid
flowchart TD

BusinessEvent --> NotificationEngine
NotificationEngine --> Email
NotificationEngine --> SMS
NotificationEngine --> WhatsApp
NotificationEngine --> PushNotification
NotificationEngine --> InAppNotification
```

Supported business events include:

- Registration
- Job Published
- Application Submitted
- Interview Scheduled
- Offer Released
- Offer Accepted

---

# 15. Candidate Status Workflow

```mermaid
stateDiagram-v2

[*] --> Registered
Registered --> Applied
Applied --> Screening
Screening --> Shortlisted
Screening --> Rejected
Shortlisted --> InterviewScheduled
InterviewScheduled --> InterviewCompleted
InterviewCompleted --> OfferPending
OfferPending --> Offered
Offered --> Accepted
Offered --> Rejected
Accepted --> Joined
Rejected --> [*]
Joined --> [*]
```

---

# 16. Job Lifecycle Workflow

```mermaid
stateDiagram-v2

[*] --> Draft
Draft --> PendingApproval
PendingApproval --> Approved
Approved --> Published
Published --> Closed
Closed --> Archived
Archived --> [*]
```

---

# 17. Offer Lifecycle Workflow

```mermaid
stateDiagram-v2

[*] --> Draft
Draft --> Approval
Approval --> Released
Released --> Accepted
Released --> Rejected
Released --> Expired
Accepted --> Joined
```

---

# 18. Workflow Exception Handling

The platform shall support exception handling for common scenarios:

| Scenario | Expected Action |
|----------|-----------------|
| Candidate Withdraws | Close application and notify recruiter |
| Interview Cancelled | Reschedule or close interview |
| Offer Expired | Update status and notify recruiter |
| Approval Rejected | Return workflow to previous stage |
| User Deactivated | Reassign ownership of active work |

---

# 19. Workflow Monitoring

The system shall provide visibility into workflow execution, including:

- Current workflow stage
- Pending approvals
- Bottlenecks
- Average processing time
- SLA breaches
- Escalations
- Historical workflow execution

---

# 20. Workflow Configuration

Organizations shall configure:

- Recruitment stages
- Approval levels
- Notification triggers
- Escalation rules
- SLA thresholds
- Workflow transitions
- Auto-approval conditions

Configuration changes shall not affect historical workflow executions.

---

# 21. Workflow Audit Requirements

Every workflow execution shall record:

- Workflow instance identifier
- Current stage
- Previous stage
- User performing action
- Timestamp
- Comments
- Approval decision
- Outcome

Workflow history shall be immutable and available for audit and reporting.

---

# 22. Summary

Business workflows define the operational processes that drive recruitment activities within KrewOps. From job creation through onboarding, each workflow ensures consistent execution, accountability, traceability, and collaboration across all stakeholders. By combining configurable workflows with comprehensive audit trails and automation, the platform enables organizations to standardize hiring practices while remaining flexible enough to support diverse business requirements.
