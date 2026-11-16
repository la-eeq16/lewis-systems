# Coding and Repository Standards

This document supplements [Development Standards](06-DEVELOPMENT-STANDARDS.md).

- Prefer small, focused, reviewable changes.
- Use clear names and consistent formatting.
- Separate business logic from provider-specific integration details where practical.
- Validate external input and handle missing or malformed values explicitly.
- Avoid hard-coded secrets and environment-specific configuration.
- Include useful error handling and privacy-conscious logging.
- Add tests for changed behaviour and document manual test evidence when automated tests are unavailable.
- Do not commit generated build output, local databases, logs, credentials, or customer data.
- Review and sanitise Make / n8n exports before version control.

A change is complete only when implementation, tests, documentation, and repository state agree.
