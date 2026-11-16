# Lewis Systems Development Standards

**Document Version:** 1.1  
**Applies To:** All Lewis Systems projects  
**Status:** Active  
**Company:** Lewis Systems  
**Author:** La-eeq Lewis  
**Last Updated:** 16 November 2026

---

## 1. Purpose and Scope

This document defines the minimum engineering, documentation, security, testing, and version-control practices for systems developed or maintained by Lewis Systems. It applies to custom client solutions, internal tools, automations, integrations, and reusable products such as ClientPilot.

## 2. Engineering Principles

- Understand the business problem before choosing technology.
- Design the workflow and data before implementation.
- Prefer simple, maintainable solutions over unnecessary complexity.
- Separate business rules from platform-specific implementation.
- Build reusable components where there is a demonstrated need.
- Use AI-assisted development with human review.
- Protect customer data and credentials.
- Test changes before declaring them complete.
- Document decisions and known limitations.

## 3. Delivery Lifecycle

```text
Discovery
   ↓
Business Requirements
   ↓
Product / Solution Requirements
   ↓
Architecture and Data Design
   ↓
Workflow / Technical Design
   ↓
Implementation
   ↓
Testing and Review
   ↓
Documentation Update
   ↓
Git Commit and Push
   ↓
Deployment / Handover
   ↓
Monitoring and Improvement
```

The lifecycle is iterative. Small changes may combine stages, but requirements, testing, documentation, and review must not be skipped.

## 4. Documentation Standards

Documents should include, where applicable:

- Document title and purpose.
- Document version and status.
- Product or project version.
- Owner / author.
- Last updated date.
- Scope and assumptions.
- Related documents.
- Revision history for documents with material ongoing changes.

Documentation must distinguish requirements, design proposals, current implementation, verified tests, and future plans. A file or heading existing in Git is not proof that the described feature is implemented.

## 5. Architecture and Design Standards

Systems should:

- Be modular, with clear component responsibilities.
- Separate business logic from vendor-specific configuration.
- Define inputs, outputs, ownership, and failure behaviour.
- Minimise unnecessary dependencies.
- Identify external service and trust boundaries.
- Consider portability and exit paths.
- Document significant decisions in ADRs.

## 6. Data Standards

- Define entities, attributes, identifiers, and relationships.
- Use stable identifiers where records cross system boundaries.
- Validate required fields and controlled values.
- Avoid unnecessary duplication of personal or business data.
- Define record ownership and access requirements.
- Preserve relevant audit history.
- Define retention and deletion expectations.
- Do not claim multi-tenant security until tenant isolation is implemented and tested.

## 7. Workflow and Automation Standards

Every workflow should have:

- A unique workflow identifier and clear purpose.
- A defined trigger and expected inputs.
- Documented steps, conditions, and outputs.
- Defined ownership of records and side effects.
- Validation and duplicate-prevention rules.
- Error handling and safe retry behaviour.
- Logging and operational monitoring appropriate to its risk.
- Test cases for normal, boundary, and failure conditions.
- A versioned implementation record and, where supported, an exported workflow definition.

Retries must be designed to avoid duplicate records, emails, bookings, or other side effects.

## 8. AI Standards

AI is optional and should be used only where it adds measurable value. Each AI capability must document:

- Purpose and use case.
- Model/provider and version where available.
- Prompt identifier and version.
- Inputs and data classification.
- Output schema and validation.
- Failure, timeout, and low-confidence behaviour.
- Human-review or override path.
- Evaluation cases and known limitations.

AI outputs must not be presented as verified facts without appropriate validation. AI should not silently override deterministic business rules unless an approved product decision explicitly defines that behaviour.

## 9. Coding and Configuration Standards

Code and configuration should be:

- Readable, consistent, modular, and maintainable.
- Named clearly and structured predictably.
- Reviewed for duplicated logic and unnecessary complexity.
- Validated for expected and invalid inputs.
- Free of committed secrets and unnecessary environment-specific identifiers.
- Accompanied by tests or documented manual verification appropriate to the change.

Keep environment-specific values in configuration or secure connection stores rather than hardcoding them into source.

## 10. Version Control Standards

- Git is the version-control system.
- GitHub is the project repository and review location.
- Use Conventional Commit-style messages where practical.

Examples:

```text
feat: add lead qualification workflow
fix: prevent duplicate contact creation
docs: update system architecture
refactor: simplify CRM mapping
test: add qualification boundary cases
chore: sanitise workflow export
```

- Commit focused, understandable changes.
- Do not commit credentials, tokens, private customer data, or raw production exports.
- Review diffs before pushing.
- Keep the main branch in a coherent state.
- Use feature branches when a change is substantial or risky.
- Tag releases when a version is formally released.

## 11. Branch and Release Strategy

- `main`: reviewed, coherent project baseline; not automatically proof of production deployment.
- `feature/<short-name>`: new functionality.
- `fix/<short-name>`: defect correction.
- `docs/<short-name>`: documentation-only work.
- `release/<version>`: optional release preparation.

Use pull requests for changes that benefit from review. Deployment and release status must be recorded separately from Git merge status.

## 12. Security and Privacy Standards

- Use least-privilege access.
- Store credentials in approved secret stores or provider-managed connections.
- Never commit API keys, OAuth tokens, passwords, or private connection secrets.
- Use synthetic or anonymised data in examples and tests.
- Minimise personal information in logs and notifications.
- Restrict customer data to authorised users and systems.
- Review third-party permissions and data flows.
- Define retention, deletion, and incident-response procedures for customer deployments.

If a secret is committed, removing it from the latest file is insufficient: revoke or rotate it and review repository history.

## 13. Testing and Quality Assurance

Select tests appropriate to the change:

- Unit or rule-level tests.
- Field mapping and validation tests.
- Integration tests.
- Workflow happy-path tests.
- Boundary and negative tests.
- Duplicate and retry tests.
- Regression tests.
- User acceptance tests.
- Security and privacy checks.

Record test date, environment, test data type, expected result, actual result, pass/fail, and known defects. Never use a test status that has not actually been observed.

## 14. Logging and Error Handling

Important events should be traceable, for example:

- Lead submitted.
- Lead created or updated.
- Qualification completed.
- Booking link sent.
- Booking confirmed.
- Notification sent.
- Workflow failed or recovered.

Errors should be classified where practical. Retry transient failures only when safe. Preserve enough context for troubleshooting without logging credentials or unnecessary personal data. Escalate failures requiring human intervention.

## 15. Definition of Done

A change is complete when all applicable criteria are satisfied:

- Requirements and scope are clear.
- Design and data impacts are reviewed.
- Implementation is present.
- Relevant normal, boundary, and failure tests pass.
- Security and privacy implications are reviewed.
- Documentation and known limitations are updated.
- Workflow exports or configuration evidence are stored safely where applicable.
- Changes are committed and pushed.
- The Project Status / changelog is updated when the change materially affects project progress.

A design-only task may be marked design-complete, but must not be labelled implementation-complete.

## 16. Technology Standards

Technology choices are project-specific and recorded in architecture documents and ADRs. For ClientPilot's current MVP:

- Workflow automation: Make.
- CRM: Airtable.
- Intake: Google Forms and Google Sheets.
- Email: Gmail.
- Booking hand-off: Calendly.
- AI: OpenAI planned, not part of the current rule-based qualification path.
- Version control: Git and GitHub.
- Development environment: Visual Studio Code.

n8n is a future option for ClientPilot, not a mandatory standard for every Lewis Systems project.

## 17. Continuous Improvement

Review standards as the business gains delivery experience. Changes should improve reliability, security, maintainability, and customer value without introducing unnecessary process overhead.

---

© Lewis Systems. All rights reserved.
