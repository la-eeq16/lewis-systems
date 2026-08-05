# Module 3 – Workflow Specifications

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

This document defines the functional specification for each workflow within the ClientPilot automation platform.

Each workflow performs a single business responsibility and communicates with other workflows through clearly defined inputs and outputs.

---

# Workflow 01 – Client Intake

## Purpose

Receive and validate new client enquiries submitted through Google Forms.

## Trigger

Google Sheets Trigger

## Inputs

- Company Name
- Contact Name
- Email Address
- Mobile Number
- Job Title
- Annual Revenue
- Service Required
- Additional Notes

## Processing

- Validate required fields
- Standardise formatting
- Remove unnecessary whitespace
- Verify email format
- Verify phone number format
- Create submission timestamp

## Outputs

Validated enquiry object

## Business Rules

- Company Name is required.
- Contact Name is required.
- Email Address is required.
- Mobile Number is required.
- Invalid submissions are rejected.

## Dependencies

- Google Forms
- Google Sheets

---

# Workflow 02 – Company Service

## Purpose

Locate an existing company or create a new company record.

## Trigger

Called by Workflow 01.

## Inputs

- Company Name
- Website (optional)
- Industry
- Annual Revenue

## Processing

- Search Airtable Companies table.
- Compare company names.
- If found, return Company ID.
- If not found, create Company record.

## Outputs

- Company ID
- Company Record

## Business Rules

- Duplicate companies are not created.
- Existing companies are reused.

## Dependencies

- Airtable CRM

---

# Workflow 03 – Contact Service

## Purpose

Locate or create the primary contact for the enquiry.

## Trigger

Called by Workflow 02.

## Inputs

- Contact Name
- Email Address
- Mobile Number
- Job Title
- Company ID

## Processing

- Search Contacts table.
- Match by Email Address.
- If found, return Contact ID.
- If not found, create Contact record.

## Outputs

- Contact ID
- Contact Record

## Business Rules

- Email Address must be unique.
- Duplicate contacts are not created.

## Dependencies

- Airtable CRM

---

# Workflow 04 – Lead Service

## Purpose

Create a new lead linked to the correct company and contact.

## Trigger

Called by Workflow 03.

## Inputs

- Company ID
- Contact ID
- Service Required
- Annual Revenue
- Additional Notes

## Processing

- Generate Lead ID
- Create Lead
- Link Company
- Link Contact
- Set Lead Status
- Record creation timestamp

## Outputs

- Lead ID
- Lead Record

## Business Rules

- Every lead must be linked to one company.
- Every lead must be linked to one contact.

## Dependencies

- Airtable CRM

---

# Workflow 05 – AI Qualification

## Purpose

Evaluate the quality of the lead using OpenAI.

## Trigger

Called by Workflow 04.

## Inputs

- Lead Information
- Company Information
- Contact Information

## Processing

- Build AI prompt
- Submit prompt to OpenAI
- Receive response
- Determine Lead Score
- Determine Priority
- Generate Summary
- Create Qualification record

## Outputs

- Qualification Record
- Lead Score
- Priority
- AI Summary

## Business Rules

- AI results must be stored.
- Original lead data must remain unchanged.

## Dependencies

- OpenAI
- Airtable CRM

---

# Workflow 06 – Notifications

## Purpose

Notify internal staff of newly qualified leads.

## Trigger

Called by Workflow 05.

## Inputs

- Lead Information
- Qualification
- Priority

## Processing

- Format Slack message
- Send notification
- Record activity log

## Outputs

- Slack Notification
- Activity Record

## Business Rules

- High-priority leads should be clearly identified.
- Notification failures must be logged.

## Dependencies

- Slack
- Airtable CRM

---

# Workflow 07 – Scheduling

## Purpose

Prepare consultation scheduling for qualified leads.

## Trigger

Called by Workflow 06.

## Inputs

- Lead Information
- Contact Information
- Qualification

## Processing

- Generate Calendly invitation
- Create Meeting record
- Update Lead status
- Record scheduling activity

## Outputs

- Meeting Record
- Calendly Link

## Business Rules

- Only qualified leads proceed to scheduling.
- Meeting records must reference the Lead.

## Dependencies

- Calendly
- Airtable CRM

---

# Workflow Execution Order

```text
Workflow 01 → Client Intake

        ↓

Workflow 02 → Company Service

        ↓

Workflow 03 → Contact Service

        ↓

Workflow 04 → Lead Service

        ↓

Workflow 05 → AI Qualification

        ↓

Workflow 06 → Notifications

        ↓

Workflow 07 → Scheduling
```

---

# Workflow Design Principles

Every workflow must:

- Perform one business responsibility.
- Be independently testable.
- Handle errors gracefully.
- Produce consistent outputs.
- Be reusable by future ClientPilot modules.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| 1.0 | 05 August 2026 | Initial workflow specifications. |

---

© Lewis Systems. All rights reserved.