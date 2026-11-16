# Module 3 – Workflow Automation

**Document Version:** 1.0  
**Product Version:** 0.3.0  
**Status:** In Progress  
**Company:** Lewis Systems  
**Product:** ClientPilot  
**Author:** La-eeq Lewis  
**Last Updated:** 16 November 2026

## 1. Purpose

Module 3 defines and documents the automation layer that connects ClientPilot intake, CRM records, lead qualification, communications, and consultation hand-off.

The module is platform-neutral at the requirements and workflow-design level. **Make is the selected execution platform for the current MVP.** n8n is retained as a possible future migration option, not the current production platform.

## 2. Canonical documents

| Document | Purpose |
|---|---|
| [Workflow Architecture](WORKFLOW-ARCHITECTURE.md) | System boundaries, components, and data flow |
| [Workflow Specifications](WORKFLOW-SPECIFICATIONS.md) | Expected behaviour, triggers, paths, and outcomes |
| [Field Mapping](FIELD-MAPPING.md) | Logical source-to-destination mapping and verification status |
| [Make implementation – WF-001A](make/WF-001A-CLIENT-INTAKE.md) | Intake scenario implementation record |
| [Make implementation – WF-001B](make/WF-001B-LEAD-QUALIFICATION.md) | Rule-based qualification implementation record |
| [n8n migration plan](n8n/MIGRATION-PLAN.md) | Conditions and controls for a future migration |

The platform-independent design in [docs/07-WORKFLOW-DESIGN.md](../../07-WORKFLOW-DESIGN.md) remains the governing workflow behaviour reference.

## 3. Current workflow scope

- **WF-001A – Client Intake:** receive a form response, validate required data, find or create Company and Contact records, and create a Lead.
- **WF-001B – Lead Qualification:** retrieve an eligible Lead, calculate rule-based component scores, determine the qualification outcome, and record the result.

The project status record describes these Make scenarios as built and tested. This repository does not yet contain the exported Make blueprints needed to independently verify their exact modules, filters, formulas, mappings, and error handlers.

## 4. Status conventions

- **Recorded:** stated in the project implementation record, but not independently verified from an export.
- **Documented:** described in repository documentation.
- **Verified:** checked against the live scenario or sanitised export and supported by evidence.
- **Planned:** not implemented or not confirmed.
- **Blocked:** requires an external input or decision.

Do not change a Recorded item to Verified without checking the live Make scenario or its export.

## 5. Security

Never commit API keys, access tokens, OAuth credentials, private customer data, or unredacted connection metadata. Use synthetic examples in documentation and tests. Sanitise scenario exports before committing.

## 6. Completion criteria

Module 3 can be closed only when both workflows have versioned, sanitised exports; exact module and field mappings; documented exception and recovery behaviour; and recorded test evidence. See [07-WORKFLOW-DESIGN.md](../../07-WORKFLOW-DESIGN.md).

---

© Lewis Systems. All rights reserved.
