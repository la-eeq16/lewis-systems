# ClientPilot Product Requirements Document (PRD)

**Document Version:** 2.2  
**Product Version:** 0.3.0  
**Status:** Active – MVP Development  
**Company:** Lewis Systems  
**Product:** ClientPilot  
**Author:** La-eeq Lewis  
**Last Updated:** 16 November 2026

---

## 1. Purpose

This document defines what ClientPilot must do, who the initial product is for, and the requirements and boundaries of the first release. It is the product-level reference; implementation details belong in the architecture, data model, and workflow documents.

## 2. Product Overview

ClientPilot is a client-intake and lead-qualification platform being developed by Lewis Systems. It helps a service business capture enquiries, organise prospect information, assess suitability, and progress appropriate leads towards a consultation.

The first release targets **small accounting firms in South Africa**. This initial market is intentionally focused; it does not limit the wider Lewis Systems business, which may deliver custom systems to other small-business sectors.

## 3. Problem Statement

Small accounting firms may spend significant time manually processing enquiries, collecting missing information, checking whether prospects fit their services, and arranging follow-up. Slow or inconsistent handling can create administrative work and cause suitable opportunities to be missed.

ClientPilot aims to make this process more consistent, traceable, and efficient.

## 4. Product Goals

- Capture prospective-client enquiries in a consistent format.
- Validate required intake information.
- Create or update company, contact, and lead records.
- Apply transparent, repeatable lead-qualification rules.
- Make qualification outcomes and reasons visible to staff.
- Support follow-up and consultation booking for suitable leads.
- Maintain a traceable record of important workflow activity.
- Establish a modular foundation for later AI-assisted capabilities.

## 5. Users and Stakeholders

| User / stakeholder | Need |
| --- | --- |
| Accounting firm owner / administrator | Visibility of enquiries, lead outcomes, and workflow health |
| Consultant / accountant | Relevant prospect information and prioritised follow-up |
| Prospective client | Clear, timely handling of an enquiry |
| Lewis Systems administrator | Ability to configure, support, and troubleshoot the implementation |

User roles and access controls are part of the intended product model; a complete user-management interface is not part of the current MVP.

## 6. Scope

### 6.1 Current MVP scope

| Capability | MVP requirement | Current implementation direction |
| --- | --- | --- |
| Enquiry capture | Receive prospective-client information | Google Forms and response spreadsheet |
| Input validation | Check required fields and basic formats | Make workflow |
| CRM records | Find or create company and contact; create lead | Airtable via Make |
| Qualification | Calculate a rule-based score and outcome | WF-001B on Make |
| Outcome handling | Update lead and record qualification result | Airtable via Make |
| Follow-up | Send configured email where supported by the current scenario | Gmail integration |
| Booking hand-off | Provide configured booking link to qualified leads | Calendly link; full booking synchronisation planned |
| Workflow traceability | Record important events and failures | Airtable activity / workflow log design; verify implementation |

The Project Status document records WF-001A and WF-001B as built and tested. Their exported Make blueprints and full implementation evidence remain outstanding in GitHub.

### 6.2 Planned capabilities, not yet part of the verified current MVP

- OpenAI-assisted qualification and meeting preparation.
- Slack staff notifications.
- Automated Calendly event synchronisation and rescheduling.
- Configurable qualification thresholds read dynamically from Settings.
- Administrator failure alerts and enhanced recovery handling.
- End-to-end acceptance testing.

### 6.3 Out of scope for the initial MVP

- A custom CRM database or full CRM replacement.
- Billing and payment processing.
- A customer-facing portal or mobile application.
- Full subscription and tenant self-service management.
- Website builder functionality.
- Voice AI receptionist.

These boundaries may change through documented product decisions.

## 7. Functional Requirements

| ID | Requirement | Priority |
| --- | --- | --- |
| FR-001 | The system shall receive an enquiry containing the defined intake fields. | Must |
| FR-002 | The system shall validate required fields before creating downstream records. | Must |
| FR-003 | The system shall search for an existing company before creating a duplicate. | Must |
| FR-004 | The system shall search for an existing contact and create or update it as appropriate. | Must |
| FR-005 | The system shall create a lead linked to its company and primary contact. | Must |
| FR-006 | The system shall calculate a qualification score using documented rule-based criteria. | Must |
| FR-007 | The system shall assign Qualified, Review Required, or Not Qualified based on the configured score bands. | Must |
| FR-008 | The system shall store the score, outcome, and explanation against the lead and/or qualification record. | Must |
| FR-009 | The system shall provide the configured booking link to eligible leads when the relevant email step is enabled. | Should |
| FR-010 | The system should record important workflow events and failures. | Should |
| FR-011 | The system should notify authorised staff of important events and failures. | Planned |
| FR-012 | The system may use AI to provide additional recommendations after the AI module is designed and tested. | Future |

## 8. Non-Functional Requirements

- **Reliability:** workflow failures should be detectable and recoverable where possible.
- **Data integrity:** linked company, contact, lead, and qualification records must remain consistent.
- **Security:** credentials and customer data must not be exposed in source control or unnecessary notifications.
- **Privacy:** collect and retain only information needed for the defined business purpose.
- **Traceability:** important automated actions should be attributable to a workflow execution and timestamp.
- **Maintainability:** business rules and platform-specific implementation details should be documented separately.
- **Usability:** staff should be able to understand a lead's status and qualification reason.
- **Portability:** business logic and data definitions should not depend unnecessarily on Make-specific features.

## 9. Qualification Rules – Current Rule-Based Version

The current MVP uses rule-based scoring, not an AI decision. The documented score bands are:

| Total score | Qualification outcome |
| --- | --- |
| 64–100 | Qualified |
| 40–63 | Review Required |
| 0–39 | Not Qualified |

The architecture document records revenue, service, urgency, and employee criteria as scoring inputs. The exact points and boundary conditions must be validated against the live Make scenario and Airtable configuration before being treated as final. Budget is not collected by the current intake form and contributes zero in the documented MVP. Industry and decision-maker status are validated or stored but do not affect the v1 score.

## 10. Success Metrics

The pilot should establish baselines and measure:

- Enquiry-to-record processing success rate.
- Percentage of submissions requiring manual correction.
- Time from enquiry submission to first response.
- Qualification outcome distribution and staff agreement with outcomes.
- Consultation booking rate.
- Workflow failure and recovery rate.
- Administrative time saved.

Targets should be set after baseline data is available rather than inventing unsupported numeric goals.

## 11. Dependencies and Assumptions

- The accounting firm provides accurate service, qualification, and contact requirements.
- Google Forms, Google Sheets, Airtable, Make, Gmail, and Calendly remain available and appropriately authorised.
- Airtable field names and select options match the workflow mappings.
- The firm's booking link and communication settings are maintained correctly.
- The first pilot is configured for one client firm; production multi-tenant isolation is not yet complete.

## 12. Risks

| Risk | Response |
| --- | --- |
| Incomplete or inaccurate enquiry data | Validate required fields and provide a manual review path |
| Duplicate company/contact records | Define matching rules and test duplicate cases |
| Third-party service outage | Log failures, preserve data, and define retry/manual recovery |
| Incorrect qualification result | Keep rules transparent and test score boundaries |
| Exposure of customer data | Restrict access, minimise notification content, and sanitise exports |
| AI produces unreliable recommendations | Keep AI out of the current rule-based decision path until evaluated and reviewed |

## 13. Acceptance Criteria

The MVP is not ready for pilot release until the end-to-end flow has been tested with representative synthetic data and demonstrates:

1. Valid submissions create or update the correct company and contact records.
2. A lead is created with correct linked records and mapped fields.
3. Qualification scores and outcomes match approved test cases, including threshold boundaries.
4. Missing or invalid required information is handled safely.
5. Repeated submissions do not create unintended duplicate records.
6. Workflow errors are visible and recoverable through a documented process.
7. No secrets or real customer data are present in committed test assets.

## 14. Change Control

Changes to product scope, priorities, or acceptance criteria must be reflected in this document and the Project Status document. Material architectural choices must be recorded in an ADR.

---

© Lewis Systems. All rights reserved.
