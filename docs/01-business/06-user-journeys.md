# 06. User Journeys

---

# 1. Introduction

User journeys describe how different users interact with the KrewOps marketplace to achieve their goals. These journeys define the end-to-end experience for work owners, workers, workforce providers, service businesses, and platform administrators.

KrewOps supports two primary business models:

1. Work Owner posts work and receives quotations from workers.
2. Worker or Service Business advertises services and receives bookings directly from work owners.

These journeys form the foundation for product design, workflows, APIs, notifications, and business rules.

---

# 2. Marketplace Journey Overview

KrewOps supports two primary marketplace journeys.

## Journey A – Work Request Marketplace

```text
Register
    │
    ▼
Create Profile
    │
    ▼
Post Work
    │
    ▼
Workers Discover Work
    │
    ▼
Workers Submit Quotes
    │
    ▼
Owner Reviews Quotes
    │
    ▼
Worker Selected
    │
    ▼
Booking Created
    │
    ▼
Work Started
    │
    ▼
Work Completed
    │
    ▼
Payment
    │
    ▼
Rating & Review
```

---

## Journey B – Service Marketplace

```text
Worker Registers
        │
        ▼
Create Service Listing
        │
        ▼
Owner Searches Service
        │
        ▼
View Worker Profile
        │
        ▼
Book Worker
        │
        ▼
Booking Confirmation
        │
        ▼
Work Completed
        │
        ▼
Payment
        │
        ▼
Rating & Review
```

---

# 3. Work Owner Journey

## Objective

Find trusted workers quickly and complete work efficiently.

### Journey

### Step 1 – Register

- Mobile number verification
- Profile creation

### Step 2 – Post Work

Provide:

- Category
- Description
- Location
- Preferred date
- Budget (Optional)
- Photos (Optional)

### Step 3 – Receive Quotations

Work owners receive quotations from interested workers including:

- Price
- Estimated duration
- Worker rating
- Experience

### Step 4 – Compare Workers

Compare:

- Ratings
- Reviews
- Price
- Distance
- Experience
- Availability

### Step 5 – Book Worker

Select worker.

System creates booking.

### Step 6 – Track Work

View

- Booking status
- Worker arrival
- Work progress

### Step 7 – Payment

Complete payment after work completion.

### Step 8 – Rating

Rate worker and provide review.

---

# 4. Worker Journey

## Objective

Receive work opportunities and grow income.

### Step 1 – Register

OTP verification.

### Step 2 – Complete Profile

Add

- Skills
- Experience
- Service areas
- Photos
- Identity verification

### Step 3 – Publish Services

Create service listings.

OR

Browse work requests.

### Step 4 – Submit Quotation

Provide

- Price
- Estimated duration
- Remarks

### Step 5 – Receive Booking

Booking notification received.

Accept or decline booking.

### Step 6 – Perform Work

Update

- Started
- In Progress
- Completed

### Step 7 – Receive Payment

Track

- Earnings
- Settlement
- Payment history

---

# 5. Workforce Provider Journey

## Objective

Supply workforce for larger work requirements.

### Journey

- Register organization
- Add workers
- Manage workforce
- Submit quotations
- Allocate workers
- Track work progress
- Receive payments

---

# 6. Service Business Journey

## Objective

Advertise professional services and receive customer bookings.

### Journey

- Register business
- Publish services
- Manage technicians
- Receive bookings
- Schedule work
- Complete service
- Collect payment
- Build ratings

---

# 7. Platform Administrator Journey

### Activities

- User verification
- Worker verification
- Category management
- Skill management
- Marketplace moderation
- Payment monitoring
- Fraud monitoring
- Analytics
- Reports

---

# 8. Booking Journey

```text
Work Posted
      │
      ▼
Quotation Submitted
      │
      ▼
Quotation Accepted
      │
      ▼
Booking Created
      │
      ▼
Worker Assigned
      │
      ▼
Work Completed
```

---

# 9. Payment Journey

```text
Booking Completed
        │
        ▼
Payment Initiated
        │
        ▼
Payment Successful
        │
        ▼
Settlement Processed
        │
        ▼
Receipt Generated
```

---

# 10. Communication Journey

Notifications are sent through:

- Push Notifications
- In-App Notifications
- SMS (Optional)
- WhatsApp (Optional)
- Email (Optional)

Events include:

- Registration
- Work Posted
- Quote Submitted
- Booking Confirmed
- Booking Cancelled
- Work Started
- Work Completed
- Payment Successful
- Rating Received

---

# 11. Exceptional Journeys

## Owner Cancels Booking

- Worker notified
- Refund policy applied
- Booking updated

## Worker Rejects Booking

- Owner notified
- Booking reopened

## Payment Failure

- Retry payment
- Notify users

## Worker No Show

- Owner reports issue
- Platform support notified

---

# 12. User Experience Principles

KrewOps follows these principles:

- Mobile-first design
- Minimal user effort
- Transparent pricing
- Real-time updates
- Location-aware discovery
- Secure payments
- Fast booking
- Simple navigation
- Multilingual support

---

# 13. Journey Success Metrics

- Time to post work
- Time to receive first quotation
- Booking conversion rate
- Average response time
- Work completion rate
- Payment success rate
- Customer satisfaction
- Worker earnings
- Repeat bookings

---

# 14. Summary

KrewOps provides two complementary marketplace journeys: work owners can publish work requests and receive quotations from workers, while workers and service businesses can advertise their services for direct booking. These user journeys establish a transparent, mobile-first, and trusted workforce marketplace that simplifies work discovery, booking, payments, and reputation management for all participants.
