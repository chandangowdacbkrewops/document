# 05. Stakeholders & User Personas

---

# 1. Introduction

KrewOps is a digital workforce marketplace that connects work owners with skilled workers, workforce providers, and service businesses through a trusted and transparent platform.

Unlike traditional recruitment platforms, KrewOps enables users to either publish work requirements or advertise their professional services. The platform facilitates workforce discovery, quotation management, bookings, payments, and reputation building.

Understanding the needs of each stakeholder is essential for designing intuitive user experiences, secure authorization, scalable workflows, and future platform capabilities.

---

# 2. Stakeholder Overview

| Stakeholder | Primary Goal | Interaction Level |
|-------------|--------------|------------------|
| Work Owner | Find trusted workers and complete work efficiently | Very High |
| Worker | Find work opportunities and increase earnings | Very High |
| Workforce Provider | Supply workers for work requests | High |
| Service Business | Advertise services and manage customer bookings | High |
| Platform Administrator | Manage and monitor the marketplace | High |
| Customer Support | Resolve user issues and disputes | Medium |
| Finance & Operations | Manage payments and settlements | Medium |

---

# 3. Work Owner Persona

## Profile

A Work Owner is an individual or business looking for skilled or semi-skilled workers to complete specific work.

Examples include:

- Home Owners
- Farmers
- Apartment Associations
- Shop Owners
- Contractors
- Small Businesses

### Responsibilities

- Register and verify account
- Create work requests
- Browse worker profiles
- Receive quotations
- Compare workers
- Book workers
- Track work progress
- Complete payments
- Rate completed work

### Goals

- Find trusted workers quickly
- Receive competitive quotations
- Transparent pricing
- Quality workmanship
- Timely work completion

### Pain Points

- Difficulty finding reliable workers
- Lack of pricing transparency
- Last-minute cancellations
- No trusted reviews
- Payment disputes

### Success Metrics

- Time to find worker
- Booking success rate
- Work completion rate
- Customer satisfaction
- Repeat bookings

---

# 4. Worker Persona

## Profile

Workers provide professional or skilled services through the KrewOps marketplace.

Examples include:

- Plumber
- Electrician
- Carpenter
- Painter
- Mason
- Driver
- Agriculture Worker
- Housekeeping Worker
- Welder
- General Labourer

### Responsibilities

- Create profile
- Verify identity
- Add skills
- Create service listings
- Browse work requests
- Submit quotations
- Accept bookings
- Complete assigned work
- Receive payments
- Maintain ratings

### Goals

- Receive regular work
- Increase income
- Build professional reputation
- Grow customer base

### Pain Points

- Finding customers
- Negotiating prices
- Payment delays
- Limited visibility

### Success Metrics

- Completed jobs
- Earnings
- Customer ratings
- Repeat customers

---

# 5. Workforce Provider Persona

## Profile

A Workforce Provider supplies multiple workers for large projects or recurring workforce requirements.

Examples include:

- Labour Contractors
- Workforce Agencies
- Staffing Providers

### Responsibilities

- Register workforce
- Manage workers
- Submit quotations
- Allocate workers
- Track ongoing work
- Manage workforce availability

### Goals

- Secure large contracts
- Efficient workforce utilization
- Improve client satisfaction

---

# 6. Service Business Persona

## Profile

A Service Business provides specialized workforce services under a registered business.

Examples include:

- Plumbing Company
- Electrical Service Provider
- Cleaning Company
- Painting Services
- Pest Control Services
- Agriculture Equipment Services

### Responsibilities

- Publish service offerings
- Manage technicians
- Accept bookings
- Schedule work
- Deliver services
- Manage customer relationships

### Goals

- Increase customer acquisition
- Build brand reputation
- Improve service quality
- Increase revenue

---

# 7. Platform Administrator Persona

## Responsibilities

- Manage categories
- Verify users
- Verify workers
- Moderate marketplace content
- Monitor fraud
- Manage disputes
- Configure platform settings
- Generate reports
- Monitor system health

### Goals

- Platform stability
- Marketplace trust
- Regulatory compliance
- Operational excellence

---

# 8. Customer Support Persona

## Responsibilities

- Resolve booking issues
- Handle payment disputes
- Assist account recovery
- Support verification requests
- Resolve customer complaints

### Success Metrics

- Resolution time
- Customer satisfaction
- First response time
- Ticket closure rate

---

# 9. Finance & Operations Persona

## Responsibilities

- Payment reconciliation
- Settlement processing
- Refund management
- Commission calculation
- Revenue reporting
- Financial compliance

---

# 10. Marketplace Interaction Matrix

| Stakeholder | Post Work | Post Service | Quote | Booking | Payment | Rating |
|-------------|-----------|--------------|-------|---------|---------|--------|
| Work Owner | ✓ | | | ✓ | ✓ | ✓ |
| Worker | | ✓ | ✓ | ✓ | | ✓ |
| Workforce Provider | | ✓ | ✓ | ✓ | | ✓ |
| Service Business | | ✓ | ✓ | ✓ | | ✓ |
| Platform Administrator | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

---

# 11. Permission Boundaries

Each stakeholder can only access resources required for their role.

Examples include:

- Work Owners can manage only their own work requests, bookings, and payments.
- Workers can manage only their own profile, services, quotations, and assigned work.
- Workforce Providers can manage only the workers associated with their organization.
- Service Businesses can manage only their services, bookings, and staff.
- Platform Administrators have access to global platform management functions.

Role-Based Access Control (RBAC) combined with fine-grained authorization ensures secure access across the marketplace.

---

# 12. Summary

KrewOps serves a diverse workforce ecosystem by connecting work owners, workers, workforce providers, and service businesses through a unified digital marketplace. Each stakeholder has clearly defined responsibilities, permissions, and goals that enable secure collaboration, transparent pricing, efficient bookings, digital payments, and reputation-based trust. This stakeholder model forms the foundation for the platform's business workflows, security model, and future product evolution.
