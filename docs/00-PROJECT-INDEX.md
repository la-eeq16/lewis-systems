# ClientPilot Project Documentation Index

**Document Version:** 3.5  
**Product Version:** 0.3.0  
**Status:** Active Development  
**Company:** Lewis Systems  
**Product:** ClientPilot  
**Author:** La-eeq Lewis  
**Last Updated:** 16 November 2026

---

## 1. Purpose

This index is the navigation and governance entry point for ClientPilot's engineering documentation. It identifies the purpose and current state of each document and points contributors to the appropriate implementation records.

A listed document must not be treated as complete merely because a file has been created.

## 2. Core project documents

| No. | Document | Purpose | Current state |
| :-: | --- | --- | --- |
| 00 | [Project Index](00-PROJECT-INDEX.md) | Documentation navigation and governance | Maintained |
| 01 | [Master Project](01-MASTER-PROJECT.md) | Company, product, strategy, and project overview | Maintained |
| 02 | [Product Requirements](02-PRODUCT-REQUIREMENTS.md) | Product scope, users, requirements, and outcomes | Reviewed and aligned to MVP |
| 03 | [Business Requirements](03-BUSINESS-REQUIREMENTS.md) | Business problem, objectives, and requirements | Reviewed and aligned to business strategy |
| 04 | [System Architecture](04-SYSTEM-ARCHITECTURE.md) | System components, boundaries, and integrations | Reviewed; Make rule-based MVP clarified |
| 05 | [Data Model](05-DATA-MODEL.md) | CRM entities, fields, and relationships | Reviewed; implementation gaps made explicit |
| 06 | [Development Standards](06-DEVELOPMENT-STANDARDS.md) | Engineering and documentation practices | Reviewed and updated |
| 07 | [Workflow Design](07-WORKFLOW-DESIGN.md) | Platform-independent workflow behaviour | Reviewed; Make scenarios and exceptions clarified |
| 08 | [AI Prompts](08-AI-PROMPTS.md) | Prompt inventory and prompt standards | Existing; review when AI module begins |
| 09 | [API Integrations](09-API-INTEGRATIONS.md) | External service integration specifications | Existing; completeness to verify |
| 10 | [Testing](10-TESTING.md) | Test strategy, cases, and QA evidence | Existing; evidence to verify |
| 11 | [Roadmap](11-ROADMAP.md) | Planned milestones and sequencing | Existing; align with status |
| 12 | [Changelog](12-CHANGELOG.md) | Project change history | Maintained |
| 13 | [Project Status](13-PROJECT-STATUS.md) | Current milestones, sprint, and blockers | Maintained |\n| 19 | [Repository Quality Audit](19-REPOSITORY-QUALITY-AUDIT.md) | Repository hygiene findings and corrective actions | Stage 4 reviewed; outstanding actions remain |

## 3. Supporting documentation

| Location | Purpose | Current state |
| --- | --- | --- |
| `adr/` | Architecture Decision Records | ADR-004 records Make for the MVP |
| `modules/module-01-crm-database/` | CRM implementation documentation | Existing; verify against Airtable |
| `modules/module-02-google-forms/` | Intake form documentation | Existing; verify against live form |
| [modules/module-03-workflow-automation/](modules/module-03-workflow-automation/README.md) | Canonical platform-neutral workflow module, Make implementation, and n8n migration plan | Current; Make exports outstanding |
| `modules/module-03-n8n/` | Earlier n8n design and workflow artefacts | Legacy reference; not the current execution platform |
| `api/` | Service-specific API notes | Completeness to verify |
| `database/` | Airtable tables, sample data, and schema references | Completeness to verify |
| `integrations/` | Integration-specific implementation notes | Completeness to verify |
| `prompts/` | Prompt assets | Completeness to verify |
| `scripts/` | Utility scripts | Completeness to verify |
| `templates/` | Reusable documentation templates | Completeness to verify |
| `assets/` | Branding, diagrams, and other assets | Completeness to verify |
| `journal/2026/` | Development journal | Ongoing |

## 4. Implementation modules

| Module | Scope | Status |
| --- | --- | --- |
| 1 – CRM Database | Airtable CRM entities, relationships, views, and QA | Documented complete; live configuration should be periodically verified |
| 2 – Google Forms Client Intake | Form, response capture, validation, and field mapping | Documented complete |
| 3 – Workflow Automation | WF-001A intake and WF-001B rule-based qualification on Make | In progress; canonical documentation created, exports and evidence outstanding |
| 4 – OpenAI Qualification | AI-assisted evaluation | Planned |
| 5 – Slack Notifications | Internal notifications | Planned |
| 6 – Calendly Integration | Booking workflow and synchronisation | Planned |
| 7 – End-to-End MVP Testing | Integrated acceptance and regression testing | Planned |

## 5. Current automation decision

Make is the selected automation platform for the ClientPilot MVP. n8n is a possible future migration target. Workflow requirements, business rules, CRM data definitions, and expected outcomes should remain independent of the execution platform wherever practical.

See [ADR-004 – Make as the MVP Automation Platform](adr/ADR-004-make-automation-platform.md).

The current Make scenarios are:
- **WF-001A – Client Intake**
- **WF-001B – Lead Qualification (rule-based)**

The project records these scenarios as built and tested. Their exported Make blueprints and complete implementation evidence are not yet present in the repository and remain outstanding version-control deliverables.

## 6. Documentation status definitions

| Status | Meaning |
| --- | --- |
| Maintained | Reviewed and used as a current project reference |
| Reviewed | Recently checked and aligned to current scope; further implementation verification may remain |
| Existing; review | A document exists, but its completeness or alignment still needs review |
| Planned | Work has not yet been completed |
| Legacy | Retained for history or reference; not the current implementation |
| Complete | Deliverable has been implemented and its required testing/evidence has been recorded |

Do not use “complete” to describe empty placeholders, unverified configurations, or documents that only describe intended future behaviour.

## 7. Engineering lifecycle

```text
Requirements
    ↓
Design
    ↓
Build
    ↓
Test
    ↓
Document
    ↓
Git Commit
    ↓
Git Push
```

A module can be marked complete only when its scope, implementation, tests, documentation, and version-control records are consistent.

## 8. Repository quality\n\nSee [19-REPOSITORY-QUALITY-AUDIT.md](19-REPOSITORY-QUALITY-AUDIT.md) for the 16 November 2026 audit. It records 76 zero-byte files at audit time, the missing Make exports, legacy n8n artefacts, and repository hygiene corrections.\n\n## 9. Repository governance

- Keep this index aligned with the actual repository tree.
- Keep the Project Status document as the operational progress record.
- Record significant technology and architecture choices as ADRs.
- Record implementation details in the relevant module documentation.
- Keep credentials, access tokens, private customer data, and environment-specific secrets out of Git.
- Update document versions and revision history when material changes are made.
- Identify placeholders explicitly and avoid describing them as finished deliverables.

---

© Lewis Systems. All rights reserved.
