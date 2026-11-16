# WF-001 – Client Intake & Qualification: Make Implementation

> **Historical implementation record.** This document is retained for traceability. The canonical current records are [WF-001A](../module-03-workflow-automation/make/WF-001A-CLIENT-INTAKE.md) and [WF-001B](../module-03-workflow-automation/make/WF-001B-LEAD-QUALIFICATION.md). Verify every configuration detail against the live Make account before relying on it.

**Module:** 03 – Workflow Automation
**Workflow ID:** WF-001
**Platform:** Make (EU1)
**Document Version:** 1.0
**Last Updated:** 03 November 2026
**Author:** La-eeq Lewis
**Status:** Historical record dated 03 November 2026; not independently re-verified

---

# 1. Purpose

WF-001 takes a Google Form enquiry, creates the CRM records, qualifies the lead, and either sends a consultation booking link or a polite follow-up. The business logic is defined in `docs/07-WORKFLOW-DESIGN.md`. This document records how it is built in Make.

WF-001 is split into two scenarios because intake and qualification run on different triggers and can fail independently.

| Scenario | Make ID | Name | Trigger |
|---|---|---|---|
| WF-001A | 6907653 | Client Intake | Google Sheets – Watch Rows (every 15 minutes) |
| WF-001B | 7171530 | Lead Qualification | Airtable – Watch Records (`Qualification Status = Pending`, max 10) |

Both scenarios are currently set to run on demand during testing. Activate scheduling only after sign-off.

---

# 2. WF-001A – Client Intake

```
Watch Rows → Set Variables → Router
   ├─ Valid submission → Search Company → Search Contact → Create/Update Company, Contact, Lead
   │                       → Workflow Log (Completed) → Activity ("Lead Created")
   └─ Invalid submission → Workflow Log (Failed, "Validation failed…")
```

## 2.1 Validation (filter "Valid submission")

All of the following must be present: first name, last name, company name, email, phone, annual revenue, service required, industry, consent. Email must match `^[^@\s]+@[^@\s]+\.[^@\s]+$`.

Invalid submissions create no CRM records and are logged as Failed.

## 2.2 Data cleaning (Set Variables)

- Revenue band → number (0 / 500 000 / 1 000 000 / 5 000 000 / 20 000 000).
- Employee band → number (1 / 6 / 21 / 51 / 101).
- Urgency normalised.
- **Industry:** trimmed and matched against the approved list below. Anything else becomes `Other`, and the original text is appended to the lead notes as `[Industry submitted: …]`.

**Approved industries (must match Airtable, the Google Form and Make exactly):**
Accounting, Agriculture, Business Coaching, Construction, Consulting, Education, Financial Services, Healthcare, Hospitality & Food, Insurance, Law, Manufacturing, Marketing, Mining, Real Estate, Retail, Technology, Transport & Logistics, Other.

Airtable select fields are written with `typecast = false`, so a misspelled value fails with a 422 error rather than creating a new option.

## 2.3 Company / contact logic

| Company | Contact | Result |
|---|---|---|
| Not found | – | Create company (industry set here) and contact, then lead |
| Found | Not found | Create contact, then lead |
| Found | Found | Update contact, then lead |

Industry is only set when a company is first created.

---

# 3. WF-001B – Lead Qualification

```
Watch Records (Pending) → Get Lead → Calculate score → Update Lead
   → Create Qualification → Workflow Log → Activity ("Qualification Completed")
   → Get Contact → Get Settings → Router
        ├─ Qualified → Create Meeting (Awaiting Booking) → Booking email → Activity ("Email Sent")
        ├─ Not Qualified → Follow-up email → Activity ("Email Sent")
        └─ Review Required → no email, no meeting
```

## 3.1 Scoring (rule-based v1)

| Factor | Points |
|---|---|
| Annual revenue | 0 / 10 / 20 / 30 |
| Service requested | 25 / 20 / 15 / 10 / 5 |
| Urgency | 15 / 11 / 7 / 3 |
| Employees | 2 / 4 / 6 / 8 / 10 |
| Budget | 0 (not collected by the form) |

Thresholds: **Qualified ≥ 64**, **Review Required 40–63**, **Not Qualified < 40**. The threshold is currently also held in the Settings table (value 64); the scenario uses fixed values.

Note: industry does not affect the score.

## 3.2 Outcomes

- **Qualified:** Lead Status = Qualified; Meeting created with type "Initial Consultation" and status **Awaiting Booking**; booking email sent.
- **Not Qualified:** Lead Status = Not Qualified; follow-up email sent.
- **Review Required:** staff review manually.

## 3.3 Emails

Sent with the Make `google-email` v4 "Send an Email" module through the existing Google connection. Content comes from the **Settings** table (Setting Group = "System Configuration"): Company Name, Default Consultant, Booking Link, Email Notifications Enabled.

Because ClientPilot is built for client firms, Settings must hold the **client firm's** details, not Lewis Systems'. Emails are skipped when Email Notifications Enabled is false or the contact has no email.

---

# 4. Logging and error handling

- Every run writes a Workflow Log (Completed or Failed) and Activity records.
- Every Airtable step has an error handler that writes a Failed log and then a Break handler: 3 retries, 10 minutes apart.
- Incomplete executions keep the settings of the scenario version that created them. After fixing a scenario, **delete** stored incomplete executions rather than re-running them.
- Not yet built: an administrator alert when all retries are exhausted.

---

# 5. Test results (03 November 2026)

| Lead | Score | Outcome | Verified |
|---|---|---|---|
| Harbour Advisory Test | 76 | Qualified | Meeting "Awaiting Booking"; booking email received; link and wording checked |
| Corner Bakery Test | 15 | Not Qualified | Follow-up email received; Lead Status checked |
| Mid Retail Test | 50 | Review Required | No email or meeting created |

Not yet re-tested after the industry list change (19 industries): a new submission with a newly added industry.

---

# 6. Known issues and fixes

| Issue | Cause | Fix |
|---|---|---|
| `[422] Field "Retry Count" cannot accept the provided value` | A text value was written to a number field | Removed Retry Count from the completion log modules |
| Gmail module rejected the connection (SC424) | Restricted Google scopes are not available to personal @gmail.com accounts | Use `google-email` v4 "Send an Email" |
| Industry blank after recreating "Other" | Recreating a select option clears values on existing records | Re-set values manually |

---

# 7. Remaining work

- Administrator alert after retries are exhausted.
- AI evaluation step (replace or supplement rule-based scoring) and meeting-preparation summary.
- Staff notification (Slack).
- Update meeting status when a consultation is booked (Calendly, Module 6).
- Organisation ID for multi-tenancy.
- Export Make blueprints to `workflows/make/`.