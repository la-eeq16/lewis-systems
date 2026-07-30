# Lewis Systems AI Prompt Library

Document Version: 1.0

Status: Active

Company: Lewis Systems

Product: ClientPilot

Author: La-eeq Lewis

Last Updated: 30 July 2026

---

# Purpose

The `prompts` directory contains the official AI prompt specifications used by Lewis Systems products.

Each prompt is maintained as an independent document and is treated as a version-controlled engineering asset.

Prompts should not be embedded solely within application code or automation platforms. Instead, they should be documented, reviewed, tested, and versioned within this repository.

---

# Objectives

The Prompt Library aims to:

- Standardize AI behaviour across products.
- Improve prompt quality through version control.
- Enable prompt reuse.
- Support testing and validation.
- Simplify maintenance.
- Separate AI logic from implementation.

---

# Directory Structure

```
prompts/
│
├── README.md
├── PRM-001-Lead-Qualification.md
├── PRM-002-Meeting-Preparation.md
├── PRM-003-Executive-Summary.md
├── PRM-004-Follow-up-Email.md
├── PRM-005-Service-Recommendation.md
└── PRM-006-Lead-Classification.md
```

Future prompts should follow the same naming convention.

---

# Naming Convention

Every prompt must have a unique identifier.

Format:

```
PRM-001
PRM-002
PRM-003
```

File names should follow:

```
PRM-001-Lead-Qualification.md
```

Use descriptive names with hyphens.

---

# Required Sections

Every prompt specification should contain the following sections.

## Document Information

- Prompt ID
- Prompt Name
- Version
- Status
- Product
- Owner
- Workflow Reference
- Last Updated

---

## Purpose

Describe why the prompt exists.

---

## Business Goal

Explain the business problem the prompt solves.

---

## Inputs

List every expected input.

Example:

- Company Name
- Industry
- Revenue
- Budget
- Services
- Notes

---

## Outputs

Describe every expected output.

Example:

- Qualification Score
- Recommendation
- Confidence
- Reason
- Next Step

---

## System Prompt

The complete system prompt provided to the AI model.

---

## User Prompt Template

The template used to construct the user message.

---

## Expected Response Format

Specify the required response structure.

Prefer structured JSON where appropriate.

---

## Example Input

Provide a realistic example.

---

## Example Output

Provide the expected AI response.

---

## Failure Handling

Describe how the prompt should behave when:

- Information is missing.
- The AI is uncertain.
- Invalid inputs are received.

---

## Test Cases

Include representative test cases to verify prompt behaviour.

---

## Revision History

Track all changes made to the prompt.

Example:

| Version | Date | Description |
|----------|------|-------------|
| 1.0 | 30 Jul 2026 | Initial release |
| 1.1 | TBD | Improved qualification logic |

---

# Versioning

Prompt versions follow Semantic Versioning.

Examples:

Version 1.0

Initial release

Version 1.1

Minor improvements

Version 1.2

Prompt wording improvements

Version 2.0

Major behavioural changes

---

# AI Design Principles

Every prompt should:

- Solve a business problem.
- Produce consistent outputs.
- Avoid unnecessary creativity.
- Minimize hallucinations.
- Clearly communicate uncertainty.
- Support structured responses.
- Be easy to maintain.

---

# Best Practices

When writing prompts:

- Use clear and concise language.
- Avoid ambiguity.
- Request structured outputs.
- Define expectations explicitly.
- Provide sufficient context.
- Test prompts with realistic examples.
- Update documentation whenever prompts change.

---

# Relationship to Other Documentation

The Prompt Library works alongside:

- `docs/08-AI-PROMPTS.md` – Prompt catalogue and governance.
- `docs/07-WORKFLOW-DESIGN.md` – Business workflows using each prompt.
- `docs/09-API-INTEGRATIONS.md` – AI provider integrations.
- `docs/10-TESTING.md` – Prompt testing strategy.

---

# Engineering Principle

> AI prompts are considered part of the product and must be documented, version-controlled, tested, and reviewed like application code.

---

# Current Status

Phase

AI Prompt Library

Status

🟢 Active Development