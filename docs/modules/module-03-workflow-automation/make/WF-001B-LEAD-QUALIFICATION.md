# Make Implementation Record – WF-001B Lead Qualification

**Document Version:** 1.1  
**Product Version:** 0.3.0  
**Status:** Recorded as built and tested; live verification and export outstanding  
**Platform:** Make (EU1, per ADR-004)  
**Last Updated:** 16 November 2026

## 1. Purpose

Calculate a deterministic qualification score for an eligible Airtable Lead, update the Lead outcome, create the related Qualification record, and run the configured follow-up path.

**The current scoring engine is rule-based. OpenAI evaluation is planned, not the current scoring mechanism.**

## 2. Recorded scenario configuration

| Item | Recorded value |
|---|---|
| Make scenario ID | 7171530 |
| Scenario name | Lead Qualification |
| Trigger | Airtable – Watch Records |
| Trigger filter | Qualification Status = Pending |
| Maximum records | 10 |
| Testing state | Both WF-001 scenarios were recorded as on-demand during testing; activate scheduling only after sign-off |
| Export | Not present in repository |

These values are taken from the implementation note dated 03 November 2026 and must be verified against the live Make account.

## 3. Recorded logical flow

```text
Watch Records (Pending) → Get Lead → Calculate score → Update Lead
  → Create Qualification → Workflow Log → Activity
  → Get Contact → Get Settings → Router
       ├── Qualified → Create Meeting (Awaiting Booking)
       │                 → Booking email → Activity (Email Sent)
       ├── Not Qualified → Follow-up email → Activity (Email Sent)
       └── Review Required → no email and no meeting
```

The implementation note records emails sent using Make's `google-email` v4 Send an Email module. It records email content/configuration from the Settings table and says emails are skipped when Email Notifications Enabled is false or the Contact has no email. Verify current live configuration.

## 4. Recorded scoring model

| Component | Documented points |
|---|---:|
| Annual revenue | 0 / 10 / 20 / 30 |
| Service requested | 25 / 20 / 15 / 10 / 5 |
| Urgency | 15 / 11 / 7 / 3 |
| Employees | 2 / 4 / 6 / 8 / 10 |
| Budget | 0 (not collected by the documented form) |

Revenue bands recorded in earlier implementation notes:

| Estimated annual revenue | Points |
|---|---:|
| Less than R500,000 | 0 |
| R500,000 to less than R1,000,000 | 10 |
| R1,000,000 to less than R5,000,000 | 20 |
| R5,000,000 or more | 30 |

The exact service, urgency, and employee category-to-point mappings must be copied from the live Make expressions and current form options. Do not infer them from the point ranges.

## 5. Outcome thresholds and behaviour

| Score | Outcome | Recorded action |
|---:|---|---|
| 64 or higher | Qualified | Set Lead Status Qualified; create Meeting with status Awaiting Booking; send booking email |
| 40–63 | Review Required | Manual staff review; no email or Meeting |
| Below 40 | Not Qualified | Set Lead Status Not Qualified; send polite follow-up email |

The Settings table is recorded as holding a threshold value of 64, but the scenario uses fixed threshold values. Settings-driven thresholds remain outstanding.

A booking link being sent does not mean a consultation has been booked. Calendly event synchronisation and automatic Meeting status updates remain planned.

## 6. Logging and error handling recorded

The 03 November implementation note records:
- Workflow Log and Activity records for qualification outcomes.
- Failed logs and Break-handler retries on Airtable-step errors.
- Three retries, ten minutes apart.
- Administrator alert after all retries are exhausted: not yet built in that record.
- Incomplete executions retain the scenario settings from their originating version; review and clear stale incomplete executions after fixing a scenario rather than blindly re-running them.

Verify current settings and behaviour in Make.

## 7. Sample test results recorded (03 November 2026)

| Test lead | Score | Outcome | Result recorded |
|---|---:|---|---|
| Harbour Advisory Test | 76 | Qualified | Meeting Awaiting Booking created; booking email received; link and wording checked |
| Corner Bakery Test | 15 | Not Qualified | Follow-up email received; Lead Status checked |
| Mid Retail Test | 50 | Review Required | No email or Meeting created |

These are historical test results recorded in the implementation note, not a new test run performed during this audit. The note also states the newly expanded industry list had not yet been re-tested.

## 8. Required verification and regression tests

- Verify all component score mappings and formulas.
- Verify missing, empty, text, and out-of-range values.
- Test scores 39, 40, 63, and 64.
- Test maximum possible score and each revenue boundary.
- Reprocess the same Lead and confirm no duplicate Qualification, Meeting, or email.
- Test Airtable failure and retry recovery.
- Confirm disabled email setting and missing Contact email suppress sending.
- Confirm only Qualified leads create an Awaiting Booking Meeting.
- Confirm a sent booking link is not recorded as a confirmed appointment.

## 9. Export checklist

- [ ] Export the current WF-001B Make blueprint.
- [ ] Remove credentials, tokens, connection metadata, unnecessary IDs, and customer data.
- [ ] Verify formula and filter configuration against the live scenario.
- [ ] Validate JSON syntax and review the export.
- [ ] Record export date and scenario version.
- [ ] Commit to `workflows/make/WF-001B-LEAD-QUALIFICATION.blueprint.json`.

---

© Lewis Systems. All rights reserved.
