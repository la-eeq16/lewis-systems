# Module 3 – Decision Log

**Module:** 03 – n8n Workflow Automation

**Document Version:** 1.0

**Product Version:** 0.3.0

**Status:** 🚧 Active

**Company:** Lewis Systems

**Product:** ClientPilot

**Author:** La-eeq Lewis

**Phase:** Phase 3 – MVP Implementation

**Last Updated:** 05 August 2026

---

# 1. Purpose

This document records the key architectural and technical decisions made during the design and implementation of the ClientPilot automation platform.

The purpose of this log is to preserve the reasoning behind important decisions, ensuring consistency, maintainability, and informed future development.

---

# Decision 001

## Title

Use Google Forms for Client Intake

### Decision

Google Forms will serve as the primary client enquiry interface for the MVP.

### Reason

- Fast to implement
- No development cost
- Mobile friendly
- Reliable
- Easy for accounting firms to adopt

### Alternatives Considered

- Custom web form
- Typeform
- Jotform

### Outcome

Approved

---

# Decision 002

## Title

Use Google Sheets as an Intermediate Data Store

### Decision

All Google Form submissions will first be stored in Google Sheets before entering the automation workflow.

### Reason

- Maintains a complete record of submissions
- Simplifies troubleshooting
- Supports replay of failed workflows
- Allows manual verification

### Alternatives Considered

- Direct Google Forms trigger
- Webhook-only approach

### Outcome

Approved

---

# Decision 003

## Title

Use n8n as the Automation Platform

### Decision

n8n will orchestrate all ClientPilot workflows.

### Reason

- Open source
- Self-hostable
- Lower long-term cost
- Flexible integrations
- Visual workflow design

### Alternatives Considered

- Make
- Zapier
- Custom backend

### Outcome

Approved

---

# Decision 004

## Title

Use Airtable as the Initial CRM

### Decision

Airtable will act as the primary CRM database during MVP development.

### Reason

- Rapid implementation
- Relational capabilities
- Easy administration
- Excellent API support
- Suitable for MVP scale

### Alternatives Considered

- PostgreSQL
- Supabase
- MySQL

### Outcome

Approved

---

# Decision 005

## Title

Adopt Modular Workflow Architecture

### Decision

The automation platform will consist of multiple small workflows rather than one large workflow.

### Reason

- Easier maintenance
- Independent testing
- Better fault isolation
- Improved scalability
- Greater reusability

### Alternatives Considered

- Single monolithic workflow

### Outcome

Approved

---

# Decision 006

## Title

Separate Business and Technical Documentation

### Decision

Business documentation and technical implementation documentation will be maintained as separate documents.

### Reason

- Improves readability
- Simplifies maintenance
- Supports both business and technical audiences
- Reduces duplication

### Outcome

Approved

---

# Decision 007

## Title

Create Companies and Contacts Before Leads

### Decision

The workflow will always ensure Company and Contact records exist before creating a Lead.

### Reason

- Maintains CRM integrity
- Prevents orphaned leads
- Supports reporting
- Enables linked-record relationships

### Outcome

Approved

---

# Decision 008

## Title

Perform AI Qualification After Lead Creation

### Decision

OpenAI qualification will occur after the Lead has been created in Airtable.

### Reason

- Every enquiry is preserved
- AI failures do not result in lost leads
- Supports manual qualification if required
- Improves workflow resilience

### Alternatives Considered

- AI qualification before CRM creation

### Outcome

Approved

---

# Decision 009

## Title

Maintain Business IDs Alongside Airtable Record IDs

### Decision

ClientPilot will use business-friendly identifiers in addition to Airtable Record IDs.

### Reason

- Easier reporting
- Human-readable references
- Supports future database migration
- Simplifies external integrations

### Outcome

Approved

---

# Decision 010

## Title

Documentation-First Development

### Decision

Every module must be documented before implementation begins.

### Reason

- Reduces implementation errors
- Improves planning
- Ensures consistency
- Supports onboarding
- Aligns with Lewis Systems engineering principles

### Outcome

Approved

---

# Future Decisions

Additional architectural decisions will be documented as ClientPilot evolves.

Examples include:

- Hosting strategy
- Authentication
- Multi-tenancy
- Billing
- Customer portal
- API versioning
- Reporting architecture
- Mobile application

---

# Revision History

| Version | Date | Description |
|---------|------|-------------|
| 1.0 | 05 August 2026 | Initial decision log. |

---

© Lewis Systems. All rights reserved.