# ClientPilot Data Model

Document Version: 2.1

Product Version: 0.2.0

Status: ✅ CRM Structure Complete

Implementation Status: ✅ Airtable MVP Implemented

Company: Lewis Systems

Product: ClientPilot

Author: La-eeq Lewis

Phase: Phase 2 – Solution Design

Last Updated: 03 August 2026

---

# 1. Purpose

This document defines the business data model for ClientPilot.

The data model describes the core business entities, their relationships, and the information required to support ClientPilot's client intake, qualification, scheduling, meeting management, workflow automation, and communication processes.

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
- Automation-first design

Every business record belongs to an Organization.

---

> **Implementation Note**
>
> This document defines the conceptual business data model.
>
> The current MVP implementation uses Airtable as the CRM platform.
>
> Where supported by Airtable, relationships are implemented using Linked Record fields rather than manually maintained foreign keys.
>
> Logical business identifiers (Company ID, Contact ID, Lead ID, Qualification ID, Meeting ID, Activity ID, Workflow Log ID) remain part of the business model for integrations, reporting, auditing, and future migration to PostgreSQL or another relational database.

---

# 3. Entity Relationship Overview

```text
                    Organization
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
      User           Company           Lead
                         │                │
                         │        ┌───────┼──────────┐
                         │        │       │          │
                         ▼        ▼       ▼          ▼
                    Contact Qualification Meeting Activity
                                         │
                                         ▼
                                  Workflow Log

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

### Airtable Implementation

The Companies table is the primary business entity within the CRM.

Each Company may be linked to multiple Contacts, Leads, Meetings, Activities, and future business records using Airtable Linked Records.

---

## 4.4 Contact

Represents the primary contact person.

### Primary Key

Contact ID

### Relationships

- Organization
- Company

### Attributes

- First Name
- Last Name
- Email
- Phone Number
- Job Title
- Decision Maker
- Preferred Contact Method

### Airtable Implementation

The Company relationship is implemented using an Airtable Linked Record field.

The logical Company ID remains part of the conceptual business model for reporting, integrations, and future database portability.

---

## 4.5 Lead

Represents a client enquiry.

### Primary Key

Lead ID

### Relationships

- Organization
- Company
- Contact

### Attributes

- Lead Status
- Lead Source
- Services Requested
- Submission Date
- Assigned Consultant
- Priority
- Qualification Status

### Airtable Implementation

Lead records are linked to the Company and Contact tables using Airtable Linked Record fields.

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
|---------------|--------------|--------------|
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
- Every Lead must be linked to one Company.
- Every Lead must have one primary Contact.
- Every Company may have multiple Contacts.
- Every Contact belongs to one Company.
- A Lead can only have one active Qualification.
- A Meeting may only be scheduled for qualified Leads.
- Every AI Summary must belong to a Meeting.
- Every Workflow Execution must reference the Lead it processed.
- Every Activity must include a timestamp.
- Where supported by the implementation platform, relationships should be maintained using native relational features (such as Airtable Linked Records) rather than manually maintained foreign-key values.

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

**Phase**

Phase 2 – Solution Design

**Status**

🟢 CRM Database Structure Complete

**Implementation Status**

✅ All MVP CRM tables implemented in Airtable

**Completed**

- CRM business data model approved
- Companies table implemented
- Contacts table implemented
- Leads table implemented
- Qualifications table implemented
- Meetings table implemented
- Activities table implemented
- Workflow Logs table implemented
- Settings table implemented
- Linked record relationships configured
- Standard views created for all tables
- Initial QA validation completed across all tables

**Current Module**

CRM Database

**Current Task**

Data validation and workflow integration.

**Next Task**

Design and implement the Google Form client intake process.

---

# 11. Design Approval

The ClientPilot data model has been reviewed and approved as the foundation for the MVP implementation.

The MVP implementation is being developed using Airtable as the initial CRM platform while maintaining a technology-independent architecture that supports future migration to relational database systems such as PostgreSQL.

The current CRM implementation consists of the following operational tables:

- Companies
- Contacts
- Leads
- Qualifications
- Meetings
- Activities
- Workflow Logs
- Settings

All MVP tables have been implemented, linked using Airtable Linked Record fields, and validated through quality assurance checks.

The conceptual business entities defined in this document remain the authoritative data model for ClientPilot.

Future changes to the data model must be be documented through Architecture Decision Records (ADRs) and version updates.