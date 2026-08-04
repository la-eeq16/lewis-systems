# Google Form Field Mapping

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

This document defines how every Google Form field maps into the ClientPilot CRM.

It serves as the implementation blueprint for Google Forms, Google Sheets, n8n, Airtable, and future integrations.

---

# 2. Data Flow

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
```

---

# 3. CRM Tables Used

The automation will create or update records in the following Airtable tables:

- Companies
- Contacts
- Leads
- Qualifications
- Activities
- Workflow Logs

---

# 4. Google Form → Airtable Mapping

## Contact Information

| Google Form Field | Airtable Table | Airtable Field |
|-------------------|---------------|----------------|
| First Name | Contacts | First Name |
| Last Name | Contacts | Last Name |
| Business Email | Contacts | Email |
| Phone Number | Contacts | Phone Number |
| Job Title | Contacts | Job Title |
| Preferred Contact Method | Contacts | Preferred Contact Method |

---

## Company Information

| Google Form Field | Airtable Table | Airtable Field |
|-------------------|---------------|----------------|
| Company Name | Companies | Company Name |
| Company Website | Companies | Website |
| Industry | Companies | Industry |
| Number of Employees | Companies | Employee Count |
| Annual Revenue Range | Companies | Annual Revenue |
| Country | Companies | Country |
| Province | Companies | Province |
| City | Companies | City |

---

## Lead Information

| Google Form Field | Airtable Table | Airtable Field |
|-------------------|---------------|----------------|
| Services Required | Leads | Services Requested |
| Business Challenge | Leads | Notes |
| Desired Outcome | Leads | Notes |
| Estimated Budget | Leads | Budget |
| Preferred Start Date | Leads | Start Date |
| Preferred Consultation Method | Leads | Consultation Method |
| Best Time To Contact | Leads | Preferred Contact Time |
| Additional Information | Leads | Notes |

---

## System Generated Fields

The following fields are created automatically by the automation.

### Companies

- Company ID
- Created Time
- Last Modified

### Contacts

- Contact ID
- Contact Status
- Created Time
- Last Modified

### Leads

- Lead ID
- Lead Name
- Lead Source = Google Form
- Lead Status = New
- Qualification Status = Pending
- Submission Date
- Assigned Consultant
- Created Time
- Last Modified

### Qualifications

Automatically created after lead creation.

Fields populated:

- Qualification ID
- Lead
- Company
- Contact
- Qualification Status
- AI Recommendation
- Total Score

---

### Activities

Automatically created.

Fields populated:

- Activity ID
- Activity Name
- Lead
- Company
- Contact
- Activity Type = Form Submission
- Activity Status = Completed
- Source = Google Forms
- Activity Date

---

### Workflow Logs

Automatically created.

Fields populated:

- Workflow Log ID
- Workflow Name
- Workflow Type = Client Intake
- Trigger Source = Google Forms
- Execution Status
- Started At
- Finished At
- Duration
- Execution ID

---

# 5. Duplicate Handling

Before creating records, the automation must check for existing data.

## Company Matching

Primary Match

- Company Name

Secondary Match

- Website

---

## Contact Matching

Primary Match

- Email Address

Secondary Match

- Phone Number

---

## Lead Matching

A new Lead is created for every new enquiry.

Multiple enquiries from the same company are permitted.

---

# 6. Relationships

After record creation the automation must link:

Company
        │
        ▼
Contact
        │
        ▼
Lead
        │
        ├── Qualification
        ├── Activity
        └── Workflow Log

---

# 7. Validation Rules

The automation must validate:

- Required fields completed
- Valid email address
- Company Name supplied
- Contact Name supplied
- Services selected
- Privacy consent accepted

If validation fails:

- Stop workflow
- Record failure in Workflow Logs
- Notify administrator (future enhancement)

---

# 8. Error Handling

If any stage fails:

- Log the error
- Record execution status
- Save the error message
- Stop downstream processing

Future versions may include automatic retries.

---

# 9. Future Integrations

This mapping supports future integration with:

- Calendly
- Slack
- Gmail
- OpenAI
- WhatsApp
- Client Portal
- Reporting Dashboard

---

# 10. Revision History

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 04 August 2026 | Initial Google Form field mapping specification. |