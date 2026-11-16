# ClientPilot Changelog

All notable changes to the ClientPilot project will be documented in this file.

This project follows the principles of **Keep a Changelog** and **Semantic Versioning**.

---

# [Unreleased] - 16 November 2026\n\n## Repository Quality – Stage 4\n\n- Added root `.gitignore`, contribution guidance, security standards, and a pull request template.\n- Added `workflows/make/README.md` to define the location and sanitisation requirements for Make exports; actual exports remain outstanding.\n- Added the repository quality audit and corrected README, ADR-004, and integration catalogue references.\n- Sanitised spreadsheet, sheet, credential-reference, and instance metadata in the inactive legacy n8n workflow JSON.\n- Preserved empty placeholders pending owner review; no licence was selected.\n

## Added

### Module 3 – Workflow Automation (WF-001 on Make)

- Built WF-001A (Client Intake) and WF-001B (Lead Qualification) on Make.
- Intake validation: required fields, email format, industry and consent.
- Standard industry list (19 industries plus Other) shared by Airtable, the Google Form and Make.
- Rule-based qualification scoring (Qualified ≥ 64, Review Required 40–63, Not Qualified < 40).
- Qualified path: consultation Meeting (*Awaiting Booking*) and booking email. Not Qualified path: polite follow-up email.
- Workflow Logs, Activities and Break-handler retries (3 attempts, 10 minutes apart).
- Booking Link field in the Settings table.
- ADR-002, ADR-003 and ADR-004; Module 3 decision log entries 011–014.
- WF-001 Make implementation document.

## Changed

- Automation platform for the MVP changed from n8n to Make (ADR-004). A migration to n8n is planned after the first paying client.
- Documentation aligned across the repository: module statuses (Modules 1 and 2 complete, Module 3 in progress), product and document versions, field mappings (Module 1 table specifications, Module 2 and Module 3 field mappings), workflow structure (WF-001A/B), scoring and thresholds.
- Module 3 documents rewritten for the Make implementation.

## Fixed

- Retry Count 422 error in completion logs.
- Gmail connection error for personal Google accounts.

## Pending

- Administrator alert, Settings-driven threshold, Make blueprint export, AI evaluation, Slack notifications, Calendly integration.

---

# [0.3.0] - 05 August 2026

## Added

### Module 2 – Google Forms Client Intake

- Completed Module 2 of the ClientPilot MVP.
- Designed and implemented the ClientPilot client intake form.
- Created a professional five-section Google Form workflow.
- Configured required field validation.
- Configured email validation.
- Configured mobile number validation.
- Added custom confirmation message.
- Optimised the form for desktop and mobile devices.

### Google Forms Documentation

Completed the complete engineering documentation for Module 2:

- README
- Specification
- Field Mapping
- Implementation Plan
- QA Report
- Implementation Notes

### CRM Integration

- Mapped every Google Form field to the ClientPilot Airtable CRM.
- Verified compatibility with the ClientPilot Data Model.
- Prepared the form for workflow automation.
- Prepared the form for future OpenAI processing.

### Documentation

Updated:

- README
- Master Project
- Project Status
- Roadmap
- Project Index
- Repository documentation
- Google Forms module documentation

### Engineering Improvements

- Adopted a modular implementation strategy for the ClientPilot MVP.
- Standardised every implementation module to include:
  - README
  - Specification
  - Field Mapping
  - Implementation Plan
  - QA Report
  - Implementation Notes

### Quality Assurance

Completed validation of the Google Forms module, including:

- Form structure
- Required fields
- Email validation
- Mobile number validation
- User experience
- CRM compatibility
- Automation readiness

### Milestone

✅ Module 2 – Google Forms Client Intake completed.

### Next Milestone

- Begin Module 3 – Workflow Automation.
- Design the automation workflow architecture.
- Connect Google Forms to Airtable.
- Implement Company and Contact lookup.
- Create Lead automation.
- Prepare OpenAI qualification workflow.

---

# [0.2.0] - 03 August 2026

## Added

### CRM Database

- Completed ClientPilot CRM database implementation in Airtable.
- Built the eight operational CRM tables.
- Configured linked-record relationships across the CRM.
- Implemented standardized field naming conventions.
- Implemented business identifier standards across all entities.
- Created operational and filtered views for every CRM table.
- Performed quality assurance (QA) validation on every table.
- Validated relationships, field types, and implementation consistency.

### CRM Tables Completed

- Companies
- Contacts
- Leads
- Qualifications
- Meetings
- Activities
- Workflow Logs
- Settings

### Database Improvements

- Adopted Airtable Linked Records as the primary relationship mechanism.
- Preserved logical business identifiers (Company ID, Contact ID, Lead ID, etc.) for reporting, integrations, and future database migration.
- Added AI research fields to the Contacts table:
  - Research Full Name
  - Job Title
  - Employer
- Standardized linked-record, lookup, and computed fields across the CRM.

### Documentation

- Updated Data Model.
- Updated Project Status.
- Updated CRM implementation documentation.
- Documented Airtable implementation strategy.
- Documented CRM architecture refinements.

### Quality Assurance

Completed QA validation for:

- Companies
- Contacts
- Leads
- Qualifications
- Meetings
- Activities
- Workflow Logs
- Settings

Validation included:

- Field structure verification
- Relationship verification
- View validation
- Naming consistency
- Business rule validation

### Engineering Process

Continued following the Lewis Systems engineering lifecycle:

Requirements → Design → Build → Test → Document → Git Commit → Git Push

### Milestone

✅ Module 1 – CRM Database completed.

---

# [0.1.0] - 30 July 2026

## Added

### Foundation

- Project repository created.
- README completed.
- Product Requirements Document completed.
- Business Requirements Document completed.
- System Architecture completed.
- Data Model completed.
- Development Standards completed.
- Workflow Design completed.
- AI Prompt Library completed.
- API Integrations documented.
- Testing Strategy completed.
- Product Roadmap completed.
- Project Index created.
- Project Status documentation created.
- Changelog created.

### Repository

- GitHub repository initialized.
- Professional repository structure established.
- ADR directory created.
- Prompt library created.
- Template library created.

### Status

✅ Phase 1 – Foundation completed.

---