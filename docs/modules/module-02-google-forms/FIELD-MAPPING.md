# Module 2 – Google Forms Field Mapping

**Module:** 02 – Google Forms

**Document Version:** 1.0

**Product Version:** 0.3.0

**Status:** ✅ Approved

**Company:** Lewis Systems

**Product:** ClientPilot

**Author:** La-eeq Lewis

**Phase:** Phase 3 – MVP Implementation

**Last Updated:** 05 August 2026

---

# 1. Purpose

This document defines the mapping between the ClientPilot Google Form and the Airtable CRM.

It ensures every response submitted through the Google Form is stored consistently and correctly within the ClientPilot CRM.

This mapping serves as the primary reference for the n8n automation workflow and future integrations.

---

# 2. Mapping Overview

The Google Form captures information across four core business areas:

- Company Information
- Contact Information
- Service Requirements
- Consent

Each response is mapped to one or more Airtable tables.

---

# 3. Google Form → Airtable Mapping

| Google Form Field | Airtable Table | Airtable Field | Data Type | Required | Notes |
|-------------------|---------------|----------------|-----------|----------|-------|
| Company Name | Companies | Company Name | Single Line Text | ✅ | Used to find or create a company |
| Industry | Companies | Industry | Single Select | ✅ | Used for reporting and qualification |
| Website | Companies | Website | URL | No | Optional |
| Annual Revenue | Companies | Annual Revenue | Single Select | ✅ | Used during qualification |
| Number of Employees | Companies | Employee Count | Number | ✅ | Used for reporting |
| First Name | Contacts | First Name | Single Line Text | ✅ | Primary contact |
| Last Name | Contacts | Last Name | Single Line Text | ✅ | Primary contact |
| Email Address | Contacts | Email | Email | ✅ | Used for communication |
| Mobile Number | Contacts | Phone Number | Phone Number | ✅ | Used for follow-up |
| Job Title | Contacts | Job Title | Single Line Text | No | Useful for AI research |
| Services Required | Leads | Services Requested | Multiple Select | ✅ | Supports multiple selections |
| Urgency | Leads | Priority | Single Select | ✅ | Determines lead priority |
| Additional Information | Leads | Description | Long Text | No | Used by AI during qualification |
| Referral Source | Leads | Lead Source | Single Select | ✅ | Marketing analytics |
| Consent | Leads | Consent Given | Checkbox | ✅ | Compliance requirement |
| Submission Date | Leads | Submission Date | Created Time | Automatic | Recorded automatically |

---

# 4. Airtable Tables Used

The Google Form interacts with the following CRM tables.

## Companies

Stores business information.

Fields populated:

- Company Name
- Industry
- Website
- Annual Revenue
- Employee Count

---

## Contacts

Stores the primary contact.

Fields populated:

- First Name
- Last Name
- Email
- Phone Number
- Job Title

---

## Leads

Stores the enquiry.

Fields populated:

- Services Requested
- Priority
- Description
- Lead Source
- Consent Given
- Submission Date

---

# 5. Automation Logic

The intended automation flow is:

```text
Google Form Submitted
        │
        ▼
Read Form Response
        │
        ▼
Search Companies
        │
 ┌──────┴──────┐
 │             │
Exists       Doesn't Exist
 │             │
 │         Create Company
 │             │
 └──────┬──────┘
        ▼
Search Contacts
        │
 ┌──────┴──────┐
 │             │
Exists       Doesn't Exist
 │             │
 │         Create Contact
 │             │
 └──────┬──────┘
        ▼
Create Lead
        │
        ▼
Continue Workflow
```

---

# 6. Data Validation Rules

Before data is written to Airtable, the automation should validate:

- Company Name is not empty.
- Email Address is valid.
- Mobile Number is valid.
- Required fields are completed.
- Consent is provided.
- Duplicate companies are identified.
- Duplicate contacts are identified.

---

# 7. Business Rules

- One company may have many contacts.
- One company may have many leads.
- One contact may submit multiple enquiries.
- A lead must always belong to a company.
- A lead must always have a primary contact.
- Company records should be reused when possible.
- Contact records should be reused when possible.

---

# 8. Integration Dependencies

This mapping supports:

- Google Forms
- Airtable
- n8n
- OpenAI
- Slack
- Calendly

Any future changes to field names or data types should be reflected in this document before implementation.

---

# 9. Approval

This field mapping has been reviewed and approved as the official integration reference for the ClientPilot MVP.

It will serve as the implementation guide for all automation workflows involving Google Forms and Airtable.

---

© Lewis Systems. All rights reserved.