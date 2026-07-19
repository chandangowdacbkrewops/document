# 08. Data Validation

## Purpose

This chapter defines validation rules that ensure data quality, consistency, and integrity throughout the KrewOps Recruitment Platform.

## Validation Categories

- Mandatory field validation
- Data type validation
- Format validation
- Length validation
- Range validation
- Cross-field validation
- Business rule validation
- Duplicate detection
- File validation
- API request validation

## General Rules

- Required fields must not be empty.
- Email addresses must follow RFC-compliant format.
- Phone numbers must follow configured country formats.
- Dates must be valid and logically consistent.

## Job Validation

- Job title is mandatory.
- Hiring manager must exist.
- Closing date cannot precede opening date.

## Candidate Validation

- Candidate email should be unique within configurable constraints.
- Resume upload is required before AI screening.

## Resume Validation

- Supported file formats: PDF and DOCX.
- File size must not exceed configured limits.
- Corrupted documents are rejected.

## API Validation

- Request schema validation.
- Authentication validation.
- Authorization validation.
- Payload sanitization.

## Error Reporting

Validation failures return clear, field-specific messages without exposing internal implementation details.

## Summary

Consistent validation ensures reliable workflows, improves data quality, and prevents invalid business operations across the recruitment lifecycle.