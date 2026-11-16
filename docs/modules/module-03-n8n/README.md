# Legacy Module 3 – Earlier n8n Workflow Automation Design

<badge>LEGACY – NOT THE CURRENT MVP PLATFORM</badge>

**Document Version:** 1.1  
**Product Version:** 0.3.0  
**Status:** Archived reference  
**Last Updated:** 16 November 2026

## 1. Legacy notice

This directory contains earlier n8n-oriented design documents and workflow artefacts, plus the superseded `WF-001-MAKE-IMPLEMENTATION.md` record that documented the initial Make build. It is retained for historical reference and must not be interpreted as the current canonical ClientPilot implementation. The Make implementation details have been carried forward into the canonical Module 3 Make records.

**Make is the selected automation platform for the current MVP.** The canonical, platform-neutral Module 3 documentation is now located at [docs/modules/module-03-workflow-automation/README.md](../module-03-workflow-automation/README.md).

## 2. How to use this directory

- Treat documents here as historical design inputs, not verified current specifications.\n- The legacy Make implementation note is a historical source; use the canonical Make records for current documentation.
- Do not assume an n8n workflow is deployed or active.
- Review and selectively reuse useful concepts only after comparing them with the canonical workflow requirements.
- Do not use legacy n8n JSON exports as production workflows without inspection, sanitisation, and testing.
- Keep current Make implementation records in the canonical Module 3 directory.

## 3. Current references

- [Canonical Module 3](../module-03-workflow-automation/README.md)
- [Workflow Architecture](../module-03-workflow-automation/WORKFLOW-ARCHITECTURE.md)
- [Workflow Specifications](../module-03-workflow-automation/WORKFLOW-SPECIFICATIONS.md)
- [Field Mapping](../module-03-workflow-automation/FIELD-MAPPING.md)
- [Make WF-001A](../module-03-workflow-automation/make/WF-001A-CLIENT-INTAKE.md)
- [Make WF-001B](../module-03-workflow-automation/make/WF-001B-LEAD-QUALIFICATION.md)
- [n8n Future Migration Plan](../module-03-workflow-automation/n8n/MIGRATION-PLAN.md)

## 4. Legacy artefact handling

Before reusing any workflow JSON or technical note:
1. Inspect its nodes, credentials references, IDs, and active state.
2. Confirm whether it contains environment-specific identifiers or personal data.
3. Compare its behaviour with the current platform-independent specification.
4. Sanitise and test it in a non-production environment.
5. Record any adopted implementation in the canonical Module 3 documentation.

---

© Lewis Systems. All rights reserved.
