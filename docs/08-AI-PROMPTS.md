# ClientPilot AI Prompt Library

This document is the index for AI prompts intended for ClientPilot. The current MVP qualification workflow uses deterministic rule-based scoring; AI prompts are not the active scoring mechanism.

Individual prompt specifications are maintained in the project's `/prompts` directory.

## Prompt Catalogue

| Prompt ID | Name | Status |
|---|---|---|
| PRM-001 | Lead Qualification | Planned – not used by current WF-001B |
| PRM-002 | Meeting Preparation | Planned |
| PRM-003 | Executive Summary | Planned |
| PRM-004 | Follow-up Email | Planned |
| PRM-005 | Service Recommendation | Planned |
| PRM-006 | Lead Classification | Planned |

## Governance

Before enabling a prompt in a live workflow, document its purpose, inputs, output schema, model/configuration, privacy constraints, failure behaviour, evaluation tests, and human-review requirements. AI output must not silently override the current deterministic qualification result without an approved product decision.
