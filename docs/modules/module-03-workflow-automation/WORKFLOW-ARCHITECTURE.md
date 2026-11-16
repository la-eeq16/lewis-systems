# Module 3 – Workflow Architecture

**Document Version:** 1.0  
**Product Version:** 0.3.0  
**Status:** Reviewed design; implementation evidence outstanding  
**Last Updated:** 16 November 2026

## 1. Architecture overview

The current ClientPilot MVP uses Google Forms and Google Sheets for intake capture, Make for orchestration and rule-based qualification, Airtable as the CRM datastore, Gmail for configured email communication, and a Calendly booking link for consultation hand-off.

```text
Prospective client
      |
      v
Google Form
      |
      v
Google Sheets response
      |
      v
Make – WF-001A Client Intake
      |                 |
      |                 +--> Validate required fields
      |                 +--> Find/create Company
      |                 +--> Find/create Contact
      |                 +--> Create Lead
      v
Airtable CRM
      |
      v
Make – WF-001B Lead Qualification
      |                 |
      |                 +--> Retrieve eligible Lead
      |                 +--> Calculate rule-based scores
      |                 +--> Determine outcome
      |                 +--> Record Qualification
      v
Airtable Lead and Qualification records
      |
      +--> Configured Gmail communication
      |
      +--> Calendly booking-link hand-off (where enabled)
```

This is a logical view, not a verified Make module-by-module diagram. Consult the exported scenarios before treating individual connections or branches as confirmed.

## 2. Workflow boundaries

| Workflow | Responsibility | Primary output |
|---|---|---|
| WF-001A | Validate and persist intake entities | Company, Contact, Lead |
| WF-001B | Score and classify an eligible Lead | Qualification result linked to Lead |

The workflows should remain independently testable. WF-001B must not assume that every intake record is complete or that every trigger event is unique.

## 3. Data ownership

- Google Forms / Sheets capture submitted intake values.
- Make validates, transforms, routes, and orchestrates the process.
- Airtable stores the operational CRM records.
- Gmail handles configured email delivery.
- Calendly handles the external booking experience; a sent booking link is not proof of a confirmed appointment.

The logical entity definitions and relationships are maintained in [05-DATA-MODEL.md](../../05-DATA-MODEL.md).

## 4. Current versus planned components

| Component | MVP position |
|---|---|
| Make orchestration | Selected current platform |
| Airtable CRM | Current operational datastore |
| Rule-based qualification | Current documented qualification approach |
| Gmail | Configured communication component; exact paths require scenario verification |
| Calendly booking link | Booking hand-off; full event synchronisation not assumed |
| OpenAI qualification | Planned enhancement, not current scoring mechanism |
| Slack notifications | Planned / not verified as implemented |
| n8n | Possible future migration platform |

## 5. Reliability requirements

- Validate required fields before creating downstream records.
- Avoid duplicate records when a scenario is retried.
- Never guess when a search returns multiple matches.
- Preserve Company–Contact–Lead relationships.
- Treat a Contact found under an unexpected Company as an exception requiring association verification.
- Do not fabricate qualification scores when required inputs are missing.
- Record failures and provide a safe recovery path.
- Keep booking-link delivery distinct from booking confirmation.

## 6. Verification required

The following require a live Make review or exported blueprint:

- Exact trigger configuration and polling behaviour.
- Actual module sequence, filters, routers, and route conditions.
- Airtable table and field identifiers.
- Formula expressions and missing-value handling.
- Error handlers, retries, and duplicate prevention.
- Gmail and Calendly hand-off configuration.
- Workflow log creation and administrator alerts.

---

© Lewis Systems. All rights reserved.
