# Contributing to Lewis Systems / ClientPilot

## Before changing files
1. Read the root README, [Project Index](docs/00-PROJECT-INDEX.md), and [Project Status](docs/13-PROJECT-STATUS.md).
2. Identify the authoritative requirement or architecture document.
3. Keep changes focused and avoid unrelated refactoring.

## Documentation
- Use clear Markdown headings and relative links.
- Distinguish implemented, recorded, verified, planned, and blocked work.
- Do not mark a feature complete without implementation and test evidence.
- Update the Project Index, Project Status, and Changelog when structure or milestones change.
- Record significant technology decisions as ADRs.

## Workflow exports
- Export Make scenarios only from a known scenario version.
- Sanitise tokens, credential references, private connection metadata, customer data, and unnecessary environment-specific IDs.
- Store reviewed exports in `workflows/make/` with export date and scenario version.
- Legacy n8n artefacts are not the current MVP implementation.

## Security
Read [Security Standards](docs/16-SECURITY.md). Never commit secrets or real customer personal information. Use synthetic examples.

## Commits and completion
Use clear commit messages. Before committing, review changed files, links, test evidence, and staged content. A change is complete only when implementation, testing, documentation, and repository state agree.
