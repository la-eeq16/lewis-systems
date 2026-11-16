# Make Implementation Record – WF-001A Client Intake

**Document Version:** 1.1  
**Product Version:** 0.3.0  
**Status:** Recorded as built and tested; live verification and export outstanding  
**Platform:** Make (EU1, per ADR-004)  
**Last Updated:** 16 November 2026

## 1. Purpose

Receive a Google Forms enquiry through Google Sheets, validate it, find or create the Company and Contact records, and create a linked Lead in Airtable.

## 2. Recorded scenario configuration

| Item | Recorded value |
|---|---|
| Make scenario ID | 6907653 |
| Scenario name | Client Intake |
| Trigger | Google Sheets – Watch Rows |
| Trigger interval | Every 15 minutes |
| Testing state | Both WF-001 scenarios were recorded as on-demand during testing; activate scheduling only after sign-off |
| Export | Not present in repository |

These details come from the Make implementation record dated 03 November 2026. Verify them in the live Make account before changing schedules or configuration.

## 3. Recorded logical flow

```text
Google Sheets – Watch Rows
        ↓
Set Variables / normalise intake values
        ↓
Router – Valid submission?
   ├── Valid → Search Company → Search Contact
   │             → Create / Update Company and Contact
   │             → Create Lead
   │             → Workflow Log (Completed)
   │             → Activity (Lead Created)
   └── Invalid → Workflow Log (Failed: validation failure)
```

Exact Make module numbers, router filters, and mapping expressions still require the exported blueprint.

## 4. Validation and normalisation recorded

Required values documented in the 03 November implementation note:
- First name and last name.
- Company name.
- Email and phone.
- Annual revenue.
- Service required.
- Industry.
- Consent.

Email format check recorded as:

`^[^@\\s]+@[^@\\s]+\\.[^@\\s]+$`

The implementation note also records normalisation of revenue band, employee band, urgency, and industry. Industry values are mapped to the approved list; unknown values become `Other`, with the original text appended to Lead notes. Airtable select writes use typecast disabled, so invalid option labels should fail rather than silently create new options.

## 5. Company and Contact handling

| Company match | Contact match | Recorded expected handling |
|---|---|---|
| Not found | Not found / no match | Create Company, create Contact, create Lead |
| Found | Not found | Create Contact, create Lead |
| Found | Found | Update Contact, create Lead |

The legacy implementation note does not fully specify the case where the Company is not found but the Contact search returns an existing Contact. Treat this as an exception until the live router logic and association rules are verified. Do not link a Contact to an unrelated Company.

## 6. Logging and error handling recorded

The 03 November implementation note records:
- Workflow Log written for Completed and Failed outcomes.
- Activity record for Lead Created.
- Airtable-step error handlers that write a Failed log.
- Break handler configured for three retries, ten minutes apart.
- Administrator alert after retries are exhausted: not yet built in that record.
- Stored incomplete executions retain the settings of the scenario version that created them; the note advises deleting them after a scenario fix rather than re-running stale executions.

Verify all of these settings against the live scenario.

## 7. Test evidence recorded

The earlier implementation record documents three qualification-path tests, but it does not provide a complete independent WF-001A intake regression matrix. Required intake retests:
- New Company + new Contact.
- Existing Company + existing Contact.
- Existing Company + new Contact.
- Contact / Company association exception.
- Missing required fields and invalid email.
- Unknown industry normalisation.
- Duplicate submissions and safe retry.

Record observed inputs, expected and actual outputs, date, and sanitised evidence. Do not mark a test Passed without an observed result.

## 8. Export checklist

- [ ] Export the current WF-001A Make blueprint.
- [ ] Remove credentials, tokens, connection metadata, unnecessary IDs, and customer data.
- [ ] Validate JSON syntax and review the export.
- [ ] Record export date and scenario version.
- [ ] Commit to `workflows/make/WF-001A-CLIENT-INTAKE.blueprint.json`.

---

© Lewis Systems. All rights reserved.
