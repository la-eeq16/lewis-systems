# Module 3 – n8n Workflow Automation

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

This module implements the automation layer of ClientPilot using n8n.

The workflow automates the processing of client enquiries received through Google Forms, synchronises data with Airtable, performs AI-powered lead qualification, and triggers notifications and scheduling workflows.

The automation layer serves as the central orchestration engine connecting all external services used by ClientPilot.

---

# 2. Overview

The n8n Workflow Automation module coordinates the complete client intake process by integrating:

- Google Forms
- Google Sheets
- Airtable
- OpenAI
- Slack
- Calendly

The workflow transforms manual client intake into a fully automated process while maintaining data integrity, traceability, and scalability.

---

# 3. Objectives

This module aims to:

- Automate client intake.
- Validate incoming enquiries.
- Synchronise data with the CRM.
- Prevent duplicate company and contact records.
- Create new lead records.
- Prepare leads for AI qualification.
- Notify internal staff.
- Support consultation scheduling.
- Maintain workflow execution logs.

---

# 4. Scope

The module includes:

- Google Sheets trigger
- Data validation
- Company lookup
- Contact lookup
- Lead creation
- AI qualification preparation
- Slack notifications
- Calendly preparation
- Error handling
- Workflow logging

---

# 5. Technology Stack

## Automation Platform

- n8n

## Integrated Services

- Google Forms
- Google Sheets
- Airtable
- OpenAI
- Slack
- Calendly

---

# 6. Workflow Architecture

The automation layer is divided into multiple workflows.

| Workflow | Purpose |
|----------|---------|
| Workflow 1 | Client Intake |
| Workflow 2 | CRM Processing |
| Workflow 3 | AI Qualification |
| Workflow 4 | Notifications |
| Workflow 5 | Scheduling |

This modular architecture improves maintainability, testing, and scalability.

---

# 7. Dependencies

This module depends on:

- Module 1 – CRM Database
- Module 2 – Google Forms Client Intake

Future modules depending on this implementation include:

- Module 4 – OpenAI Qualification Engine
- Module 5 – Slack Integration
- Module 6 – Calendly Integration
- Module 7 – End-to-End MVP Testing

---

# 8. Module Deliverables

The completed module will include:

- Workflow Architecture
- Node Specifications
- Field Mapping
- Workflow JSON exports
- QA Report
- Implementation Notes

---

# 9. Module Status

| Deliverable | Status |
|-------------|--------|
| README | ✅ Complete |
| Workflow Specification | ⏳ Pending |
| Workflow Architecture | ⏳ Pending |
| Node Specifications | ⏳ Pending |
| Field Mapping | ⏳ Pending |
| Implementation Plan | ⏳ Pending |
| QA Report | ⏳ Pending |
| Implementation Notes | ⏳ Pending |
| n8n Workflow | ⏳ Pending |

---

# 10. Expected Outcome

When complete, this module will provide a fully automated client intake pipeline capable of:

- Receiving Google Form submissions.
- Processing client information.
- Updating the Airtable CRM.
- Preparing AI lead qualification.
- Sending notifications.
- Initiating consultation scheduling.

---

# 11. Next Document

The next document in this module is:

**SPECIFICATION.md**

This document defines the technical requirements, workflow standards, integration rules, and implementation approach for the ClientPilot automation layer.

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| 1.0 | 05 August 2026 | Initial n8n Workflow Automation README. |

---

© Lewis Systems. All rights reserved.