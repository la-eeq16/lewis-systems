# ADR-002 – System Philosophy

**Status:** Accepted
**Date:** 04 August 2026 (documented 16 November 2026)
**Author:** La-eeq Lewis

## Context

Lewis Systems builds software for professional service firms and intends to build several automation systems over time. ClientPilot is the first.

## Decision

All systems follow these principles (see `docs/01-MASTER-PROJECT.md` and `docs/04-SYSTEM-ARCHITECTURE.md`):

- Business first, systems first: design capabilities before choosing tools.
- Technology independence: business engines and the data model are platform-independent.
- Modular design: one responsibility per engine, workflow and module.
- Documentation first: a module is complete only when requirements, design, build, test, documentation, commit and push are done.
- AI native and security by design.
- Business rules live in configuration (Airtable Settings), not hard-coded in automation platforms.

## Consequences

- Technologies can be replaced without redesigning the platform (for example Make → n8n, Airtable → PostgreSQL).
- Every change must update the relevant documents.
