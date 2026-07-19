# 07. State Machines

## Purpose

This chapter defines the lifecycle states and valid transitions for the major business entities managed by KrewOps.

## Job States

Draft → Pending Approval → Approved → Published → On Hold → Closed → Archived

Rules:
- Only approved jobs may be published.
- Archived jobs are read-only.

## Candidate States

Applied → Resume Parsed → AI Screened → Recruiter Reviewed → Shortlisted → Interview Scheduled → Interviewed → Selected → Offered → Hired

Alternate terminal states:
- Rejected
- Withdrawn

## Interview States

Scheduled → Confirmed → In Progress → Completed → Feedback Submitted → Closed

Cancelled may occur before completion.

## Offer States

Draft → Pending Approval → Approved → Released → Accepted

Alternate states:
- Rejected
- Expired
- Withdrawn

## Onboarding States

Initiated → Documents Pending → Verification → Ready to Join → Joined → Completed

## State Transition Rules

- Invalid state transitions are rejected.
- Every transition is audited.
- Configured notifications may be triggered after transitions.
- Permissions determine who may perform each transition.

## Summary

State machines ensure every business object follows a controlled lifecycle with predictable transitions, traceability, and enforcement of business policies.