# ClientPilot Google Form Field Mapping

**Document Version:** 1.0

**Product Version:** 0.3.0

**Status:** 🚧 Draft

**Company:** Lewis Systems

**Product:** ClientPilot

**Author:** La-eeq Lewis

**Module:** Module 2 – Google Forms Client Intake

**Last Updated:** 04 August 2026

---

# 1. Purpose

This document defines how every Google Form field maps into the ClientPilot CRM.

It serves as the single source of truth for all future integrations, ensuring consistent data flow between:

- Google Forms
- Google Sheets
- n8n
- Airtable
- OpenAI
- Slack
- Calendly

---

# 2. Data Flow

```text
Google Form
      │
      ▼
Google Sheets
      │
      ▼
n8n
      │
      ▼
Airtable CRM
```

---

# 3. Field Mapping

| # | Google Form Question | Form Type | Required | Airtable Table | Airtable Field | Notes |
|---|----------------------|-----------|----------|----------------|----------------|------|
| 1 | Company Name | Short Answer | ✅ | Companies | Company Name | Creates company if it doesn't exist |
| 2 | First Name | Short Answer | ✅ | Contacts | First Name | Primary contact |
| 3 | Last Name | Short Answer | ✅ | Contacts | Last Name | Primary contact |
| 4 | Email Address | Short Answer (Email) | ✅ | Contacts | Email | Used for communication |
| 5 | Phone Number | Short Answer | ✅ | Contacts | Phone Number | International format preferred |
| 6 | Job Title | Short Answer | ✅ | Contacts | Job Title | Decision-maker role |
| 7 | Industry | Dropdown | ✅ | Companies | Industry | Business sector |
| 8 | Number of Employees | Dropdown | ✅ | Companies | Employee Count | Company size |
| 9 | Annual Revenue | Dropdown | ✅ | Companies | Annual Revenue | Used for lead qualification |
|10 | Services Required | Checkbox | ✅ | Leads | Services Requested | Multiple selections allowed |
|11 | Estimated Budget | Dropdown | ⬜ | Leads | Budget | Optional |
|12 | Project Urgency | Multiple Choice | ✅ | Leads | Priority | AI scoring input |
|13 | How did you hear about us? | Dropdown | ⬜ | Leads | Lead Source | Marketing attribution |
|14 | Additional Information | Paragraph | ⬜ | Leads | Notes | Free-text comments |

---

# 4. Validation Rules

- Company Name is required.
- First Name is required.
- Last Name is required.
- Email must be valid.
- Phone Number is required.
- Annual Revenue must be selected.
- Services Required must contain at least one selection.
- Project Urgency is required.

---

# 5. Notes

This mapping document will be used during the implementation of:

- Google Forms
- Google Sheets
- n8n
- Airtable
- OpenAI
- Slack
- Calendly

Any changes to the Google Form must be reflected here before implementation.