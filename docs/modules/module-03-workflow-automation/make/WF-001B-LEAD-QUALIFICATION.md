# Make Implementation Record – WF-001B Lead Qualification

**Document Version:** 1.0  
**Product Version:** 0.3.0  
**Status:** Recorded as built and tested; formula and repository evidence outstanding  
**Platform:** Make  
**Last Updated:** 16 November 2026

## 1. Purpose

Record the Make scenario that calculates a deterministic lead qualification score and stores the outcome in Airtable.

## 2. Implementation status

The project implementation record states that WF-001B has been built and tested as a rule-based qualification workflow. The live scenario and exported blueprint have not been independently checked for this repository update.

**Important:** Current qualification is documented as rule-based. OpenAI-powered evaluation is a planned enhancement, not the current scoring engine.

## 3. Recorded logical sequence

1. Watch eligible Airtable Lead records.
2. Get the full Lead record.
3. Set component variables: RevenueScore, ServiceScore, BudgetScore, UrgencyScore, EmployeeScore.
4. Calculate QualificationScore in a separate variable step using the numeric component variables.
5. Determine Qualification Status using the configured thresholds.
6. Update the Lead with score and outcome.
7. Create or update the related Qualification record.
8. Execute any configured communication / booking hand-off.
9. Record execution outcome where workflow logging is configured.

Confirm exact Make module names, sequence, filters, and field mappings against the export.

## 4. Documented scoring reference

| Component | Documented points |
|---|---:|
| Revenue | 0 / 10 / 20 / 30 |
| Service | 5 / 10 / 15 / 20 / 25 |
| Urgency | 3 / 7 / 11 / 15 |
| Employee count | 2 / 4 / 6 / 8 / 10 |
| Budget | 0 in the current documented intake design |

Revenue bands recorded in earlier implementation notes:

| Estimated annual revenue | Points |
|---|---:|
| Less than R500,000 | 0 |
| R500,000 to less than R1,000,000 | 10 |
| R1,000,000 to less than R5,000,000 | 20 |
| R5,000,000 or more | 30 |

The exact service, urgency, and employee category mappings are not reproduced here because they require confirmation from the deployed Make expressions and current form options. Do not infer them.

## 5. Qualification thresholds

| Total score | Status |
|---:|---|
| 64–100 | Qualified |
| 40–63 | Review Required |
| 0–39 | Not Qualified |

Verify the threshold filters, score maximum, and behaviour for null, empty, text, or out-of-range values.

## 6. Configuration record – to complete from Make

| Configuration item | Recorded value |
|---|---|
| Scenario name | WF-001B – Lead Qualification (confirm exact name) |
| Scenario ID | Pending |
| Scenario version / last modified | Pending |
| Trigger table and field | Pending |
| Qualification lookup / Get a Record mapping | Pending |
| Component score formulas | Pending |
| Total score formula | Numeric component variables; exact expression pending |
| Outcome filters | Thresholds above; verify exact operators |
| Airtable update/create mappings | Pending |
| Error handlers / retries | Pending |

## 7. Required tests

- Revenue band boundaries.
- Every service option and unknown service value.
- Every urgency option and missing urgency.
- Employee count boundaries and missing employee count.
- Budget absent / zero handling.
- Scores 39, 40, 63, 64, and maximum possible score.
- Reprocessing the same Lead without duplicate Qualification records.
- Airtable failure and recovery.
- Confirmed distinction between booking link sent and appointment booked.

Record observed inputs, expected outputs, actual outputs, date, and evidence reference. Do not mark a test Passed without an observed result.

## 8. Export and security checklist

- [ ] Export current Make scenario blueprint.
- [ ] Sanitise connection metadata, tokens, credentials, and unnecessary environment-specific identifiers.
- [ ] Remove private customer data.
- [ ] Verify formulas and route filters against the live scenario.
- [ ] Record scenario version and export date.
- [ ] Commit the sanitised export in the agreed workflow export directory.

---

© Lewis Systems. All rights reserved.
