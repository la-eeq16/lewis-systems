# Module 1 – CRM Database Table Specifications

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

This document defines the operational tables used by the ClientPilot CRM.

It serves as the implementation reference for the Airtable database by documenting the purpose, relationships, and primary data stored within each table.

This specification complements the Data Model and Entity Relationships documentation.

---

# 2. CRM Overview

The ClientPilot CRM consists of eight operational tables.

| Table | Purpose |
|---------|---------|
| Companies | Stores organisations that interact with ClientPilot. |
| Contacts | Stores individual people linked to companies. |
| Leads | Stores client enquiries and sales opportunities. |
| Qualifications | Stores AI and business qualification outcomes. |
| Meetings | Stores consultation bookings. |
| Activities | Stores business and user activity history. |
| Workflow Logs | Stores automation execution history. |
| Settings | Stores configurable system settings. |

---

# 3. Companies

## Purpose

Stores every company that submits an enquiry.

## Primary Information

- Company ID
- Company Name
- Industry
- Website
- Annual Revenue
- Number of Employees
- Address
- Notes

## Relationships

- One Company → Many Contacts
- One Company → Many Leads

---

# 4. Contacts

## Purpose

Stores individuals associated with companies.

## Primary Information

- Contact ID
- Full Name
- Email Address
- Mobile Number
- Job Title
- Research Full Name
- Employer
- Notes

## Relationships

- Many Contacts → One Company
- One Contact → Many Leads

---

# 5. Leads

## Purpose

Represents every client enquiry entering ClientPilot.

## Primary Information

- Lead ID
- Lead Status
- Service Required
- Estimated Revenue
- Priority
- Source
- Date Created

## Relationships

- Many Leads → One Company
- Many Leads → One Contact
- One Lead → One Qualification
- One Lead → One Meeting
- One Lead → Many Activities
- One Lead → Many Workflow Logs

---

# 6. Qualifications

## Purpose

Stores qualification results produced through business rules and AI analysis.

## Primary Information

- Qualification ID
- Qualification Status
- AI Score
- Lead Score
- Qualification Notes
- Decision
- Review Date

## Relationships

- One Qualification → One Lead

---

# 7. Meetings

## Purpose

Stores consultation bookings for qualified leads.

## Primary Information

- Meeting ID
- Meeting Status
- Meeting Date
- Meeting Time
- Meeting Type
- Calendly Reference
- Assigned Consultant

## Relationships

- One Meeting → One Lead

---

# 8. Activities

## Purpose

Provides a historical audit trail of important actions.

## Primary Information

- Activity ID
- Activity Type
- Activity Date
- Activity Description
- User
- Timestamp

## Relationships

- Many Activities → One Lead

---

# 9. Workflow Logs

## Purpose

Records workflow execution history.

## Primary Information

- Workflow ID
- Workflow Name
- Status
- Execution Time
- Duration
- Error Message
- Trigger Source

## Relationships

- Many Workflow Logs → One Lead

---

# 10. Settings

## Purpose

Stores configurable application settings.

## Primary Information

- Setting Name
- Setting Value
- Category
- Description

## Relationships

The Settings table is independent and is referenced by system processes rather than linked directly to operational records.

---

# 11. Data Standards

Every operational table follows the same standards.

## Naming

- Human-readable field names
- Consistent terminology
- Business-friendly labels

## Identifiers

Every operational record includes a unique business identifier.

Examples:

- Company ID
- Contact ID
- Lead ID
- Qualification ID
- Meeting ID
- Activity ID
- Workflow ID

## Relationships

Relationships are implemented using Airtable Linked Records.

Business identifiers remain available for reporting and future migrations.

---

# 12. Future Expansion

The CRM structure has been designed to support future functionality including:

- Client Portal
- Proposal Generator
- Email Automation
- AI Meeting Preparation
- Executive Dashboards
- Multi-Tenant SaaS
- Additional professional service industries

No structural redesign is expected for these future enhancements.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| 1.0 | 05 August 2026 | Initial Table Specifications documentation. |

---

© Lewis Systems. All rights reserved.