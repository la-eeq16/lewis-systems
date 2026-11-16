# ClientPilot Workflow Design

**Document Version:** 1.2  
**Product Version:** 0.3.0  
**Status:** Active – MVP Implementation  
**Company:** Lewis Systems  
**Product:** ClientPilot  
**Author:** La-eeq Lewis  
**Last Updated:** 16 November 2026

---

## 1. Purpose

This document defines ClientPilot's business workflows independently of a specific automation platform. It describes triggers, inputs, process steps, decisions, outputs, data changes, and failure expectations.

Make is the current MVP implementation platform. Scenario-specific module mappings and exported blueprints belong in the Module 3 implementation documentation.

## 2. Workflow Principles

Every workflow should:

- Have a clear business trigger and outcome.
- Validate input before creating downstream records.
- Maintain correct relationships between CRM records.
- Avoid unintended duplicate side effects.
- Record important events and execution failures.
- Define safe retry and manual recovery behaviour.
- Protect customer data and credentials.
- Be independently testable.
- Remain portable across workflow platforms where practical.

## 3. Workflow Catalogue

| ID | Workflow | Purpose | Status |
| --- | --- | --- | --- |
| WF-001A | Client Intake | Validate enquiry and create/update CRM records | Recorded as built and tested on Make; exports/evidence outstanding |
| WF-001B | Lead Qualification | Score a lead and store its qualification outcome | Recorded as built and tested on Make; exports/evidence outstanding |
| WF-002 | Consultation Booking | Receive and synchronise booking events | Planned |
| WF-003 | AI Meeting Preparation | Generate a consultation brief | Planned |
| WF-004 | Lead Follow-up | Manage follow-up tasks and messages | Planned |
| WF-005 | Lead Nurturing | Manage longer-term prospect communication | Planned |
| WF-006 | Client Onboarding | Convert an accepted prospect into an onboarded client | Planned |
| WF-007 | Reporting and Analytics | Measure pipeline and workflow performance | Planned |
| WF-008 | Administration | Manage configuration and operational controls | Planned |

WF-001A and WF-001B together form the initial WF-001 intake-to-qualification process.

## 4. WF-001A – Client Intake

### Trigger

A prospective client submits the Google Form and a new response becomes available to the workflow.

### Inputs

The form's configured business and contact fields, including company details, contact details, service requirements, revenue, employee count, urgency, and other required validation fields.

The exact live form schema is authoritative for implementation mapping and must be maintained in the implementation record.

### Business process

1. Receive the new response.
2. Map response values into standardised workflow variables.
3. Validate required fields and applicable formats.
4. If required information is invalid or missing, stop record creation and record/route the validation outcome.
5. Search Airtable Companies using the approved company matching rule.
6. If the company exists, update it; otherwise create it.
7. Search Airtable Contacts using the approved contact matching rule and company relationship.
8. If the contact exists, update it; otherwise create it.
9. Create a Lead linked to the correct Company and primary Contact.
10. Record the processing result and make the new Lead available for qualification.

### Company/contact outcomes

| Company | Contact | Expected action |
| --- | --- | --- |
| Found | Found | Update Company; update Contact; create Lead |
| Found | Not found | Update Company; create Contact; create Lead |
| Not found | Not found | Create Company; create Contact; create Lead |
| Not found | Found | Treat as an exception: verify the contact's company association before creating or linking records |

The fourth case must not silently attach a contact to an unrelated company. The matching logic and exception route should be documented and tested.

### Outputs

- Company record ID.
- Contact record ID.
- Lead record ID.
- Validation and processing outcome.
- Workflow execution trace where configured.

## 5. WF-001B – Rule-Based Lead Qualification

### Trigger

A newly created or eligible Lead is detected by the qualification scenario.

### Inputs

The lead's mapped revenue, services requested, urgency, employee count, and any other fields required by the approved scoring rules.

### Business process

1. Retrieve the Lead record.
2. Validate that the scoring inputs are available and usable.
3. Calculate the Revenue Score.
4. Calculate the Service Score.
5. Calculate the Urgency Score.
6. Calculate the Employee Score.
7. Set Budget Score to zero in the current documented MVP because the form does not collect budget.
8. Calculate the total Qualification Score.
9. Determine the qualification outcome using the approved thresholds.
10. Update the Lead with the score, status, reason, and qualification date.
11. Create or update the related Qualification record.
12. For Qualified leads, perform the configured booking-link hand-off and relevant email/activity steps where enabled.
13. For Not Qualified leads, perform the configured follow-up email/activity steps where enabled.
14. For Review Required leads, retain the lead for staff review; do not automatically treat it as booked or rejected.
15. Record the workflow outcome and any error requiring recovery.

### Documented score outcome bands

| Total score | Outcome |
| --- | --- |
| 64–100 | Qualified |
| 40–63 | Review Required |
| 0–39 | Not Qualified |

The architecture records the current scoring components as revenue (0/10/20/30), service (25/20/15/10/5), urgency (15/11/7/3), employee count (2/4/6/8/10), and budget (0). The exact category-to-points mapping and missing-value rules must be confirmed from the live Make scenario before these values are treated as final. The maximum possible score and score boundaries must be tested.

### Outputs

- Total qualification score.
- Qualification status.
- Qualification reason.
- Qualification record linked to the Lead.
- Relevant email / booking-link hand-off outcome, if enabled.
- Workflow execution result.

## 6. Qualification Decision Behaviour

- **Qualified:** eligible for the firm's configured consultation booking hand-off.
- **Review Required:** retained for manual review; no automatic approval or rejection.
- **Not Qualified:** handled according to the firm's configured follow-up policy.

A booking link being sent does not mean a meeting has been booked. A Meeting record with status Awaiting Booking is not a confirmed appointment.

## 7. Data and Field Mapping

The authoritative logical data definitions are in [05-DATA-MODEL.md](05-DATA-MODEL.md). The live Airtable base and Google Form determine exact field names and select-option values.

Key relationships:

- Lead → Company (one linked Company).
- Lead → primary Contact (one linked Contact).
- Qualification → Lead (one linked Lead).
- Meeting → Lead (one linked Lead, when a meeting record is created).
- Activity / Workflow Log → relevant Lead where applicable.

The implementation record must document source field, destination field, transformation, default, validation, and error behaviour for each mapping.

## 8. Error Handling and Recovery Requirements

| Failure | Required behaviour |
| --- | --- |
| Missing or invalid required intake data | Stop downstream record creation; record validation result |
| Company or contact search returns multiple matches | Do not guess; route for manual resolution |
| Airtable unavailable | Preserve execution context; retry safely where appropriate |
| Create/update step fails | Prevent duplicate follow-on actions; record failure |
| Qualification input missing | Do not invent a score; mark for review or error handling |
| Email send fails | Record failure and provide a safe manual retry path |
| Scenario is retried | Prevent duplicate leads, activities, emails, or qualification records where possible |

The exact Make error handlers and retry settings must be confirmed in the exported blueprint and live scenario.

## 9. Activity and Workflow Logging

Events that should be recorded include:

- Lead Submitted.
- Company Created / Updated.
- Contact Created / Updated.
- Lead Created.
- Qualification Completed.
- Lead Updated.
- Booking Link Sent.
- Email Sent.
- Workflow Failed.
- Workflow Recovered.

Each log should include a timestamp and relevant record reference. Avoid storing secrets or unnecessary personal information in logs.

## 10. Implementation Record

The current Make implementation details should be maintained in a dedicated Module 3 implementation area. The existing reference to `docs/modules/module-03-n8n/WF-001-MAKE-IMPLEMENTATION.md` is a legacy/missing path and must not be treated as a valid current implementation document.

Required Module 3 implementation artefacts:

- WF-001A Make scenario description and field mapping.
- WF-001B Make scenario description and scoring mapping.
- Sanitised Make blueprint exports.
- Test cases and observed results.
- Error handling and recovery notes.
- Change history for scenario updates.

Do not commit Make credentials, access tokens, real customer data, or sensitive connection metadata.

## 11. Future Workflows

WF-002 consultation booking synchronisation, WF-003 AI meeting preparation, notifications, lead nurturing, onboarding, analytics, and administration remain future workflow areas until separately designed, implemented, and tested.

## 12. Definition of Workflow Completion

A workflow is complete only when its trigger, inputs, logic, data mappings, normal paths, exception paths, retry behaviour, outputs, and tests are documented and verified against the deployed implementation. A design document or scenario outline alone is not evidence of completion.

---

© Lewis Systems. All rights reserved.
