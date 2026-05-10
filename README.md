# Online Fitness Coaching Platform – ER Diagram Design

## Project Overview
This project represents the database design for an **Online Fitness Coaching Platform** where fitness influencers/trainers can manage clients, coaching plans, subscriptions, consultations, progress tracking, and payments.

The system is designed for a modern online coaching ecosystem where trainers interact with clients through structured coaching programs instead of traditional gym management.

The ER diagram models how trainers handle multiple clients, how clients subscribe to plans, attend sessions, submit weekly check-ins, and track fitness progress over time.

---

# Problem Statement
A fitness influencer initially manages clients manually through Instagram DMs and video calls. As the business scales, they require a platform to:

- onboard clients
- manage trainers/coaches
- sell coaching programs
- schedule consultations and sessions
- manage subscriptions
- track progress and measurements
- maintain trainer notes and feedback
- handle payments

This ER diagram provides a scalable relational database structure for the platform.

---

# Features Covered in the ER Design

## User Management
- Common `users` table for authentication and role management
- Separate profiles for:
  - `trainer_profile`
  - `client_profile`

## Trainer & Client Relationship
- One trainer can coach multiple clients
- One client can subscribe to multiple plans over time

## Coaching Plans
- Trainers can create multiple coaching programs
- Plans include:
  - title
  - description
  - duration
  - pricing
  - plan type

## Subscriptions
Tracks:
- which client purchased which plan
- start and end dates
- subscription status

## Sessions & Consultations
Schedule online sessions between trainers and clients.

Supports:
- consultations
- live coaching sessions
- follow-ups

## Progress Tracking
- Weekly client check-ins
- Weight and body fat tracking
- Measurement tracking for different body parts
- Trainer notes and feedback

## Payments
Stores:
- payment amount
- method
- transaction reference
- payment status

---

# Database Entities

## 1. users
Stores authentication and role information.

### Attributes
- `id` (PK)
- `name`
- `email`
- `passwordHash`
- `role`
- `createdAt`

---

## 2. trainer_profile
Stores trainer-specific details.

### Attributes
- `id` (PK)
- `userId` (FK)
- `bio`
- `specialization`

---

## 3. client_profile
Stores client-specific fitness information.

### Attributes
- `id` (PK)
- `userId` (FK)
- `height`
- `initialWeight`
- `goal`

---

## 4. coaching_plan
Represents fitness/coaching programs created by trainers.

### Attributes
- `id` (PK)
- `trainerId` (FK)
- `title`
- `description`
- `price`
- `durationDays`
- `planType`

---

## 5. subscription
Tracks plan purchases by clients.

### Attributes
- `id` (PK)
- `clientId` (FK)
- `planId` (FK)
- `startDate`
- `endDate`
- `status`

---

## 6. plan_content
Stores plan resources like workout or diet content.

### Attributes
- `id` (PK)
- `planId` (FK)
- `type`
- `title`
- `contentUrl`
- `weekNumber`

---

## 7. session
Stores consultations and coaching sessions.

### Attributes
- `id` (PK)
- `trainerId` (FK)
- `clientId` (FK)
- `subscriptionId` (FK)
- `scheduledAt`
- `duration`
- `type`
- `status`
- `notes`

---

## 8. check_in
Stores weekly client progress submissions.

### Attributes
- `id` (PK)
- `clientId` (FK)
- `subscriptionId` (FK)
- `weekNumber`
- `checkinDate`
- `weight`
- `bodyFat`
- `notes`

---

## 9. measurement
Stores body measurements linked to check-ins.

### Attributes
- `id` (PK)
- `checkInId` (FK)
- `bodyPart`
- `value`

---

## 10. trainer_notes
Stores trainer feedback and observations.

### Attributes
- `id` (PK)
- `trainerId` (FK)
- `clientId` (FK)
- `subscriptionId` (FK)
- `note`
- `createdAt`

---

## 11. payment
Stores payment and transaction details.

### Attributes
- `id` (PK)
- `subscriptionId` (FK)
- `amount`
- `paymentDate`
- `method`
- `status`
- `transactionRef`

---

# Relationships & Cardinality

| Relationship | Cardinality |
|---|---|
| One trainer → many coaching plans | 1 : M |
| One trainer → many clients | 1 : M |
| One client → many subscriptions | 1 : M |
| One plan → many subscriptions | 1 : M |
| One subscription → many sessions | 1 : M |
| One subscription → many check-ins | 1 : M |
| One check-in → many measurements | 1 : M |
| One subscription → many payments | 1 : M |

---

# Design Decisions

## Why separate trainer/client profiles?
The `users` table handles authentication, while profile tables store role-specific information. This keeps the database normalized and scalable.

## Why keep check-ins separate?
Progress tracking changes frequently and contains time-series data. Separating it avoids bloating the user table.

## Why separate measurements?
Clients may track multiple body parts for every check-in, making a separate table more flexible.

## Why use subscriptions?
A client may purchase multiple plans over time, so subscriptions act as the bridge between clients and coaching plans.

---

# Tools Used
- Eraser / Draw.io style ER modeling
- Relational Database Design Concepts
- Primary Keys & Foreign Keys
- Cardinality Mapping

---

# Learning Outcomes
Through this project, the following database design concepts were practiced:

- ER Diagram Modeling
- Relational Database Structuring
- Entity Relationships
- Database Normalization
- Primary & Foreign Keys
- One-to-Many Relationships
- Scalable System Design

---

# Submission Format
This project can be submitted as:
- ER Diagram Image
- PDF Export
- Draw.io / Eraser Board Link
- GitHub Repository

---

# Conclusion
This ER diagram provides a scalable and practical database design for an online fitness coaching ecosystem. It supports trainers managing multiple clients, structured coaching programs, subscriptions, consultations, progress tracking, and payment management while maintaining proper normalization and separation of concerns.