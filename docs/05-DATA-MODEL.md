Document Version: 2.0

Product Version: 0.2.0

Status: ✅ Design Approved

Implementation Status: ⏳ Pending

Company: Lewis Systems

Product: ClientPilot

Author: La-eeq Lewis

Phase: Phase 2 – Solution Design

Last Updated: 02 August 2026

---

# 1. Purpose

This document defines the business data model for ClientPilot.

The data model describes the core business entities, their relationships, and the information required to support ClientPilot's client intake, qualification, scheduling, and communication processes.

The model is technology-independent and is not tied to any specific database platform.

---

# 2. Design Principles

The ClientPilot data model follows these principles:

- Business-first design
- Technology independence
- Modular architecture
- Data integrity
- Scalability
- Multi-tenant architecture
- Auditability

Every business record belongs to an Organization.

---

> **Implementation Note**
>
> This document defines the conceptual business data model.
> The physical implementation (Airtable tables, field types, relationships, and views) is derived from this model and may contain implementation-specific details while remaining consistent with the business architecture.

# 3. Entity Relationship Overview

```
                    Organization
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
      User           Company           Lead
                                          │
                    ┌─────────────────────┼────────────────────┐
                    │                     │                    │
                    ▼                     ▼                    ▼
                 Contact           Qualification          Meeting
                                                              │
                                           ┌──────────────────┴──────────────┐
                                           ▼                                 ▼
                                     AI Summary                         Activity
                                                                      │
                                                                      ▼
                                                                  Workflow
```

---

# 4. Core Entities

## 4.1 Organization

Represents a ClientPilot customer.

### Primary Key

Organization ID

### Attributes

- Organization Name
- Industry
- Subscription Plan
- Country
- Time Zone
- Status
- Created Date
- Last Updated

---

## 4.2 User

Represents an employee of an organization.

### Primary Key

User ID

### Foreign Key

Organization ID

### Attributes

- First Name
- Last Name
- Email
- Role
- Status
- Last Login

---

## 4.3 Company

Represents the business making the enquiry.

### Primary Key

Company ID

### Foreign Key

Organization ID

### Attributes

- Company Name
- Industry
- Annual Revenue
- Employee Count
- Website
- Country
- Province
- City

---

## 4.4 Contact

Represents the primary contact person.

### Primary Key

Contact ID

### Foreign Keys

- Organization ID
- Company ID

### Attributes

- First Name
- Last Name
- Email
- Phone Number
- Job Title
- Decision Maker
- Preferred Contact Method

---

## 4.5 Lead

Represents a client enquiry.

### Primary Key

Lead ID

### Foreign Keys

- Organization ID
- Company ID
- Contact ID

### Attributes

- Lead Status
- Lead Source
- Services Requested
- Submission Date
- Assigned Consultant
- Priority
- Qualification Status

---

## 4.6 Qualification

Stores the outcome of the qualification process.

### Primary Key

Qualification ID

### Foreign Key

Lead ID

### Attributes

- Revenue Score
- Industry Score
- Budget Score
- Urgency Score
- Decision Maker Score
- Total Score
- Qualified (Yes/No)
- AI Recommendation
- Qualification Reason

---

## 4.7 Meeting

Represents a scheduled consultation.

### Primary Key

Meeting ID

### Foreign Keys

- Organization ID
- Lead ID

### Attributes

- Meeting Date
- Meeting Time
- Calendly Event ID
- Assigned Consultant
- Meeting Status
- Meeting Notes

---

## 4.8 AI Summary

Stores AI-generated meeting preparation.

### Primary Key

Summary ID

### Foreign Key

Meeting ID

### Attributes

- Executive Summary
- Client Background
- Suggested Services
- Potential Risks
- Questions to Ask
- Opportunities
- Confidence Score

---

## 4.9 Activity

Stores an audit trail of important events.

### Primary Key

Activity ID

### Foreign Keys

- Organization ID
- Lead ID

### Attributes

- Activity Type
- Description
- Created By
- Created Date
- Status

---

## 4.10 Workflow

Stores workflow execution information.

### Primary Key

Workflow ID

### Foreign Keys

- Organization ID
- Lead ID

### Attributes

- Workflow Name
- Execution Status
- Start Time
- End Time
- Duration
- Error Message
- Retry Count

---

# 5. Entity Relationships

| Parent Entity | Relationship | Child Entity |
|----------------|--------------|--------------|
| Organization | One-to-Many | Users |
| Organization | One-to-Many | Companies |
| Organization | One-to-Many | Leads |
| Company | One-to-Many | Contacts |
| Company | One-to-Many | Leads |
| Contact | One-to-Many | Leads |
| Lead | One-to-One | Qualification |
| Lead | One-to-One | Meeting |
| Meeting | One-to-One | AI Summary |
| Lead | One-to-Many | Activities |
| Lead | One-to-Many | Workflow Executions |

---

# 6. Business Rules

- Every Organization must have a unique Organization ID.
- Every User belongs to one Organization.
- Every Lead belongs to one Organization.
- Every Lead must be linked to a Company.
- Every Lead must have a primary Contact.
- A Lead can only have one active Qualification.
- A Meeting may only be scheduled for qualified Leads.
- Every AI Summary must belong to a Meeting.
- Every Workflow Execution must reference the Lead it processed.
- Every Activity must include a timestamp.

---

# 7. Identifier Standards

| Entity | Prefix | Example |
|----------|--------|----------|
| Organization | ORG | ORG-000001 |
| User | USR | USR-000001 |
| Company | COM | COM-000001 |
| Contact | CON | CON-000001 |
| Lead | LED | LED-000001 |
| Qualification | QLF | QLF-000001 |
| Meeting | MTG | MTG-000001 |
| AI Summary | AIS | AIS-000001 |
| Activity | ACT | ACT-000001 |
| Workflow | WFL | WFL-000001 |

---

# 8. Data Security Principles

ClientPilot follows a multi-tenant architecture.

Rules:

- Organizations cannot access each other's data.
- Every record must include an Organization ID.
- Sensitive data must be protected.
- Access is controlled by user role.
- All workflow activity should be logged.

---

# 9. Future Entities

Future versions of ClientPilot may introduce:

- Proposal
- Invoice
- Client Portal Account
- Subscription
- Knowledge Base
- Document
- Task
- Email Campaign
- WhatsApp Conversation
- Voice Call

---

# 10. Current Status

Phase

Phase 2 – Solution Design

Status

🟢 Database Design Approved

Current Module

CRM Database

Next Task

Build the Companies table in Airtable.

---

# 11. Design Approval

The ClientPilot data model has been reviewed and approved as the foundation for the MVP implementation.

The implementation will begin using Airtable as the initial database platform while maintaining a technology-independent architecture that supports future migration to relational database systems such as PostgreSQL.

The approved CRM implementation consists of the following operational tables:

- Companies
- Contacts
- Leads
- Consultations
- AI Assessments
- Workflow Logs
- Settings

The conceptual business entities defined in this document remain the authoritative data model for ClientPilot. Future changes to the data model must be documented through Architecture Decision Records (ADRs) and version updates.