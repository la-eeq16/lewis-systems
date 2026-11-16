# ClientPilot Project Status

**Document Version:** 3.5  
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

The documents distinguish the wider Lewis Systems strategy (custom systems for small businesses) from ClientPilot's initial accounting-firm target market. Make is identified as the current MVP platform and n8n as a future option.

### Stage 2 – Architecture and engineering

Reviewed and updated:
- 02-PRODUCT-REQUIREMENTS.md
- 03-BUSINESS-REQUIREMENTS.md
- 04-SYSTEM-ARCHITECTURE.md
- 05-DATA-MODEL.md
- 06-DEVELOPMENT-STANDARDS.md
- 07-WORKFLOW-DESIGN.md

The updates clarify that the current qualification path is rule-based, not AI-driven; distinguish current MVP functionality from planned extensions; document the conceptual data model separately from the Airtable implementation; identify incomplete multi-tenancy; and describe WF-001A/WF-001B with exception and recovery requirements.

This was a documentation review. It did not independently verify the live Airtable base or Make scenarios.

### Stage 3 – Module 3 implementation documentation

Created the canonical platform-neutral directory:
`docs/modules/module-03-workflow-automation/`

New documents:
- README.md – module entry point and status conventions.
- WORKFLOW-ARCHITECTURE.md – current logical system architecture.
- WORKFLOW-SPECIFICATIONS.md – WF-001A and WF-001B behaviour and test requirements.
- FIELD-MAPPING.md – logical mapping baseline and verification gaps.
- make/WF-001A-CLIENT-INTAKE.md – Make intake implementation record.
- make/WF-001B-LEAD-QUALIFICATION.md – Make qualification implementation record.
- n8n/MIGRATION-PLAN.md – future migration criteria and approach.

The former `module-03-n8n` README now marks that directory as legacy and points to the canonical Module 3 documentation. Existing legacy files have been preserved rather than deleted.

The new implementation records are documentation templates populated with currently recorded project facts. They do not independently prove the live Make configuration.

## 4. Module status

| Module | Scope | Status |
| --- | --- | --- |
| 1 – CRM Database | Airtable CRM structure, relationships, views, and QA | Documented complete; live configuration verification remains advisable |
| 2 – Google Forms Client Intake | Form, response capture, validation, and field mapping | Documented complete |
| 3 – Workflow Automation | WF-001A intake and WF-001B qualification on Make | In progress; documentation created, exports and evidence outstanding |
| 4 – OpenAI Qualification | AI-assisted lead evaluation | Pending |
| 5 – Slack Notifications | Internal workflow notifications | Pending |
| 6 – Calendly Integration | Booking workflow and synchronisation | Pending |
| 7 – End-to-End MVP Testing | Integrated testing and acceptance | Pending |

## 5. Current workflow implementation

### 5.1 WF-001A – Client Intake (Make)

**Recorded status:** Built and tested, according to the project implementation record.

The scenario is intended to receive a form response, validate fields, find or create a company, find or create a contact, and create a linked lead.

Exact Make modules, router filters, Airtable mappings, error handlers, and observed test evidence remain to be captured from the live scenario or sanitised export.

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

The GitHub repository does not yet contain exported Make blueprints for WF-001A and WF-001B. Detailed scenario implementation records now exist, but their configuration tables and test evidence remain to be completed.

Required deliverables:
- Export and sanitise the WF-001A Make blueprint.
- Export and sanitise the WF-001B Make blueprint.
- Complete exact module, filter, formula, and field mappings.
- Record scenario versions and change history.
- Add test cases and representative, non-sensitive test evidence.
- Confirm exports contain no secrets, personal customer data, or unnecessary environment-specific identifiers.

## 6. Current sprint – Sprint 2: Workflow Automation

| Task | Status |
| --- | --- |
| Stage 1 project foundation documentation | Complete |
| Stage 2 architecture and engineering documentation review | Complete |
| Stage 3 canonical Module 3 documentation | Complete |
| WF-001A client intake scenario | Built and tested, per project record |
| WF-001B rule-based qualification scenario | Built and tested, per project record |
| Make implementation records | Created; exact configuration details outstanding |
| Sanitised Make blueprint exports | Outstanding |
| Verify live Airtable fields and linked relationships | Outstanding |
| Verify score mappings and boundary cases | Outstanding |
| Administrator failure alert | Outstanding |
| Settings-driven qualification threshold | Outstanding |
| Workflow logging and recovery verification | Outstanding |
| End-to-end regression testing | Pending |

## 7. Architecture decision: Make and n8n

Make is the selected automation platform for the MVP. A future migration to n8n may be considered after the first paying client or earlier if a concrete cost, control, hosting, or client requirement justifies it.

The workflow design and business rules remain the platform-independent reference. See [ADR-004](adr/ADR-004-make-automation-platform.md).

The canonical Module 3 documentation is in `modules/module-03-workflow-automation/`. The former `module-03-n8n` directory is retained as legacy reference material and is not the current execution platform.

## 8. Risks and controls

| Risk | Control / next action |
| --- | --- |
| Make blueprint exports are absent from GitHub | Export, sanitise, document, and commit both scenarios |
| Live configuration may differ from documentation | Recheck Make and Airtable configuration during implementation verification |
| Qualification thresholds may be hard-coded or inconsistent | Verify source of truth and test boundary values |
| Workflow failures may go unnoticed | Complete administrator alerts, logging, and recovery tests |
| Legacy n8n documentation may cause confusion | Legacy notice added; preserve old files as reference |
| Customer information or credentials could be exposed | Use synthetic test data and sanitise exports before committing |
| Documentation may overstate completion | Require implementation and test evidence before closing tasks |

## 9. Next milestones

1. Export and sanitise Make WF-001A and WF-001B blueprints.
2. Complete exact module-level implementation and field mappings.
3. Verify both scenarios against the live Make configuration and Airtable base.
4. Complete failure alerts, logging, idempotency, and recovery checks.
5. Run and record end-to-end regression tests.
6. Reassess readiness for a controlled pilot.

---

© Lewis Systems. All rights reserved.
