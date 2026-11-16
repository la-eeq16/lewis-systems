# ClientPilot Workflow Design

Document Version: 1.1

Product Version: 0.3.0

Status: Active

Company: Lewis Systems

Product: ClientPilot

Author: La-eeq Lewis

Last Updated: 16 November 2026

---

# 1. Purpose

This document defines the business workflows that power ClientPilot.

Each workflow describes the business process, the participating business engines, the data exchanged, and the expected outcome.

The workflows are implementation-independent and serve as the blueprint for automation.

---

# 2. Workflow Principles

All ClientPilot workflows must:

- Start with a business event.
- Follow a defined sequence of activities.
- Use modular business engines.
- Log important events.
- Handle failures gracefully.
- Support multi-tenancy.
- Be documented before implementation.

---

# 3. Workflow Catalogue

| Workflow ID | Name | Status |
|--------------|--------------------------------------|-----------|
| WF-001 | Client Intake & Qualification | Active (implemented on Make as WF-001A and WF-001B) |
| WF-002 | Consultation Booking | Planned |
| WF-003 | AI Meeting Preparation | Planned |
| WF-004 | Lead Follow-up | Planned |
| WF-005 | Lead Nurturing | Planned |
| WF-006 | Client Onboarding | Planned |
| WF-007 | Reporting & Analytics | Planned |
| WF-008 | Administration | Planned |

---

# 4. Workflow WF-001 – Client Intake & Qualification

## Purpose

To automate the journey from a new client enquiry to a qualified consultation.

---

## Business Trigger

A prospective client submits an enquiry.

---

## Workflow Overview

```

Prospective Client
        │
        ▼
Intake Engine
        │
        ▼
Lead Created
        │
        ▼
Qualification Engine
        │
        ▼
AI Decision Engine
        │
        ▼
Qualification Result
        │
        ▼
Decision
        │
 ┌──────┴──────────────┐
 │                     │
 ▼                     ▼

Qualified         Not Qualified

 │                     │

 ▼                     ▼

Scheduling      Communication

 │                     │

 ▼                     ▼

CRM Update       CRM Update

 │

 ▼

Slack Notification

 │

 ▼

AI Meeting Summary

 │

 ▼

Workflow Complete

```

---

# 5. Workflow Steps

## Step 1

### Business Engine

Intake Engine

### Action

Receive a client enquiry.

### Input

- Client submission

### Output

- New Lead

---

## Step 2

### Business Engine

CRM Engine

### Action

Create a Lead record.

### Output

- Lead ID
- Organization ID

---

## Step 3

### Business Engine

Qualification Engine

### Action

Validate the submission.

Checks include:

- Required fields
- Industry
- Revenue
- Budget
- Services Requested
- Decision Maker

---

## Step 4

### Business Engine

AI Decision Engine

### Action

Evaluate the lead.

Outputs:

- Qualification Score
- AI Recommendation
- Qualification Reason
- Confidence Score

---

## Step 5

### Business Engine

Qualification Engine

### Decision

What is the qualification result?

If **Qualified**:

Proceed to consultation booking.

If **Not Qualified**:

Proceed to follow-up communication.

If **Review Required** (score between the two thresholds):

No email or meeting is created. Staff review the lead manually.

---

## Step 6A – Qualified Lead

### Business Engine

Scheduling Engine

### Action

Provide a consultation booking link.

---

## Step 7A

### Business Engine

CRM Engine

### Update

Lead Status:

Qualified

Meeting Status:

Awaiting Booking

---

## Step 8A

### Business Engine

Communication Engine

### Actions

- Send confirmation email
- Notify staff
- Record activity

---

## Step 9A

### Business Engine

AI Decision Engine

### Action

Generate a meeting preparation summary.

Outputs:

- Executive Summary
- Client Background
- Recommended Services
- Risks
- Suggested Questions

---

## Step 10A

Workflow Complete

---

## Step 6B – Not Qualified Lead

### Business Engine

Communication Engine

### Action

Send a polite follow-up email.

---

## Step 7B

### Business Engine

CRM Engine

### Update

Lead Status:

Not Qualified

---

## Step 8B

Workflow Complete

---

# 5A. Implementation (MVP – Make)

WF-001 is implemented as two Make scenarios. This section is the mapping between the design above and the build. Full detail is in `docs/modules/module-03-n8n/WF-001-MAKE-IMPLEMENTATION.md`.

| Step | Implemented in |
|---|---|
| 1–2 Receive enquiry, create Lead | WF-001A – Client Intake (Google Sheets trigger) |
| 3 Validate | WF-001A – checks required fields, valid email format, industry, consent |
| 4 AI decision | WF-001B – **rule-based scoring in v1**; AI evaluation planned (Module 4) |
| 5 Decision | WF-001B – Qualified ≥ 64, Review Required 40–63, Not Qualified < 40 |
| 6A–7A Booking link, Lead and Meeting status | WF-001B – booking link from Settings; Meeting created as *Awaiting Booking* |
| 8A Confirmation email, activity | WF-001B – Gmail; Activity "Email Sent". **Slack staff notification planned (Module 5)** |
| 9A AI meeting summary | Planned (Module 4) |
| 6B–7B Follow-up email, Lead Status | WF-001B – Gmail; Lead Status *Not Qualified* |

Differences from the design:

- The validation list includes **Budget** and **Decision Maker**, but the MVP form does not collect them. Budget scores 0.
- Industry is validated but does not affect the score in v1.
- Email content and booking link come from the Settings table and must describe the **client firm**, not Lewis Systems.

---

# 6. Error Handling

The workflow must handle:

- Missing required information
- AI service unavailable
- CRM unavailable
- Scheduling unavailable
- Communication failure

For each error:

- Record the event.
- Retry where appropriate.
- Notify administrators if retries fail.
- Preserve workflow state.

---

# 7. Activity Logging

The following events should be logged:

- Lead Submitted
- Lead Created
- Qualification Completed
- AI Evaluation Completed
- CRM Updated
- Meeting Scheduled
- Email Sent
- Slack Notification Sent
- Workflow Completed

---

# 8. Workflow Metrics

Monitor:

- Workflow execution time
- Qualification accuracy
- Booking conversion rate
- AI response time
- Workflow failures
- Retry frequency

---

# 9. Future Workflows

Future versions of ClientPilot will include:

- Proposal Generation
- Client Onboarding
- Document Collection
- Invoice Automation
- Annual Client Reviews
- Tax Deadline Reminders
- WhatsApp Communication
- Voice AI Receptionist

---

# 10. Workflow Standards

Every ClientPilot workflow must:

- Have a unique Workflow ID.
- Be version controlled.
- Be documented before implementation.
- Be independently testable.
- Support multi-tenancy.
- Log important business events.
- Follow Lewis Systems Development Standards.

---

# 11. Current Status

Phase

Phase 3 – MVP Implementation

Status

🟢 Active Development – WF-001 built and tested on Make