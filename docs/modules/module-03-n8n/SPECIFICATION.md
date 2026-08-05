# Module 3 – n8n Workflow Automation Specification

**Module:** 03 – n8n Workflow Automation

**Document Version:** 1.0

**Product Version:** 0.3.0

**Status:** 🚧 In Progress

**Company:** Lewis Systems

**Product:** ClientPilot

**Author:** La-eeq Lewis

**Phase:** Phase 3 – MVP Implementation

**Last Updated:** 05 August 2026

---

# 1. Purpose

This specification defines the automation layer of ClientPilot using n8n.

It establishes the architecture, technical requirements, workflow standards, integration rules, and implementation guidelines for all automation workflows within the ClientPilot MVP.

The n8n automation layer acts as the orchestration engine that connects all external systems used by ClientPilot.

---

# 2. Objectives

The automation layer is designed to:

- Process new client enquiries automatically.
- Validate incoming data.
- Synchronise information with the CRM.
- Prevent duplicate records.
- Prepare data for AI processing.
- Trigger business notifications.
- Initiate consultation scheduling.
- Record workflow execution for auditing.

---

# 3. Scope

This module covers the implementation of workflows integrating:

- Google Forms
- Google Sheets
- Airtable
- OpenAI
- Slack
- Calendly

---

# 4. Architecture Principles

The automation layer follows the Lewis Systems engineering principles:

- Documentation First
- Business First
- Modular Architecture
- Single Responsibility
- Error Resilience
- Scalability
- Maintainability
- Security by Design

---

# 5. Workflow Design Principles

Each workflow should:

- Perform one primary responsibility.
- Minimise dependencies on other workflows.
- Return clear success or failure results.
- Handle expected errors gracefully.
- Produce consistent outputs.
- Support future expansion.

---

# 6. Workflow Modules

The automation layer consists of five primary workflows.

| Workflow | Purpose |
|----------|---------|
| Workflow 1 | Client Intake |
| Workflow 2 | CRM Processing |
| Workflow 3 | AI Qualification |
| Workflow 4 | Notifications |
| Workflow 5 | Scheduling |

Each workflow can be developed, tested, and maintained independently.

---

# 7. Data Flow

The automation follows this sequence:

1. Client submits Google Form.
2. Google Sheets records the response.
3. n8n detects a new submission.
4. Submission is validated.
5. Company is located or created.
6. Contact is located or created.
7. Lead is created.
8. AI qualification is prepared.
9. Notifications are sent.
10. Scheduling is initiated if required.

---

# 8. Integration Standards

Each external platform has a defined responsibility.

| Platform | Responsibility |
|----------|----------------|
| Google Forms | Data collection |
| Google Sheets | Response storage |
| n8n | Workflow orchestration |
| Airtable | CRM database |
| OpenAI | Lead qualification |
| Slack | Team notifications |
| Calendly | Meeting scheduling |

---

# 9. Error Handling

All workflows should:

- Detect validation errors.
- Log failures.
- Prevent duplicate records.
- Continue processing where possible.
- Return meaningful error messages.

Critical failures should stop the workflow and generate a notification.

---

# 10. Logging

Every workflow execution should record:

- Workflow name
- Trigger time
- Execution status
- Processing duration
- Error details (if applicable)

Workflow history should be stored within the ClientPilot CRM.

---

# 11. Security

The automation layer must:

- Protect API credentials.
- Restrict workflow access.
- Use secure connections.
- Validate external input.
- Avoid exposing confidential client data.

---

# 12. Success Criteria

The module will be considered complete when:

- All workflows execute successfully.
- CRM data is synchronised correctly.
- Duplicate records are prevented.
- AI processing is triggered correctly.
- Notifications are delivered.
- Documentation is complete.
- QA validation passes.

---

# 13. Deliverables

The completed module will include:

- Workflow Architecture
- Node Specifications
- Field Mapping
- Workflow JSON exports
- QA Report
- Implementation Notes

---

# 14. Module Outcome

The completed automation layer will provide the first fully automated client intake pipeline for ClientPilot.

It will serve as the operational backbone connecting all external systems into a single, scalable workflow.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| 1.0 | 05 August 2026 | Initial workflow specification. |

---

© Lewis Systems. All rights reserved.