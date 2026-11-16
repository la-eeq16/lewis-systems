# Module 3 – Workflow Specifications

**Document Version:** 1.0  
**Product Version:** 0.3.0  
**Status:** Design baseline; implementation verification outstanding  
**Last Updated:** 16 November 2026

## 1. WF-001A – Client Intake

### Objective

Convert a valid Google Forms submission into correctly linked Company, Contact, and Lead records in Airtable.

### Expected process

1. Receive a new form response through the configured Google Sheets / Make trigger.
2. Map submitted values into normalised working variables.
3. Validate required intake fields.
4. Search Airtable for the relevant Company.
5. Search for the Contact and verify the Contact's Company association.
6. Update or create the Company and Contact as appropriate.
7. Create the Lead and link it to the correct Company and Contact.
8. Record processing outcome and errors where workflow logging is configured.

### Company / Contact decision table

| Company match | Contact match | Expected handling |
|---|---|---|
| Found | Found and associated with Company | Update applicable records; create Lead |
| Found | Not found | Update Company; create Contact; create Lead |
| Not found | Not found | Create Company; create Contact; create Lead |
| Not found | Found | Exception: verify and resolve the Contact's Company association; do not silently attach it to an unrelated Company |

A multiple-match result must be routed for manual resolution rather than choosing an arbitrary record.

### Expected outputs

- Company record reference.
- Contact record reference.
- Lead record reference.
- Validation and processing outcome.
- Execution trace / workflow log where configured.

## 2. WF-001B – Rule-Based Lead Qualification

### Objective

Calculate a deterministic qualification score for an eligible Lead and persist the outcome.

### Expected process

1. Detect an eligible Lead according to the configured trigger.
2. Retrieve the Lead record.
3. Validate scoring inputs and handle missing or invalid values.
4. Calculate Revenue, Service, Urgency, Employee, and Budget component scores.
5. Calculate the total Qualification Score.
6. Apply the approved outcome thresholds.
7. Update the Lead with score, status, reason, and qualification date.
8. Create or update the linked Qualification record.
9. Perform only those email / booking hand-off actions confirmed as enabled in the live scenario.
10. Record execution outcome and errors where configured.

### Documented outcome thresholds

| Score | Outcome |
|---:|---|
| 64–100 | Qualified |
| 40–63 | Review Required |
| 0–39 | Not Qualified |

The project documentation records component score bands as revenue (0/10/20/30), service (25/20/15/10/5), urgency (15/11/7/3), employee count (2/4/6/8/10), and budget (0 in the current documented intake design). Exact category mappings, maximum possible score, missing-value rules, and threshold boundaries must be checked against the live Make scenario before being treated as verified.

### Outcome handling

- **Qualified:** eligible for the configured consultation booking-link hand-off.
- **Review Required:** retained for human review; not automatically approved or rejected.
- **Not Qualified:** handled according to the firm's configured follow-up policy.

A booking link being sent does not mean a meeting has been booked. A Meeting record with an awaiting-booking status is not a confirmed appointment.

## 3. Cross-workflow requirements

- WF-001A must create or link the Lead before WF-001B qualifies it.
- WF-001B must not create duplicate Qualification records on repeated trigger events.
- Both workflows must preserve Airtable record relationships.
- All dates and timestamps must use the agreed Africa/Johannesburg business timezone where local business time is required.
- Sensitive data must not be copied into unnecessary logs or repository test fixtures.

## 4. Error and exception requirements

| Condition | Required behaviour |
|---|---|
| Missing required intake value | Stop downstream creation and record validation failure |
| Multiple Company / Contact matches | Manual resolution; do not guess |
| Contact found but Company association conflicts | Exception path; verify association |
| Airtable operation fails | Preserve context and support safe retry |
| Qualification input missing | Do not invent a score; route to review/error handling |
| Email send fails | Record failure and allow controlled manual retry |
| Scenario retried | Avoid duplicate Leads, Qualifications, Activities, or messages |

The actual Make error handlers and retry settings are not verified until inspected.

## 5. Test scenarios required

- New Company + new Contact.
- Existing Company + existing associated Contact.
- Existing Company + new Contact.
- Contact exists but Company does not match.
- Duplicate search results.
- Missing required intake field.
- Missing / invalid qualification input.
- Scores immediately below, at, and above each qualification threshold.
- Repeated trigger / retry for the same source submission or Lead.
- Airtable unavailable and recovery.
- Email failure and booking-link hand-off.

Observed results and evidence belong in the project testing documentation and the relevant workflow implementation record.

---

© Lewis Systems. All rights reserved.
