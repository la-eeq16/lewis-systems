# ClientPilot API and External Integrations

**Document Version:** 1.3  
**Product Version:** 0.3.0  
**Status:** Active – MVP integrations  
**Company:** Lewis Systems  
**Product:** ClientPilot  
**Author:** La-eeq Lewis  
**Last Updated:** 16 November 2026

---

## 1. Purpose

This document records the external services used by ClientPilot, their current MVP role, and their implementation status. A service being listed does not prove every planned endpoint or capability is implemented.

## 2. Integration principles

- Integrations must serve a defined business requirement.
- Use secure, least-privilege authentication.
- Validate inbound and outbound data.
- Handle transient and permanent failures appropriately.
- Prevent duplicate writes or messages on retries.
- Protect customer and personal information.
- Keep credentials out of source code and exported documentation.

## 3. Integration catalogue

| ID | Service | Current role | Status |
|---|---|---|---|
| API-001 | Google Forms | Prospect intake form | Current MVP |
| API-002 | Google Sheets | Form response capture | Current MVP |
| API-003 | Make | Workflow orchestration and rule-based qualification | Current MVP |
| API-004 | Airtable | Operational CRM datastore | Current MVP |
| API-005 | Gmail | Configured prospect outcome emails via Make | Recorded in workflow implementation note |
| API-006 | Calendly | Booking-link hand-off | Link hand-off recorded; event synchronisation planned |
| API-007 | OpenAI | AI-assisted qualification and meeting preparation | Planned |
| API-008 | Slack | Internal workflow notifications | Planned |
| API-009 | n8n | Possible future workflow platform | Migration option only |

## 4. Current MVP data flow

```text
Prospective client
    ↓
Google Forms
    ↓
Google Sheets
    ↓
Make – WF-001A
    ↓
Airtable – Company / Contact / Lead
    ↓
Make – WF-001B (rule-based qualification)
    ↓
Airtable – Lead / Qualification outcome
    ├── Configured Gmail outcome email
    └── Calendly booking-link hand-off for Qualified leads
```

OpenAI and Slack are not part of the current rule-based qualification path. Calendly event synchronisation is not assumed to be implemented. Sending a booking link is not proof of a confirmed appointment.

## 5. Service responsibilities

### Google Forms and Google Sheets
- Capture prospect and company information.
- Preserve form responses as the source submission.
- Validate required values downstream before CRM creation.
- Restrict access to response data.

### Make
- Execute WF-001A intake and WF-001B rule-based qualification.
- Keep workflow logic documented in the canonical Module 3 directory.
- Record failures and use safe retries where configured.
- Store connection credentials in Make's secure connection manager.
- Export sanitised scenario blueprints to `workflows/make/` after significant changes.

### Airtable
- Store Companies, Contacts, Leads, Qualifications, Meetings, Activities, Workflow Logs, and Settings.
- Preserve linked-record integrity.
- Restrict base access and protect personal data.
- Verify field types, linked-record relationships, and select options before changing mappings.

### Gmail
The 03 November 2026 Make implementation note records a qualified-lead booking email and a not-qualified follow-up email using Make's `google-email` v4 Send an Email module. It records that sending is skipped when Email Notifications Enabled is false or the Contact has no email. Confirm the current live configuration and delivery behaviour separately.

### Calendly
- Provide the configured booking URL to eligible prospects.
- Do not mark a Meeting confirmed solely because the URL was sent.
- Booking-event synchronisation and automatic Meeting status updates remain planned.

### OpenAI (planned)
- May provide a separate recommendation, summary, or assisted analysis.
- Must not silently override deterministic qualification without an approved policy.
- Requires prompt/version management, output validation, privacy review, and human-review rules.

### Slack (planned)
- Intended for internal workflow and failure notifications.
- Avoid unnecessary personal data in messages.
- Requires channel access controls and failure handling.

### n8n (future option)
n8n is not a current execution dependency. Reconsider only when the migration plan's business and operational prerequisites are met.

## 6. Security and error handling

- Never hard-code API keys, OAuth tokens, or personal access tokens.
- Use provider-managed connections or approved secret storage.
- Limit access to the minimum required permissions.
- Avoid placing personal information in unnecessary workflow logs or notifications.
- Retry only transient failures and guard against duplicate records or messages.
- Document manual recovery for failures requiring human intervention.

## 7. Authoritative implementation references

- [System Architecture](04-SYSTEM-ARCHITECTURE.md)
- [Workflow Design](07-WORKFLOW-DESIGN.md)
- [Module 3 – Workflow Automation](modules/module-03-workflow-automation/README.md)
- [ADR-004 – Make for the MVP](adr/ADR-004-make-automation-platform.md)

---

© Lewis Systems. All rights reserved.
