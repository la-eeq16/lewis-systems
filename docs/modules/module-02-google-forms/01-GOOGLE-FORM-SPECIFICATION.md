# Google Form Specification

Document Version: 1.0

Module: Module 2 – Google Forms Client Intake

Product Version: 0.3.0

Status: 🚧 In Development

Company: Lewis Systems

Product: ClientPilot

Author: La-eeq Lewis

Phase: Phase 3 – MVP Implementation

Last Updated: 04 August 2026

---

# 1. Purpose

This document defines the design, structure, validation rules, and field mappings for the ClientPilot Google Form.

The form is the primary entry point into the ClientPilot platform and captures all information required to create or update CRM records within Airtable.

The design prioritizes simplicity, usability, and high-quality data collection for accounting firms.

---

# 2. Objectives

The Google Form must:

- Capture prospective client enquiries.
- Collect accurate business information.
- Create high-quality CRM records.
- Support automated lead qualification.
- Trigger downstream workflows through n8n.
- Minimize manual data entry.
- Provide a professional client experience.

---

# 3. User Journey

```text
Prospective Client
        │
        ▼
Google Form
        │
        ▼
Google Sheets
        │
        ▼
n8n Automation
        │
        ▼
Airtable CRM
        │
        ├── Companies
        ├── Contacts
        ├── Leads
        ├── Qualifications
        ├── Activities
        └── Workflow Logs
```

---

# 4. Form Structure

The form consists of six sections.

| Section | Purpose |
|----------|----------|
| Welcome | Introduce the form |
| Contact Information | Capture contact details |
| Company Information | Capture company details |
| Accounting Requirements | Capture lead information |
| Consultation Preferences | Capture preferred contact details |
| Consent | Capture required agreements |

---

# 5. Section Specifications

## Section 1 – Welcome

Purpose

Introduce the company and explain the process.

Display:

- Estimated completion time
- Privacy statement
- What happens after submission

---

## Section 2 – Contact Information

Fields

- First Name *
- Last Name *
- Business Email *
- Phone Number *
- Job Title
- Preferred Contact Method *

---

## Section 3 – Company Information

Fields

- Company Name *
- Company Website
- Industry *
- Number of Employees
- Annual Revenue Range
- Country *
- Province
- City

---

## Section 4 – Accounting Requirements

Fields

- Services Required *
- Describe Your Business Challenge *
- Desired Outcome
- Estimated Budget
- Preferred Start Date

---

## Section 5 – Consultation Preferences

Fields

- Preferred Consultation Method *
- Best Time To Contact
- Additional Information

---

## Section 6 – Consent

Fields

- I agree to the Privacy Policy *
- I agree to be contacted regarding my enquiry *

Optional

- Marketing Communications

---

# 6. Validation Rules

The form must enforce:

- Required fields for mandatory information.
- Valid email addresses.
- Valid phone number format.
- Dropdown selections where possible.
- Checkbox validation for consent.
- Character limits where appropriate.

---

# 7. Data Flow

```text
Google Form
        │
        ▼
Google Sheets
        │
        ▼
n8n Workflow
        │
        ▼
Airtable CRM
        │
        ├── Companies
        ├── Contacts
        ├── Leads
        ├── Qualifications
        ├── Activities
        └── Workflow Logs
```

---

# 8. Airtable Mapping

The Google Form will populate the following CRM tables:

| Google Form Section | Airtable Table |
|---------------------|----------------|
| Contact Information | Contacts |
| Company Information | Companies |
| Accounting Requirements | Leads |
| Consultation Preferences | Leads |
| Consent | Activities / Workflow Logs |

Record identifiers such as Company ID, Contact ID, and Lead ID are generated automatically within the CRM.

---

# 9. Business Rules

- Every submission creates a Lead.
- Every Lead must be linked to a Company.
- Every Lead must be linked to a Contact.
- Duplicate Companies should not be created.
- Duplicate Contacts should not be created.
- Submission source must be recorded as Google Forms.
- Qualification records are created by the automation workflow.
- Workflow Logs are created automatically by n8n.

---

# 10. Success Criteria

The module is considered complete when:

- Google Form is fully configured.
- Validation rules are working.
- Google Sheets receives responses.
- n8n receives the data.
- Airtable records are created successfully.
- Documentation is complete.
- QA checklist passes.

---

# 11. Future Enhancements

Future versions may include:

- File uploads
- Conditional logic
- Dynamic service lists
- Multi-language support
- Industry-specific form templates
- Client portal integration

---

# 12. Approval

This specification serves as the implementation blueprint for the ClientPilot Google Form.

Any future changes should be documented through version updates and Architecture Decision Records (ADRs) where applicable.