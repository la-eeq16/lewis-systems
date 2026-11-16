# ClientPilot Project Status

**Document Version:** 3.4  
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
| Pilot launch | Not ready; end-to-end validation remains |

The project foundation and architecture/engineering documentation reviews have been completed. The MVP workflow implementation and verification work remains active.

## 3. Documentation work completed

### Stage 1 – Project foundation

Updated and aligned:

- README.md
- 00-PROJECT-INDEX.md
- 01-MASTER-PROJECT.md
- 13-PROJECT-STATUS.md

The documents now distinguish the wider Lewis Systems strategy (custom systems for small businesses) from ClientPilot's initial accounting-firm target market. Make is identified as the current MVP platform and n8n as a future option.

### Stage 2 – Architecture and engineering

Reviewed and updated:

- 02-PRODUCT-REQUIREMENTS.md
- 03-BUSINESS-REQUIREMENTS.md
- 04-SYSTEM-ARCHITECTURE.md
- 05-DATA-MODEL.md
- 06-DEVELOPMENT-STANDARDS.md
- 07-WORKFLOW-DESIGN.md

The updates clarify that the current qualification path is rule-based, not AI-driven; distinguish current MVP functionality from planned extensions; document the conceptual data model separately from the Airtable implementation; identify incomplete multi-tenancy; and describe WF-001A/WF-001B with exception and recovery requirements.

This is a documentation review. It does not independently verify the live Airtable base or Make scenarios.

## 4. Module status

| Module | Scope | Status |
| --- | --- | --- |
| 1 – CRM Database | Airtable CRM structure, relationships, views, and QA | Documented complete; live configuration verification remains advisable |
| 2 – Google Forms Client Intake | Form, response capture, validation, and field mapping | Documented complete |
| 3 – Workflow Automation | WF-001A intake and WF-001B qualification on Make | In progress |
| 4 – OpenAI Qualification | AI-assisted lead evaluation | Pending |
| 5 – Slack Notifications | Internal workflow notifications | Pending |
| 6 – Calendly Integration | Booking workflow and synchronisation | Pending |
| 7 – End-to-End MVP Testing | Integrated testing and acceptance | Pending |

## 5. Current workflow implementation

### 5.1 WF-001A – Client Intake (Make)

**Recorded status:** Built and tested, according to the project implementation record.

The scenario is intended to receive a form response, validate fields, find or create a company, find or create a contact, and create a linked lead.

The company/contact decision paths and the exception case for a contact found under a different company are described in [07-WORKFLOW-DESIGN.md](07-WORKFLOW-DESIGN.md).

### 5.2 WF-001B – Lead Qualification (Make)

**Recorded status:** Built and tested using rule-based scoring, according to the project implementation record.

The scenario is intended to retrieve a lead, calculate component scores, calculate the total score, determine an outcome, update the lead, and create/update the associated Qualification record.

Documented outcome thresholds:

| Score | Outcome |
| --- | --- |
| 64–100 | Qualified |
| 40–63 | Review Required |
| 0–39 | Not Qualified |

The component point mapping, missing-value handling, maximum score, and threshold boundaries must be checked against the live scenario and tested before production use. AI evaluation is a later enhancement and is not the current qualification mechanism.

### 5.3 Repository evidence outstanding

The GitHub repository does not yet contain exported Make blueprints for WF-001A and WF-001B. Detailed scenario implementation documents and test evidence are also outstanding.

Required deliverables:

- Export and sanitise the WF-001A Make blueprint.
- Export and sanitise the WF-001B Make blueprint.
- Add scenario-specific implementation documents and field mappings.
- Record scenario versions and change history.
- Add test cases and representative, non-sensitive test evidence.
- Confirm exports contain no secrets, personal customer data, or unnecessary environment-specific identifiers.

## 6. Current sprint – Sprint 2: Workflow Automation

### Objective

Harden and document WF-001 on Make so that intake and rule-based qualification are reliable, traceable, and ready for integrated MVP testing.

| Task | Status |
| --- | --- |
| Stage 1 project foundation documentation | Complete |
| Stage 2 architecture and engineering documentation review | Complete |
| WF-001A client intake scenario | Built and tested, per project record |
| WF-001B rule-based qualification scenario | Built and tested, per project record |
| Make implementation documents | Outstanding |
| Sanitised Make blueprint exports | Outstanding |
| Verify live Airtable fields and linked relationships | Outstanding |
| Verify score mappings and boundary cases | Outstanding |
| Administrator failure alert | Outstanding |
| Settings-driven qualification threshold | Outstanding |
| Workflow logging and recovery verification | Outstanding |
| End-to-end regression testing | Pending |

## 7. Planned modules and dependencies

### Module 4 – OpenAI Qualification

- Define AI evaluation requirements and output schema.
- Decide how AI recommendations complement rule-based scoring.
- Handle unavailable, invalid, or low-confidence responses.
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

## 8. Architecture decision: Make and n8n

Make is the selected automation platform for the MVP. A future migration to n8n may be considered after the first paying client or earlier if a concrete cost, control, hosting, or client requirement justifies it.

The workflow design and business rules remain the platform-independent reference. See [ADR-004](adr/ADR-004-make-automation-platform.md).

The existing `module-03-n8n` directory is a legacy documentation location and must not be interpreted as the current execution platform. Restructuring it into a platform-neutral Module 3 with separate Make and n8n sections remains planned.

## 9. Risks and controls

| Risk | Control / next action |
| --- | --- |
| Make blueprint exports are absent from GitHub | Export, sanitise, document, and commit both scenarios |
| Live configuration may differ from documentation | Recheck Make and Airtable configuration during implementation verification |
| Qualification thresholds may be hard-coded or inconsistent | Verify source of truth and test boundary values |
| Workflow failures may go unnoticed | Complete administrator alerts, logging, and recovery tests |
| Legacy n8n documentation may cause confusion | Mark as legacy and restructure Module 3 |
| Customer information or credentials could be exposed | Use synthetic test data and sanitise exports before committing |
| Documentation may overstate completion | Require implementation and test evidence before closing tasks |

## 10. Next milestones

1. Create the platform-neutral Module 3 documentation structure.
2. Add Make WF-001A and WF-001B implementation documents and sanitised exports.
3. Verify both scenarios against the live Make configuration and Airtable base.
4. Complete failure alerts, logging, recovery, and threshold configuration.
5. Complete OpenAI, Slack, and Calendly work according to approved scope.
6. Execute and document end-to-end MVP tests.
7. Review pilot readiness and outstanding risks.
8. Reassess n8n migration only when ADR-004 review criteria are met.

## 11. Completion criteria

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
