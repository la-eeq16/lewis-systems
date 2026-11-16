# ClientPilot System Architecture

**Document Version:** 2.2  
**Product Version:** 0.3.0  
**Status:** Active – MVP Development  
**Company:** Lewis Systems  
**Product:** ClientPilot  
**Author:** La-eeq Lewis  
**Last Updated:** 16 November 2026

---

## 1. Purpose and Scope

This document describes ClientPilot's logical architecture, component responsibilities, data movement, technology choices, and current implementation boundaries.

The architecture is expressed in business capabilities first. The MVP uses specific third-party tools, but workflow requirements and business rules should remain portable where practical.

## 2. Architecture Overview

ClientPilot is organised into logical components:

1. **Intake:** receives and validates prospective-client information.
2. **CRM and Data:** stores companies, contacts, leads, qualifications, meetings, activities, settings, and workflow logs.
3. **Qualification:** applies deterministic business rules and produces a score and outcome.
4. **Communication:** sends configured prospect emails and, in a later module, internal notifications.
5. **Scheduling:** provides a booking hand-off and later synchronises booking events.
6. **Workflow Orchestration:** coordinates component interactions and error handling.
7. **Administration and Monitoring:** maintains customer-specific settings and operational visibility.
8. **AI Services (planned):** adds assisted analysis and meeting preparation after the rule-based MVP is validated.

## 3. Logical Architecture

```text
Prospective Client
       |
       v
Intake Form (Google Forms)
       |
       v
Response Capture (Google Sheets)
       |
       v
Workflow Orchestration (Make)
       |
       +----> Validate Submission
       |
       +----> CRM (Airtable)
       |         |
       |         +--> Find/Create Company
       |         +--> Find/Create Contact
       |         +--> Create Lead
       |
       +----> Rule-Based Qualification (Make)
       |         |
       |         +--> Calculate component scores
       |         +--> Determine qualification outcome
       |         +--> Update Lead / Qualification
       |
       +----> Communication (Gmail; configured email steps)
       |
       +----> Booking Hand-off (Calendly link)
       |
       +----> Activity / Workflow Logging (Airtable, where configured)

Planned extensions:
- OpenAI-assisted analysis and meeting preparation
- Slack internal notifications
- Calendly booking-event synchronisation
- Enhanced monitoring and administrator alerts
```

## 4. Component Responsibilities and Technology

| Component | Responsibility | MVP technology / state |
| --- | --- | --- |
| Intake | Capture prospect fields | Google Forms |
| Response capture | Make submission data available | Google Sheets |
| Orchestration | Run intake and qualification scenarios | Make |
| CRM | Store linked business records | Airtable |
| Qualification | Apply deterministic scoring rules | Make WF-001B |
| Prospect communication | Send configured email | Gmail, as recorded in workflow design |
| Booking hand-off | Provide firm's booking link | Calendly link; synchronisation planned |
| Internal notifications | Notify staff | Slack planned |
| AI services | AI recommendations and meeting brief | OpenAI planned |
| Monitoring | Record executions, errors, and outcomes | Airtable logging design; implementation verification outstanding |

## 5. Workflow Scenario Boundaries

### WF-001A – Client Intake

Expected responsibilities:

- Receive a new form response.
- Standardise and validate input fields.
- Search for an existing company.
- Create or update the company.
- Search for an existing contact.
- Create or update the contact.
- Create a lead linked to the company and primary contact.

### WF-001B – Lead Qualification

Expected responsibilities:

- Detect or receive a lead requiring qualification.
- Retrieve the required lead fields.
- Calculate component scores using the approved rule set.
- Calculate the total score.
- Assign a qualification outcome.
- Update the lead and create/update the associated qualification record.
- Perform configured follow-up or booking-link hand-off steps.

These responsibilities are the documented design. The live scenario configuration and exported blueprints must be reviewed to verify exact module order, filters, mappings, and error routes.

## 6. Qualification Architecture – Rule-Based MVP

The current MVP qualification path is deterministic and does not require an AI model.

The documented score inputs are:

| Factor | Documented scoring |
| --- | --- |
| Annual revenue | 0 / 10 / 20 / 30 |
| Service requested | 25 / 20 / 15 / 10 / 5 |
| Urgency | 15 / 11 / 7 / 3 |
| Employee count | 2 / 4 / 6 / 8 / 10 |
| Budget | 0; not collected by the current intake form |

Industry and decision-maker status may be collected or validated, but do not contribute to the documented v1 score.

Outcome bands:

- **Qualified:** score 64 or higher.
- **Review Required:** score 40–63.
- **Not Qualified:** score below 40.

The component scoring tables, missing-value handling, maximum score, and boundary conditions must be verified against the live Make scenario. The Settings table contains threshold fields, but WF-001B is documented as using fixed thresholds at present. Dynamic Settings-driven thresholds remain planned.

AI must not silently change the rule-based score or outcome. Any later AI recommendation should be separately identified, tested, and subject to a defined human-review policy.

## 7. Data Architecture

Airtable is the current MVP CRM store. The conceptual entities are:

- Companies
- Contacts
- Leads
- Qualifications
- Meetings
- Activities
- Workflow Logs
- Settings

The current Airtable implementation does not include a dedicated Organization table. Organization identifiers are recorded only in selected locations, and full per-record tenant isolation is not complete. The conceptual model describes the intended future multi-tenant design; it must not be mistaken for a security control already implemented.

See [05-DATA-MODEL.md](05-DATA-MODEL.md) for entity definitions and implementation gaps.

## 8. Integration and Trust Boundaries

ClientPilot depends on external services. Each integration should be treated as an independent failure boundary.

- Google Forms / Sheets provide intake and response data.
- Make orchestrates workflows and accesses connected services.
- Airtable stores CRM data.
- Gmail sends configured prospect communication.
- Calendly provides booking links; event synchronisation is planned.
- Slack and OpenAI are planned extensions.

Credentials must be stored in the providers' secure connection mechanisms or approved secret storage, not in source files, logs, exported blueprints, or public documentation.

## 9. Error Handling and Observability

The intended operational pattern is:

1. Detect a failed or invalid step.
2. Preserve enough context to identify the affected workflow and record.
3. Retry only when the error is transient and retrying is safe.
4. Avoid duplicate CRM records or duplicate messages on retry.
5. Record execution status and a useful error description.
6. Alert an authorised administrator when manual intervention is required.
7. Document the recovery action.

The full implementation of alerts, idempotency controls, and recovery routes remains to be verified and completed.

## 10. Security, Privacy, and Multi-Tenancy

- Use least-privilege access for connected accounts.
- Do not commit credentials, tokens, or customer data.
- Minimise personal information included in notifications.
- Restrict Airtable base and Make scenario access to authorised personnel.
- Define retention and deletion procedures before handling live customer data.
- Implement and test tenant isolation before serving multiple independent firms from a shared data environment.

The current MVP should be treated as a single-customer implementation until multi-tenant isolation is designed, implemented, and tested.

## 11. Platform Strategy

Make is the selected workflow platform for the MVP. n8n is a possible future migration option, not a current parallel implementation requirement. Any migration should be justified by operating cost, control, hosting, integration, or customer requirements.

The workflow specifications and data model remain the platform-independent references. See [ADR-004](adr/ADR-004-make-automation-platform.md).

## 12. Future Architecture Extensions

- OpenAI-assisted lead analysis and meeting preparation.
- Slack notifications and administrator alerts.
- Calendly event synchronisation.
- Dedicated administration interface.
- Stronger tenant isolation and user management.
- Dedicated relational database if scale and requirements justify it.

## 13. Architecture Acceptance Conditions

Before the MVP is considered pilot-ready:

- WF-001A and WF-001B match the approved workflow and data mappings.
- Score calculations and outcome boundaries pass test cases.
- Duplicate and retry behaviour is understood and tested.
- CRM links and workflow logs are verified.
- Integration failures have documented recovery steps.
- Security and customer-data handling have been reviewed.
- Make blueprint exports are sanitised and version-controlled.

---

© Lewis Systems. All rights reserved.
