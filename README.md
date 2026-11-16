# Lewis Systems

> Engineering Intelligent Business Systems

![Status](https://img.shields.io/badge/Status-Active%20Development-brightgreen)
![Product](https://img.shields.io/badge/Product-ClientPilot-blue)
![Version](https://img.shields.io/badge/Product-v0.3.0-orange)

Lewis Systems is a Cape Town, South Africa-based software and automation business that designs custom systems to help small businesses improve operations, manage information, and serve their customers more effectively.

The business combines client-specific automation services with the longer-term development of reusable software products.

## Flagship product: ClientPilot

ClientPilot is an AI-enabled client intake and lead qualification platform being developed initially for small accounting firms in South Africa. The current MVP uses deterministic, rule-based qualification; AI-assisted evaluation is planned.

The intended journey is to capture an enquiry, validate the information, create or update CRM records, qualify the lead, communicate the outcome, support consultation booking, and retain an auditable CRM history.

The initial ClientPilot market is deliberately narrower than the wider Lewis Systems service market. ClientPilot will be validated with small accounting firms before expansion is considered.

## Current development status

| Area | Current position |
| --- | --- |
| Product version | v0.3.0 |
| Development phase | Phase 3 – MVP implementation |
| Current module | Module 3 – Workflow automation |
| CRM and intake foundation | Documented as complete; live configuration verification remains advisable |
| Workflow platform | Make for the MVP |
| Qualification | Rule-based scoring in WF-001B; AI evaluation planned |
| n8n | Future migration option; legacy artefacts retained separately |
| Notifications and scheduling | Gmail outcome emails documented; Slack and Calendly event synchronisation planned |
| End-to-end validation | Pending |

### Current workflows

- **WF-001A – Client Intake:** receives a form response, validates required fields, and creates or updates Company, Contact, and Lead records.
- **WF-001B – Lead Qualification:** applies rule-based scoring, updates the Lead, records a Qualification, and follows the configured outcome path.

The implementation record dated 03 November 2026 documents both scenarios as built and tested, including three sample qualification outcomes. The live Make scenarios have not been independently re-verified during this repository audit. **Sanitised Make blueprint exports are not yet present.**

See [ADR-004](docs/adr/ADR-004-make-automation-platform.md) and the [canonical Module 3 documentation](docs/modules/module-03-workflow-automation/README.md).

## Technology

| Concern | Current / planned technology |
| --- | --- |
| CRM and data store | Airtable |
| Intake form | Google Forms |
| Response capture | Google Sheets |
| MVP automation | Make |
| Prospect email | Gmail via configured Make email module |
| Booking hand-off | Calendly booking link |
| AI evaluation | OpenAI (planned) |
| Internal notifications | Slack (planned) |
| Future automation option | n8n |
| Development and version control | JavaScript, Visual Studio Code, Git, GitHub |

## Repository structure

This is a simplified view of the current remote `main` branch. Some files remain planned placeholders; see the [Repository Quality Audit](docs/19-REPOSITORY-QUALITY-AUDIT.md).

```text
lewis-systems/
├── .github/                  # GitHub contribution templates
├── api/                      # Service API notes
├── assets/                   # Branding and diagrams
├── database/                 # Airtable schema and sample data
├── docs/
│   ├── adr/                  # Architecture Decision Records
│   ├── modules/
│   │   ├── module-01-crm-database/
│   │   ├── module-02-google-forms/
│   │   ├── module-03-workflow-automation/
│   │   │   ├── make/         # Current MVP implementation records
│   │   │   └── n8n/          # Future migration plan
│   │   └── module-03-n8n/    # Legacy n8n reference material
│   └── numbered project documents
├── integrations/
├── journal/
├── prompts/
├── scripts/
├── templates/
├── workflows/
│   └── make/                 # Sanitised exports (not yet supplied)
├── .gitignore
├── CONTRIBUTING.md
└── README.md
```

## Engineering principles

- Business requirements before tool selection.
- Documentation alongside implementation.
- Modular, reusable, and maintainable design.
- Data integrity and traceability.
- Security and privacy by design.
- Test before declaring a feature complete.
- Version-control implementation changes and sanitised workflow exports.

A feature is not complete solely because its documentation or placeholder file exists. Implementation, testing evidence, and repository records must agree.

## Development lifecycle

```text
Requirements → Design → Build → Test → Document → Commit → Push
```

## Project documentation

Start with the [Project Documentation Index](docs/00-PROJECT-INDEX.md), [Master Project Document](docs/01-MASTER-PROJECT.md), and [Project Status](docs/13-PROJECT-STATUS.md).

For repository rules, see [Contributing](CONTRIBUTING.md), [Security](docs/16-SECURITY.md), and [Repository Quality Audit](docs/19-REPOSITORY-QUALITY-AUDIT.md).

## Repository visibility and rights

This repository is publicly visible. Public visibility does not itself grant permission to reuse, modify, or distribute its contents. The root `LICENSE` file is currently empty, so no open-source licence has been selected or granted. Review and add an appropriate licence before inviting external reuse.

## Founder

**La-eeq Lewis**  
Founder – Lewis Systems  
Cape Town, South Africa

---

© Lewis Systems. All rights reserved.
