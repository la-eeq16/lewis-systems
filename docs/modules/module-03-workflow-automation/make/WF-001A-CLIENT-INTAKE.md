# Make Implementation Record – WF-001A Client Intake

**Document Version:** 1.0  
**Product Version:** 0.3.0  
**Status:** Recorded as built and tested; repository evidence outstanding  
**Platform:** Make  
**Last Updated:** 16 November 2026

## 1. Purpose

Record the deployed Make implementation of WF-001A, which processes an intake submission and creates or links Company, Contact, and Lead records in Airtable.

## 2. Implementation status

The project implementation record states that the Company, Contact, and Lead creation paths have been built and tested. This document does not independently verify the live scenario. No sanitised Make blueprint is currently attached to this record.

## 3. Recorded logical sequence

The documented scenario flow is:

1. Google Forms / Google Sheets response trigger.
2. Set Multiple Variables for normalised intake values.
3. Validate required intake fields.
4. Search Companies in Airtable.
5. Route according to Company match.
6. Update or create Company as appropriate.
7. Search for Contact and verify its Company relationship.
8. Update or create Contact as appropriate.
9. Create Lead linked to the correct Company and Contact.

Exact Make module names, module numbers, filters, and route configuration must be transcribed from the current scenario export.

## 4. Required route verification

| Company | Contact | Expected action |
|---|---|---|
| Found | Found and associated | Update Company / Contact as required; create Lead |
| Found | Not found | Update Company; create Contact; create Lead |
| Not found | Not found | Create Company; create Contact; create Lead |
| Not found | Found | Exception: verify Company relationship; do not create an unsafe association |

Confirm whether the fourth case is technically reachable under the actual search logic and document its implemented route.

## 5. Configuration record – to complete from Make

| Configuration item | Recorded value |
|---|---|
| Scenario name | WF-001A – Client Intake (confirm exact name) |
| Scenario ID | Pending |
| Scenario version / last modified | Pending |
| Trigger type and source | Google Sheets response trigger (verify exact module and configuration) |
| Airtable base and tables | Pending verification |
| Search formulas and limits | Pending |
| Router filters | Pending |
| Error handlers / retry settings | Pending |
| Workflow logging | Pending |

## 6. Test evidence

Attach or reference sanitised evidence for:
- New Company + new Contact.
- Existing Company + existing Contact.
- Existing Company + new Contact.
- Contact / Company association exception.
- Missing required data.
- Duplicate search results.
- Safe retry without duplicate records.

No test result should be marked Passed until an observed result is recorded.

## 7. Export and security checklist

- [ ] Export the current Make scenario blueprint.
- [ ] Remove credentials, tokens, private connection metadata, and unnecessary IDs.
- [ ] Remove real customer data and replace with synthetic examples.
- [ ] Confirm the sanitised blueprint can be imported or reviewed.
- [ ] Record export date and scenario version.
- [ ] Commit the sanitised export under the agreed workflow export directory.

---

© Lewis Systems. All rights reserved.
