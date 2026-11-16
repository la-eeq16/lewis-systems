# ClientPilot Project Status

**Document Version:** 3.3  
**Product Version:** 0.3.0  
**Status:** Active Development  
**Company:** Lewis Systems  
**Product:** ClientPilot  
**Author:** La-eeq Lewis  
**Last Updated:** 16 November 2026

---

## 1. Purpose

This document is the operational status record for ClientPilot. It records the current development phase, completed and active work, outstanding deliverables, dependencies, and next milestones.

Status statements distinguish between work documented as implemented, work present in the GitHub repository, and work that still requires evidence or verification.

## 2. Overall status

| Item | Current status |
| --- | --- |
| Development phase | Phase 3 – MVP Implementation |
| Current module | Module 3 – Workflow Automation |
| Current sprint | Sprint 2 – Workflow Automation |
| Product version | 0.3.0 |
| MVP automation platform | Make |
| Future platform option | n8n, subject to later review |
| Pilot launch | Not yet ready; end-to-end validation remains |

ClientPilot has completed its initial foundation and solution-design work and is implementing the MVP workflow layer.

## 3. Module status

| Module | Scope | Status |
| --- | --- | --- |
| 1 – CRM Database | Airtable CRM structure, relationships, views, and QA | Documented complete |
| 2 – Google Forms Client Intake | Form, response capture, validation, and field mapping | Documented complete |
| 3 – Workflow Automation | WF-001A intake and WF-001B qualification on Make | In progress |
| 4 – OpenAI Qualification | AI-assisted lead evaluation | Pending |
| 5 – Slack Notifications | Internal workflow notifications | Pending |
| 6 – Calendly Integration | Booking workflow and synchronisation | Pending |
| 7 – End-to-End MVP Testing | Integrated testing and acceptance | Pending |

“Documented complete” reflects the current project records. External Airtable and Google configuration should be rechecked whenever changes are made; repository documentation alone is not proof that a live service remains correctly configured.

## 4. Current workflow implementation

### 4.1 WF-001A – Client Intake (Make)

**Recorded status:** Built and tested.

The scenario is intended to:

1. Receive a new Google Forms response through the response spreadsheet.
2. Map the submitted information into standardised variables.
3. Validate required intake fields.
4. Search for an existing company.
5. Update an existing company or create a new company.
6. Search for an existing contact.
7. Update an existing contact or create a new contact.
8. Create the lead and associate it with the relevant CRM records.

The company/contact decision paths must preserve the following outcomes:

- Existing company and existing contact: update both, then create the lead.
- Existing company and new contact: update the company, create the contact, then create the lead.
- New company: create the company and contact, then create the lead.

### 4.2 WF-001B – Lead Qualification (Make)

**Recorded status:** Built and tested using rule-based scoring.

The scenario is intended to:

1. Detect a lead requiring qualification.
2. Retrieve the relevant lead data.
3. Calculate the component scores.
4. Calculate the overall qualification score.
5. assign a qualification outcome.
6. Update the lead and create the associated qualification record.

The documented outcome thresholds are:

| Score | Outcome |
| --- | --- |
| 64–100 | Qualified |
| 40–63 | Review Required |
| 0–39 | Not Qualified |

The scoring rules and thresholds must be verified against the live Make scenario and Airtable configuration before being treated as final production rules. AI evaluation is a later enhancement and is not the current qualification mechanism.

### 4.3 Repository evidence still outstanding

The GitHub repository does not yet contain the exported Make blueprints for WF-001A and WF-001B, and the referenced detailed Make implementation document is not yet present at its documented path.

Outstanding repository deliverables:

- Export and sanitise the WF-001A Make blueprint.
- Export and sanitise the WF-001B Make blueprint.
- Add the scenario-specific implementation documents.
- Record the module and scenario versions.
- Add test cases and representative, non-sensitive test evidence.
- Confirm the exports contain no secrets, personal customer data, or unnecessary environment-specific identifiers.

Do not commit credentials, access tokens, private customer data, or live connection secrets.

## 5. Current sprint – Sprint 2: Workflow Automation

### Sprint objective

Harden and document WF-001 on Make so that the intake and rule-based qualification pipeline is reliable, traceable, and ready for integrated MVP testing.

### Work tracking

| Task | Status |
| --- | --- |
| Workflow architecture for WF-001A / WF-001B | Complete in documentation |
| WF-001A client intake scenario | Built and tested, per project record |
| WF-001B rule-based qualification scenario | Built and tested, per project record |
| Make implementation document | Outstanding in repository |
| Sanitised Make blueprint exports | Outstanding |
| Administrator alert for failed workflows | Outstanding |
| Verify Settings-driven qualification threshold | Outstanding |
| Confirm workflow logging and recovery behaviour | Outstanding |
| End-to-end regression testing | Pending |

## 6. Planned modules and dependencies

### Module 4 – OpenAI Qualification

- Define the AI evaluation requirements and output schema.
- Decide how AI recommendations complement rule-based scoring.
- Handle unavailable, invalid, or low-confidence AI responses.
- Retain a human-review path for uncertain decisions.
- Test outputs against representative cases.

### Module 5 – Slack Notifications

- Define notification events and recipients.
- Avoid exposing unnecessary customer information in messages.
- Test successful and failed workflow notifications.

### Module 6 – Calendly Integration

- Define booking-link and booking-confirmation behaviour.
- Map booking information to the relevant lead and meeting records.
- Test rescheduling and cancellation handling where supported.

### Module 7 – End-to-End MVP Testing

- Test the full intake-to-qualification journey.
- Test duplicate company and contact scenarios.
- Test missing or invalid intake fields.
- Test failure handling and recovery.
- Verify CRM relationships and workflow logs.
- Record acceptance results and known limitations.

## 7. Architecture decision: Make and n8n

Make is the selected automation platform for the MVP. A future migration to n8n may be considered after the first paying client or earlier if a concrete cost, control, hosting, or client requirement justifies it.

The workflow design and business rules remain the platform-independent reference. See [ADR-004](adr/ADR-004-make-automation-platform.md).

The existing `module-03-n8n` directory is a legacy documentation location and must not be interpreted as the current execution platform. Restructuring it into a platform-neutral Module 3 with separate Make and n8n sections is planned.

## 8. Risks and controls

| Risk | Control / next action |
| --- | --- |
| Make blueprint exports are absent from GitHub | Export, sanitise, document, and commit both scenarios |
| Live configuration may differ from documentation | Recheck Make and Airtable configuration during testing |
| Qualification thresholds may be hard-coded or inconsistent | Verify the source of truth and test boundary values |
| Workflow failures may go unnoticed | Complete administrator alerts, logging, and recovery tests |
| Legacy n8n documentation may cause confusion | Mark as legacy and restructure Module 3 |
| Customer information or credentials could be exposed | Use synthetic test data and sanitise exports before committing |
| Documentation may overstate completion | Require implementation and test evidence before closing tasks |

## 9. Next milestones

1. Commit the sanitised Make blueprints and scenario implementation documentation.
2. Verify WF-001A and WF-001B against the live Make scenarios and Airtable base.
3. Complete failure alerts, logging, and qualification threshold configuration.
4. Complete OpenAI, Slack, and Calendly work according to approved scope.
5. Execute and document end-to-end MVP tests.
6. Review pilot readiness and outstanding risks.
7. Reassess n8n migration only when the review criteria in ADR-004 are met.

## 10. Completion criteria

A module may be marked complete only when:

- Its requirements and scope are documented.
- Its implementation is present and configured.
- Required tests have passed and evidence is recorded.
- Failure and recovery behaviour have been considered.
- Relevant documentation and diagrams are current.
- Changes and appropriate implementation assets are committed and pushed.
- Known limitations are explicitly recorded.

---

© Lewis Systems. All rights reserved.
