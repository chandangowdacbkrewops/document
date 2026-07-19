# 06. Workflow Engine

## Purpose

The Workflow Engine orchestrates the end-to-end recruitment lifecycle by controlling stage transitions, approvals, notifications, automation triggers, and SLA monitoring.

## Workflow Stages

1. Job Draft
2. Job Approval
3. Job Published
4. Candidate Applied
5. Resume Parsed
6. AI Screening
7. Recruiter Screening
8. Interview Scheduling
9. Interview Completed
10. Offer Approval
11. Offer Released
12. Offer Accepted
13. Onboarding
14. Hired

## Workflow Rules

- Each stage has configurable entry and exit criteria.
- Only authorized users may advance workflow stages.
- Mandatory approvals block progression until completed.
- Workflow events generate audit records.
- Notifications are sent on configurable milestones.

## Automation

- Auto-assign recruiters.
- Schedule reminders.
- Trigger AI matching after resume parsing.
- Generate onboarding tasks after offer acceptance.

## SLA Management

The engine tracks configurable SLAs for approvals, screening, interviews, and offers, with reminder and escalation support.

## Summary

The workflow engine provides a configurable, auditable process that ensures recruitment activities follow defined business policies while supporting automation and organizational customization.