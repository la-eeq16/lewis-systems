# Module 1 – CRM Database Entity Relationships

**Module:** 01 – CRM Database

**Document Version:** 1.0

**Product Version:** 0.3.0

**Status:** ✅ Complete

**Company:** Lewis Systems

**Product:** ClientPilot

**Author:** La-eeq Lewis

**Phase:** Phase 2 – Solution Design

**Last Updated:** 05 August 2026

---

# 1. Purpose

This document describes how the ClientPilot CRM entities are related within the Airtable implementation.

It explains the relationships between operational tables and how data flows through the CRM from an initial client enquiry to completed workflow execution.

This document complements the ClientPilot Data Model by documenting the practical implementation of those relationships.

---

# 2. Relationship Overview

The CRM uses Airtable Linked Records to establish relationships between business entities.

This approach:

- Reduces duplicate data
- Improves reporting
- Supports automation
- Maintains referential integrity
- Simplifies future integrations

---

# 3. Entity Relationship Flow

```text
Company
   │
   ├─────────────┐
   ▼             ▼
Contacts      Leads
                  │
                  ▼
          Qualifications
                  │
                  ▼
              Meetings
                  │
                  ▼
             Activities
                  │
                  ▼
           Workflow Logs
```

---

# 4. Relationship Definitions

## Company → Contacts

Relationship Type

One-to-Many

Description

A company may have multiple contacts.

Each contact belongs to a single company.

Examples

ABC Accounting

- John Smith
- Sarah Jones
- David Brown

---

## Company → Leads

Relationship Type

One-to-Many

Description

A company may submit multiple enquiries over time.

Each enquiry becomes a Lead.

---

## Contact → Leads

Relationship Type

One-to-Many

Description

A contact can submit multiple enquiries.

Each Lead belongs to one primary contact.

---

## Lead → Qualification

Relationship Type

One-to-One

Description

Every Lead receives one active qualification record.

The qualification stores:

- AI score
- Priority
- Lead status
- Qualification notes

---

## Lead → Meeting

Relationship Type

One-to-One

Description

Qualified Leads may proceed to a consultation meeting.

Meeting records include:

- Date
- Time
- Status
- Calendly reference

---

## Lead → Activities

Relationship Type

One-to-Many

Description

Every important action performed on a Lead is recorded as an Activity.

Examples include:

- Form received
- AI qualification completed
- Meeting booked
- Status updated
- Follow-up completed

---

## Lead → Workflow Logs

Relationship Type

One-to-Many

Description

Automation execution history is stored separately from Activities.

Workflow Logs record:

- Workflow name
- Execution time
- Success
- Failure
- Error details
- Processing duration

---

# 5. Relationship Principles

The CRM follows these relationship principles:

- Every Contact belongs to one Company.
- Every Lead belongs to one Company.
- Every Lead belongs to one Contact.
- Every Qualification belongs to one Lead.
- Every Meeting belongs to one Lead.
- Every Activity belongs to one Lead.
- Every Workflow Log belongs to one Lead.

---

# 6. Relationship Benefits

The implemented relationship model provides:

- Reduced duplication
- Easier reporting
- Better automation
- Cleaner CRM structure
- AI-ready data
- Improved scalability

---

# 7. Workflow Example

A typical ClientPilot workflow follows these relationships:

1. Client submits a Google Form.
2. Company record is located or created.
3. Contact record is located or created.
4. Lead record is created.
5. AI Qualification record is generated.
6. Meeting is scheduled.
7. Activities are logged.
8. Workflow execution is recorded.

This process ensures every enquiry is fully traceable throughout its lifecycle.

---

# 8. Future Expansion

The relationship model has been designed to support future modules, including:

- Client Portal
- Proposal Generator
- Email Campaigns
- AI Meeting Preparation
- Multi-Tenant SaaS Architecture
- Industry-specific workflows

These enhancements can be introduced without restructuring the existing CRM relationships.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| 1.0 | 05 August 2026 | Initial Entity Relationships documentation. |

---

© Lewis Systems. All rights reserved.