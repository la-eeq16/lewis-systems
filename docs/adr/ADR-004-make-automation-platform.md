# ADR-004 – Use Make as the Automation Platform for the MVP

**Status:** Accepted
**Date:** 03 November 2026
**Author:** La-eeq Lewis
**Product:** ClientPilot (Lewis Systems)
**Supersedes:** Module 3 Decision 003 (n8n) for MVP implementation

---

## Context

Module 3 was planned around n8n (see `docs/modules/module-03-n8n/DECISION-LOG.md`, Decision 003). During Phase 3 the WF-001 workflow was built on Make instead.

## Decision

WF-001 – Client Intake & Qualification is implemented on **Make** (EU1 region) for the MVP. The workflow logic, data model and Airtable CRM are unchanged. Only the execution platform differs.

## Reasons

- Native Google Sheets, Airtable and Gmail modules reduce build time.
- Built-in error handling (Break handler with automatic retries) and an execution history that stores incomplete runs.
- No server to host or maintain during the MVP.

## Consequences

- Workflow definitions live in Make, not in `workflows/` as n8n JSON. Canonical implementation records are maintained in `docs/modules/module-03-workflow-automation/make/`; the older Make note remains in the legacy folder for traceability.
- Make scenarios cannot be diffed in Git. Export blueprints to `workflows/make/` after every significant change.
- Make personal-Gmail connections cannot use restricted Google scopes, so email uses the `google-email` v4 "Send an Email" module.
- If the platform changes again, the business logic in `07-WORKFLOW-DESIGN.md` is the source of truth.

## Alternatives Considered

- **n8n** (original plan): more control and self-hosting, but more setup effort.
- **Zapier**: simpler, but weaker branching and error handling.

## Planned Review Point

Revisit this decision **after the first paying client goes live**, or earlier if any of these occur:

- A client requires their data to stay on infrastructure Lewis Systems controls.
- Make operation costs grow in line with lead volume (each lead uses roughly 15–25 operations across WF-001A and WF-001B).
- ClientPilot is deployed as a repeatable product per client and needs version-controlled workflows.

Migrating to n8n means rebuilding the scenarios, not migrating data. The Airtable data model, Google Form, scoring rules, email wording and `07-WORKFLOW-DESIGN.md` are platform-independent. To keep the move cheap:

- Keep the canonical WF-001A and WF-001B implementation records current as the step-by-step references.
- Export Make blueprints to `workflows/make/` after significant changes.
- Keep business rules (for example the qualification threshold) in the Airtable Settings table, not hard-coded in Make.
- Expect to rebuild the error handling (Break retries) in n8n's own error workflow.

The README and `04-SYSTEM-ARCHITECTURE.md` now identify Make as the MVP automation platform.

## Open Items

- Export and sanitise both Make scenarios into `workflows/make/`.
- Verify scenario IDs, schedules, modules, filters, formulas, mappings, and error handlers against the live Make account.
