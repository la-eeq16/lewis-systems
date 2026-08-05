# Module 3 – Technical Field Mapping

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

This document provides the technical implementation mapping used by the ClientPilot automation platform.

Unlike the Business Field Mapping document, this specification defines the exact field names, variables, APIs, and data objects used throughout the automation workflows.

It serves as the primary implementation reference for n8n workflows and future software development.

---

# 2. Data Flow

```text
Google Forms
      │
      ▼
Google Sheets
      │
      ▼
n8n Variables
      │
      ▼
Airtable
      │
      ▼
OpenAI
      │
      ▼
Slack
      │
      ▼
Calendly
```

---

# 3. Google Forms → Google Sheets

| Google Form Question | Google Sheets Column |
|----------------------|----------------------|
| Timestamp | Timestamp |
| Company Name | Company Name |
| Contact Name | Contact Name |
| Email Address | Email Address |
| Mobile Number | Mobile Number |
| Job Title | Job Title |
| Annual Revenue | Annual Revenue |
| Service Required | Service Required |
| Additional Notes | Additional Notes |

---

# 4. Google Sheets → n8n

| Google Sheets | n8n Variable |
|---------------|--------------|
| Timestamp | submissionTimestamp |
| Company Name | companyName |
| Contact Name | contactName |
| Email Address | email |
| Mobile Number | mobileNumber |
| Job Title | jobTitle |
| Annual Revenue | annualRevenue |
| Service Required | serviceRequired |
| Additional Notes | additionalNotes |

---

# 5. n8n → Airtable Companies

| n8n Variable | Airtable Field |
|--------------|----------------|
| companyName | Company Name |
| annualRevenue | Annual Revenue |
| submissionTimestamp | Created Date |

---

# 6. n8n → Airtable Contacts

| n8n Variable | Airtable Field |
|--------------|----------------|
| contactName | Full Name |
| email | Email |
| mobileNumber | Mobile Number |
| jobTitle | Job Title |
| companyRecordId | Company |

---

# 7. n8n → Airtable Leads

| n8n Variable | Airtable Field |
|--------------|----------------|
| companyRecordId | Company |
| contactRecordId | Contact |
| serviceRequired | Service Required |
| annualRevenue | Annual Revenue |
| additionalNotes | Additional Notes |
| submissionTimestamp | Date Created |
| leadStatus | Lead Status |

---

# 8. Airtable → OpenAI

| Airtable Field | JSON Property |
|----------------|---------------|
| Company Name | company_name |
| Industry | industry |
| Annual Revenue | annual_revenue |
| Contact Name | contact_name |
| Job Title | job_title |
| Service Required | service_required |
| Additional Notes | additional_notes |

---

# 9. OpenAI → Airtable

| OpenAI JSON | Airtable Field |
|-------------|----------------|
| lead_score | Lead Score |
| priority | Priority |
| ai_summary | AI Summary |
| recommendation | Recommendation |

---

# 10. Airtable → Slack

| Airtable Field | Slack Property |
|----------------|----------------|
| Company Name | company |
| Contact Name | contact |
| Lead Score | score |
| Priority | priority |
| Service Required | service |
| AI Summary | summary |

---

# 11. Airtable → Calendly

| Airtable Field | Calendly Property |
|----------------|-------------------|
| Contact Name | invitee_name |
| Email | invitee_email |
| Mobile Number | phone_number |
| Service Required | notes |

---

# 12. Standard Variable Naming

ClientPilot uses camelCase for internal variables.

Examples:

| Business Field | Variable |
|----------------|----------|
| Company Name | companyName |
| Contact Name | contactName |
| Mobile Number | mobileNumber |
| Annual Revenue | annualRevenue |
| Service Required | serviceRequired |
| Additional Notes | additionalNotes |

JSON payloads exchanged with external APIs should use **snake_case** where appropriate to match the API specification.

---

# 13. Integration Notes

- Airtable Record IDs are used for linked-record relationships.
- Business IDs remain visible for reporting and business reference.
- All timestamps use ISO 8601 format where supported.
- Empty optional fields should be passed as `null` rather than empty strings when supported by the target system.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| 1.0 | 05 August 2026 | Initial technical field mapping. |

---

© Lewis Systems. All rights reserved.