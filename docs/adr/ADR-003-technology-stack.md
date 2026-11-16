# ADR-003 – Technology Stack

**Status:** Accepted (automation platform amended by ADR-004)
**Date:** 04 August 2026 (documented 16 November 2026)
**Author:** La-eeq Lewis

## Decision

| Capability | Technology |
|------------|-----------|
| Development | Visual Studio Code, Git, GitHub, JavaScript |
| CRM | Airtable (PostgreSQL later) |
| Automation | n8n originally; **Make for the MVP** (ADR-004) |
| AI | OpenAI |
| Forms | Google Forms (responses in Google Sheets) |
| Scheduling | Calendly |
| Communication | Slack and Gmail |

## Reasons

Fast to implement, low cost, strong integrations, and suitable for MVP scale. Alternatives considered: custom web forms, PostgreSQL or Supabase, Zapier, a custom backend.

## Consequences

The stack is reviewed after the first paying client. Platform-specific logic must be documented so it can be rebuilt on another platform.
