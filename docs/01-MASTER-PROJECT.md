# Lewis Systems – Master Project Document

**Document Version:** 3.2  
**Product Version:** 0.3.0  
**Status:** Active Development  
**Company:** Lewis Systems  
**Product:** ClientPilot  
**Author:** La-eeq Lewis  
**Last Updated:** 16 November 2026

---

## 1. Purpose

This document is the high-level reference for Lewis Systems and its flagship product, ClientPilot. It separates the wider company's business strategy from the specific product scope and records the current development direction.

The Project Status document tracks day-to-day implementation progress. The Project Index provides navigation to the engineering documentation.

## 2. About Lewis Systems

Lewis Systems is a software and automation business based in Cape Town, South Africa. It develops custom systems that help small businesses improve how they capture information, manage operations, communicate with customers, and deliver services.

The business has two complementary objectives:

1. Deliver tailored systems and automation services to generate revenue and solve real client problems.
2. Turn repeatable capabilities and validated solutions into reusable products over time.

The initial market is small businesses broadly. Solutions are customised to the client's business process, constraints, and operational needs rather than forcing every client into one generic package.

## 3. Vision

Build a trusted South African provider of practical, intelligent business systems for small businesses, and develop reusable products from proven client needs.

## 4. Mission

Design and deliver reliable, useful systems that reduce manual work, improve operational visibility, and help businesses operate more effectively.

## 5. Operating principles

- **Business first:** understand the problem before selecting technology.
- **Documentation first:** record requirements, decisions, implementation, and tests.
- **Practical delivery:** favour solutions that can be maintained and afforded by the client.
- **Modularity:** separate responsibilities so components can evolve independently.
- **Reusability:** identify common patterns without ignoring client-specific requirements.
- **Reliability:** validate inputs, handle failures, and maintain traceability.
- **Security and privacy:** protect credentials and customer information.
- **Continuous learning:** review outcomes and improve the delivery process.

## 6. Business model and service direction

Lewis Systems uses a custom-solution service model. Potential work may include business process automation, client intake, CRM setup, lead management, notifications, reporting, and integrations.

The business should initially prioritise feasible projects that can be delivered with low operating costs and validated with real small-business clients. Reusable components can be developed where repeated client needs justify them.

The company-wide target market should not be confused with the initial target market of an individual product.

## 7. Flagship product: ClientPilot

ClientPilot is an AI-enabled client intake and lead qualification platform.

Its purpose is to streamline the journey from a prospective client's first enquiry to a qualified lead and consultation opportunity. The system combines an intake form, CRM records, workflow automation, qualification rules, communication, and scheduling capabilities.

### 7.1 Initial target customer

The first ClientPilot release targets small accounting firms in South Africa. This focused initial market allows the product's intake fields, qualification rules, and service workflows to be validated against a specific operating context.

Expansion into other service industries should follow evidence from pilot use and customer feedback, not be assumed as part of the initial release.

### 7.2 Core business problem

Small firms can lose time and opportunities through manual enquiry handling, slow responses, inconsistent qualification, fragmented customer information, and limited visibility over prospective clients.

### 7.3 Intended outcomes

- Capture enquiries consistently.
- Reduce repetitive data entry.
- Maintain linked company, contact, and lead records.
- Apply transparent qualification rules.
- Improve response and follow-up processes.
- Support consultation booking.
- Retain a traceable record of workflow activity.

## 8. Product scope and boundaries

ClientPilot's initial scope centres on client intake, CRM record management, rule-based lead qualification, and the foundations for communication and consultation scheduling.

AI evaluation, Slack notifications, expanded Calendly automation, and end-to-end MVP acceptance testing remain planned work unless the Project Status document records otherwise.

ClientPilot should not be described as a fully autonomous or production-ready platform until the relevant integrations, safeguards, and end-to-end tests have been completed.

## 9. Technology strategy

| Layer | MVP / current choice | Future consideration |
| --- | --- | --- |
| CRM and data | Airtable | Reassess as scale and client requirements evolve |
| Intake | Google Forms | Custom intake interface if justified |
| Response capture | Google Sheets | Alternative event-driven intake |
| Workflow automation | Make | n8n migration may be evaluated later |
| AI | OpenAI planned | Model/provider choice based on cost and performance |
| Email | Gmail | Additional email providers if required |
| Notifications | Slack planned | Client-specific communication channels |
| Scheduling | Calendly | Deeper booking integration |
| Development | JavaScript, Visual Studio Code | Expand engineering stack as needed |
| Version control | Git and GitHub | Continue version-controlled delivery |

### 9.1 Automation platform decision

Make is the selected execution platform for the current MVP. n8n is a future migration option, not the active platform for the current workflow.

The business rules, data structures, and workflow specifications should be documented independently of Make so that a future migration does not require redesigning the product's underlying business logic.

See [ADR-004](adr/ADR-004-make-automation-platform.md).

## 10. Current implementation overview

| Component | Current position |
| --- | --- |
| Module 1 – CRM Database | Documented complete |
| Module 2 – Google Forms Client Intake | Documented complete |
| Module 3 – Workflow Automation | In progress; WF-001A and WF-001B on Make |
| Module 4 – OpenAI Qualification | Planned |
| Module 5 – Slack Notifications | Planned |
| Module 6 – Calendly Integration | Planned |
| Module 7 – End-to-End MVP Testing | Planned |

WF-001A handles client intake and CRM record creation or updates. WF-001B applies rule-based lead scoring and updates the qualification outcome. The project records both scenarios as built and tested; the exported Make blueprints and implementation evidence still need to be committed to the repository.

For the authoritative task-level status and outstanding work, see [13-PROJECT-STATUS.md](13-PROJECT-STATUS.md).

## 11. Development lifecycle

```text
Discover → Specify → Design → Build → Test → Document → Commit → Push
```

A feature is not complete merely because it has been designed or described. Completion requires implementation, appropriate testing, updated documentation, and a version-controlled record.

## 12. Versioning and documentation governance

- Product version and document version are separate.
- Product version changes should follow the project's release/versioning policy.
- Each material document change should update its document version, date, and revision history where the document maintains one.
- The Project Index should reflect actual files and their real state.
- The Project Status document should be updated when implementation progress changes.
- Architecture decisions should be recorded in ADRs, including the context, decision, alternatives, and consequences.

## 13. Immediate project priorities

1. Complete and harden the current Make workflows.
2. Commit sanitised Make blueprint exports and detailed implementation documentation.
3. Add the planned administrator failure alert and improve operational error handling.
4. Complete the qualification rules and verify their configuration against the CRM.
5. Plan and implement the remaining AI, notification, and scheduling capabilities.
6. Perform end-to-end MVP testing before pilot use.
7. Reassess the automation platform only when there is a clear business or technical reason.

---

© Lewis Systems. All rights reserved.
