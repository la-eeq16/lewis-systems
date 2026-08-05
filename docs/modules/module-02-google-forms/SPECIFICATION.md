# Module 2 – Google Forms Specification

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

This document defines the functional and technical specification for the ClientPilot Google Forms module.

The Google Form serves as the primary client intake interface for the ClientPilot MVP, enabling prospective clients to submit structured enquiries that initiate the automated client qualification workflow.

The form is designed to provide a professional user experience while collecting accurate and complete information required for downstream processing.

---

# 2. Objectives

The objectives of this module are to:

- Capture structured client enquiries.
- Standardise data collection.
- Improve lead quality.
- Reduce manual data entry.
- Validate user input.
- Support automated lead qualification.
- Integrate seamlessly with the ClientPilot CRM.
- Serve as the entry point into the automation workflow.

---

# 3. Scope

This specification covers:

- Google Form design
- User experience
- Form structure
- Data collection
- Input validation
- CRM integration
- Automation readiness
- Future enhancements

This document does not cover the implementation of automation workflows, which are specified in the n8n module.

---

# 4. Form Overview

The ClientPilot Google Form enables prospective clients to submit an enquiry regarding professional accounting services.

The form has been designed to:

- Be easy to complete
- Be mobile friendly
- Minimise unnecessary questions
- Collect all information required for qualification
- Support future automation

Estimated completion time:

**3–5 minutes**

---

# 5. Form Structure

The form consists of five logical sections.

## Section 1 – Welcome

Purpose:

Introduce ClientPilot and explain the purpose of the form.

Collects:

- Consent to continue

---

## Section 2 – Company Information

Purpose:

Capture information about the client's business.

Fields include:

- Company Name
- Industry
- Website
- Annual Revenue
- Number of Employees

---

## Section 3 – Contact Information

Purpose:

Capture details of the primary contact.

Fields include:

- First Name
- Last Name
- Email Address
- Mobile Number
- Job Title

---

## Section 4 – Service Requirements

Purpose:

Understand the client's needs.

Fields include:

- Services Required
- Urgency
- Additional Information
- Referral Source

---

## Section 5 – Review & Submit

Purpose:

Confirm submitted information.

Includes:

- Privacy statement
- Consent confirmation
- Submission button
- Confirmation message

---

# 6. Validation Rules

The following validation rules are implemented.

| Field | Validation |
|--------|------------|
| Company Name | Required |
| Email Address | Email validation |
| Mobile Number | Phone number validation |
| Services Required | Required |
| Consent | Required |
| Additional Information | Optional |
| Website | Optional |

Validation is used to improve data quality before automation begins.

---

# 7. User Journey

The expected user journey is:

```text
Prospective Client
        │
        ▼
Open Google Form
        │
        ▼
Read Welcome
        │
        ▼
Enter Company Details
        │
        ▼
Enter Contact Details
        │
        ▼
Select Services
        │
        ▼
Review Information
        │
        ▼
Submit Form
        │
        ▼
Confirmation Message
```

The submission marks the start of the ClientPilot automation workflow.

---

# 8. Integration Points

The Google Form integrates with the following systems.

| System | Purpose |
|--------|---------|
| Google Forms | Data collection |
| Airtable | CRM storage |
| n8n | Workflow automation |
| OpenAI | Lead qualification |
| Slack | Internal notifications |
| Calendly | Consultation booking |

---

# 9. Business Rules

The following business rules apply.

- Every submission creates a new lead enquiry.
- Company information must be captured before contact information.
- Email addresses must be valid.
- Required fields must be completed before submission.
- Consent must be provided before the form can be submitted.
- All submissions must be suitable for automated processing.

---

# 10. Design Principles

The Google Form follows the Lewis Systems engineering principles.

- Documentation First
- Business First
- Simplicity
- Professional Appearance
- Mobile First
- Automation Ready
- Data Quality
- Scalability

---

# 11. Future Enhancements

Future versions may include:

- Conditional questions
- File uploads
- CAPTCHA
- Multi-language support
- Dynamic service options
- AI-assisted form completion
- Client portal integration

---

# 12. Module Status

| Phase | Status |
|--------|--------|
| Design | ✅ Complete |
| Build | ✅ Complete |
| QA / Testing | ✅ Complete |
| Documentation | ✅ Complete |
| Git Commit | ⏳ Pending |
| Git Push | ⏳ Pending |

---

# 13. Approval

The Google Forms module has been designed, implemented, and quality assured as the client intake component of the ClientPilot MVP.

The module is approved for integration with Airtable and the upcoming n8n automation workflow.

Future modifications to the form should be documented through version updates and reviewed before implementation.

---

© Lewis Systems. All rights reserved.