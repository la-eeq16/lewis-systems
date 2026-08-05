# Module 3 – Workflow Architecture

**Module:** 03 – n8n Workflow Automation

**Document Version:** 1.0

**Product Version:** 0.3.0

**Status:** 🚧 In Progress

**Company:** Lewis Systems

**Product:** ClientPilot

**Author:** La-eeq Lewis

**Phase:** Phase 3 – MVP Implementation

**Last Updated:** 05 August 2026

---

# 1. Purpose

This document defines the overall workflow architecture for the ClientPilot automation layer.

It describes how data moves through the system, how workflows interact, and how responsibilities are separated across multiple n8n workflows.

The architecture follows a modular design that promotes maintainability, scalability, and fault isolation.

---

# 2. Architecture Overview

The automation layer is built around five independent workflows.

```text
Workflow 1
Client Intake
        │
        ▼
Workflow 2
CRM Processing
        │
        ▼
Workflow 3
AI Qualification
        │
        ▼
Workflow 4
Notifications
        │
        ▼
Workflow 5
Scheduling
```

Each workflow performs one primary responsibility before handing control to the next workflow.

---

# 3. Complete System Flow

```text
Client
   │
   ▼
Google Forms
   │
   ▼
Google Sheets
   │
   ▼
Workflow 1
(Client Intake)
   │
   ▼
Workflow 2
(CRM Processing)
   │
   ▼
Workflow 3
(AI Qualification)
   │
   ▼
Workflow 4
(Notifications)
   │
   ▼
Workflow 5
(Scheduling)
```

---

# 4. Workflow 1 – Client Intake

## Responsibility

Receive new client enquiries.

## Trigger

Google Sheets Trigger

## Functions

- Detect new form submission
- Validate required fields
- Standardise input data
- Remove unnecessary whitespace
- Verify email format
- Verify phone number
- Forward validated data

## Output

Validated enquiry data

---

# 5. Workflow 2 – CRM Processing

## Responsibility

Synchronise data with Airtable.

## Functions

Search Company

↓

Company Exists?

Yes

↓

Retrieve Company

No

↓

Create Company

↓

Search Contact

↓

Contact Exists?

Yes

↓

Retrieve Contact

No

↓

Create Contact

↓

Create Lead

↓

Pass Lead Information

---

# 6. Workflow 3 – AI Qualification

## Responsibility

Prepare leads for qualification.

## Functions

Receive Lead

↓

Build Prompt

↓

Send to OpenAI

↓

Receive AI Response

↓

Determine Lead Score

↓

Determine Priority

↓

Create Qualification Record

↓

Update Lead

↓

Pass Results

---

# 7. Workflow 4 – Notifications

## Responsibility

Notify internal staff.

## Functions

Receive Qualification

↓

Format Slack Message

↓

Send Notification

↓

Record Activity

↓

Continue

---

# 8. Workflow 5 – Scheduling

## Responsibility

Prepare consultation booking.

## Functions

Qualified Lead?

↓

Yes

↓

Create Calendly Invitation

↓

Store Booking Information

↓

Create Meeting Record

↓

Workflow Complete

---

# 9. Decision Points

The automation contains several important decision nodes.

## Company Exists?

If Yes

Use existing Company.

If No

Create Company.

---

## Contact Exists?

If Yes

Use existing Contact.

If No

Create Contact.

---

## Lead Qualified?

If Yes

Proceed to Notifications and Scheduling.

If No

Store Qualification Result only.

---

# 10. Error Handling

Every workflow contains independent error handling.

Errors should:

- Stop only the current workflow.
- Record the failure.
- Notify administrators where appropriate.
- Preserve received data.

This prevents one integration failure from affecting the rest of the automation platform.

---

# 11. Data Ownership

| System | Responsibility |
|---------|----------------|
| Google Forms | Client input |
| Google Sheets | Raw submissions |
| n8n | Workflow orchestration |
| Airtable | Master CRM |
| OpenAI | Qualification |
| Slack | Notifications |
| Calendly | Scheduling |

Each system owns one specific responsibility.

---

# 12. Workflow Principles

The ClientPilot automation layer follows these principles:

- One workflow, one responsibility
- Modular design
- Independent testing
- Reusable logic
- Clear data ownership
- Scalable architecture

---

# 13. Future Expansion

Additional workflows can be added without changing existing workflows.

Examples include:

- Email Automation
- Proposal Generation
- Document Collection
- Client Portal
- Payment Processing
- Reporting
- Executive Dashboard

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| 1.0 | 05 August 2026 | Initial workflow architecture. |

---

© Lewis Systems. All rights reserved.