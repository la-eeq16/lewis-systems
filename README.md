# Lewis Systems

> Engineering Intelligent Business Systems

![Status](https://img.shields.io/badge/Status-Active%20Development-brightgreen)
![Product](https://img.shields.io/badge/Product-ClientPilot-blue)
![Version](https://img.shields.io/badge/Product-v0.3.0-orange)

Lewis Systems is a Cape Town, South Africa-based software and automation business that designs custom systems to help small businesses improve operations, manage information, and serve their customers more effectively.

The business combines client-specific automation services with the longer-term development of reusable software products. The objective is to generate revenue through practical client solutions while building repeatable capabilities and products over time.

## Flagship product: ClientPilot

ClientPilot is an AI-enabled client intake and lead qualification platform. It is being developed initially for small accounting firms in South Africa.

The intended journey is:

1. Capture a prospective client's enquiry.
2. Validate the submitted information.
3. Create or update the relevant company, contact, and lead records.
4. Evaluate and qualify the lead.
5. Communicate the outcome and support consultation booking.
6. Maintain an auditable CRM record of the process.

The initial target market is deliberately narrower than the wider Lewis Systems service market. ClientPilot will be validated with small accounting firms before expansion to other service industries is considered.

## Current development status

| Area | Current position |
| --- | --- |
| Product version | v0.3.0 |
| Development phase | Phase 3 – MVP implementation |
| Current module | Module 3 – Workflow automation |
| CRM and intake foundation | Documented as complete |
| Workflow platform | Make for the MVP |
| Qualification | Rule-based scoring in WF-001B; AI evaluation planned |
| n8n | Future migration option, not the current implementation |
| Notifications and scheduling | Slack and further Calendly automation planned |
| End-to-end validation | Pending |

### Current workflow

WF-001 is split into two Make scenarios:

- **WF-001A – Client Intake:** captures the form response, validates required information, and creates or updates CRM records.
- **WF-001B – Lead Qualification:** applies rule-based scoring and updates the lead qualification outcome.

The project documentation records both scenarios as built and tested. The Make blueprint exports and implementation evidence still need to be committed to this repository. See [ADR-004](docs/adr/ADR-004-make-automation-platform.md) for the platform decision.

## Technology

| Concern | Current / planned technology |
| --- | --- |
| CRM and data store | Airtable |
| Intake form | Google Forms |
| Response capture | Google Sheets |
| MVP automation | Make |
| AI evaluation | OpenAI (planned) |
| Email | Gmail |
| Notifications | Slack (planned) |
| Consultation scheduling | Calendly |
| Future automation option | n8n |
| Development and version control | JavaScript, Visual Studio Code, Git, GitHub |

The business workflow and data model should remain as platform-independent as practical. Make is the selected MVP execution platform; n8n is a possible later migration, not a parallel implementation requirement.

## Repository structure

This tree reflects the directories currently present on the remote `main` branch. Some directories contain planned or incomplete assets.

```text
lewis-systems/
├── .github/
├── api/
├── assets/
│   ├── branding/
│   └── diagrams/
├── database/
│   ├── airtable/
│   ├── sample-data/
│   └── schema/
├── docs/
│   ├── adr/
│   ├── modules/
│   │   ├── module-01-crm-database/
│   │   ├── module-02-google-forms/
│   │   └── module-03-n8n/       # legacy platform-specific documentation
│   └── numbered project documents
├── integrations/
├── journal/
│   └── 2026/
├── prompts/
├── scripts/
├── templates/
└── README.md
```

The Module 3 directory name is a known documentation-structure issue. The planned restructuring is to use a platform-neutral workflow-automation module with separate Make and n8n areas. Until that migration is completed, the existing directory is retained for traceability and should not be interpreted as proof that n8n is the active platform.

## Engineering principles

- Business requirements before tool selection.
- Documentation alongside implementation.
- Modular, reusable, and maintainable design.
- Data integrity and traceability.
- Security and privacy by design.
- Test before declaring a feature complete.
- Version-control implementation changes and relevant workflow exports.

A feature is not considered complete solely because its documentation or placeholder file exists. Its implementation, testing evidence, and repository record must agree.

## Development lifecycle

```text
Requirements → Design → Build → Test → Document → Commit → Push
```

## Project documentation

Start with the [Project Documentation Index](docs/00-PROJECT-INDEX.md), then consult the [Master Project Document](docs/01-MASTER-PROJECT.md) and [Project Status](docs/13-PROJECT-STATUS.md).

## Repository visibility and rights

This GitHub repository is publicly visible. Public visibility does not by itself grant permission to reuse, modify, or distribute the contents. No open-source licence is currently granted by this README; the repository's licence file and legal notice should be completed and reviewed separately.

## Founder

**La-eeq Lewis**  
Founder – Lewis Systems  
Cape Town, South Africa

---

© Lewis Systems. All rights reserved.
