# Module 3 – Field Mapping

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

This document defines how client information flows between the integrated systems used by ClientPilot.

It provides a complete mapping of data from the point of submission through to CRM storage, AI qualification, notifications, and scheduling.

The field mappings ensure consistency, reduce implementation errors, and provide a single reference for all workflow integrations.

---

# 2. Data Flow Overview

```text
Google Forms
      │
      ▼
Google Sheets
      │
      ▼
n8n
      │
 ┌────┼────┬─────────┐
 ▼    ▼    ▼         ▼
Airtable OpenAI Slack Calendly
```

---

# 3. Google Forms → Google Sheets

| Google Form Field | Google Sheets Column |
|-------------------|----------------------|
| Submission Time | Timestamp |
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

| Google Sheets Column | n8n Variable |
|----------------------|--------------|
| Timestamp | submissionTimestamp |
| Company Name | companyName |
| Contact Name | contactName |
| Email Address | email |
| Mobile Number | mobile |
| Job Title | jobTitle |
| Annual Revenue | annualRevenue |
| Service Required | serviceRequired |
| Additional Notes | notes |

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
| mobile | Mobile Number |
| jobTitle | Job Title |
| Company ID | Company (Linked Record) |

---

# 7. n8n → Airtable Leads

| n8n Variable | Airtable Field |
|--------------|----------------|
| Company ID | Company |
| Contact ID | Contact |
| serviceRequired | Service Required |
| annualRevenue | Annual Revenue |
| notes | Additional Notes |
| submissionTimestamp | Date Created |
| Lead Status | Lead Status |

---

# 8. Airtable → OpenAI

The following information is sent to OpenAI for lead qualification.

| Airtable Field |
|----------------|
| Company Name |
| Industry |
| Annual Revenue |
| Contact Name |
| Job Title |
| Service Required |
| Additional Notes |

---

# 9. OpenAI → Airtable Qualification

| OpenAI Output | Airtable Field |
|---------------|----------------|
| Lead Score | Lead Score |
| Priority | Priority |
| Qualification Summary | AI Summary |
| Recommended Action | Recommendation |

---

# 10. Airtable → Slack

| Airtable Field | Slack Message |
|----------------|---------------|
| Company Name | Company |
| Contact Name | Contact |
| Lead Score | Score |
| Priority | Priority |
| Service Required | Requested Service |
| AI Summary | Summary |

---

# 11. Airtable → Calendly

| Airtable Field | Calendly |
|----------------|-----------|
| Contact Name | Invitee Name |
| Email | Invitee Email |
| Mobile Number | Phone |
| Service Required | Meeting Notes |

---

# 12. Data Ownership

| System | Primary Responsibility |
|---------|------------------------|
| Google Forms | Client Data Collection |
| Google Sheets | Raw Submission Storage |
| n8n | Workflow Orchestration |
| Airtable | Master CRM |
| OpenAI | Lead Qualification |
| Slack | Team Notifications |
| Calendly | Consultation Scheduling |

---

# 13. Validation Rules

Before data is transferred between systems:

- Required fields must be populated.
- Email address must be valid.
- Mobile number must be valid.
- Company names should be normalised.
- Duplicate companies should not be created.
- Duplicate contacts should not be created.
- Lead records must reference both Company and Contact.

---

# 14. Future Mapping

Additional mappings may be introduced for:

- Gmail
- Proposal Generator
- Client Portal
- Executive Dashboard
- Reporting Engine
- Payment Platform

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| 1.0 | 05 August 2026 | Initial field mapping specification. |

---

© Lewis Systems. All rights reserved.