# Module 3 – Workflow Field Mapping

**Document Version:** 1.0  
**Product Version:** 0.3.0  
**Status:** Logical mapping baseline; live field verification outstanding  
**Last Updated:** 16 November 2026

## 1. Purpose

This document records the logical data flow between intake, Make processing, and Airtable. It is not a substitute for the exact field IDs, module mappings, and formulas in the exported Make scenarios.

**Verification labels:** Documented = supported by project documentation; Verify = confirm exact live field name, type, option, or mapping in Google Forms, Sheets, Airtable, or Make.

## 2. WF-001A – Intake mapping

| Source value | Destination entity / field | Transformation / rule | Status |
|---|---|---|---|
| Form submission | Lead Source | Current documentation identifies Google Forms as source | Documented; verify live value |
| Company name and company details | Companies | Search before create; update existing match | Verify exact fields |
| Contact details | Contacts | Search and verify Company association before create/update | Verify exact fields |
| Intake values | Leads | Link Company and primary Contact; preserve submitted values | Verify exact fields |
| Services requested | Leads.Services Requested | Preserve selected service values and option labels | Verify |
| Estimated annual revenue | Leads.Estimated Annual Revenue | Numeric / currency-compatible value | Verify |
| Number of employees | Leads.Number of Employees | Numeric value or defined range | Verify |
| Current accounting software | Leads.Current Accounting Software | Preserve selected / entered value | Verify |
| Budget | Leads.Budget | Current form documentation says budget is not collected; do not infer it | Documented gap |
| Referral source | Lead source / attribution field | Current data-model review says referral source is collected but not separately persisted | Documented gap |
| Consent | Consent field / audit record | Current data-model review says consent is captured but not persisted in documented Lead mapping | Documented gap |

## 3. WF-001B – Qualification mapping

| Input | Logical score variable | Documented range / rule | Status |
|---|---|---|---|
| Estimated annual revenue | RevenueScore | 0 / 10 / 20 / 30 | Bands documented; exact formula verify |
| Services requested | ServiceScore | 5 / 10 / 15 / 20 / 25 | Category-to-points mapping verify |
| Urgency | UrgencyScore | 3 / 7 / 11 / 15 | Category-to-points mapping verify |
| Employee count | EmployeeScore | 2 / 4 / 6 / 8 / 10 | Category-to-points mapping verify |
| Budget | BudgetScore | 0 in current documented intake design | Documented; confirm no later form change |
| Component scores | QualificationScore | Sum of numeric score variables | Verify exact Make formula |
| QualificationScore | Qualification Status | 64–100 Qualified; 40–63 Review Required; 0–39 Not Qualified | Thresholds documented; verify live filters |
| Lead fields and score result | Qualifications record | Create/update linked Qualification record | Verify exact mapping |

### Revenue bands recorded in earlier implementation notes

- Less than R500,000: 0 points.
- R500,000 to less than R1,000,000: 10 points.
- R1,000,000 to less than R5,000,000: 20 points.
- R5,000,000 or more: 30 points.

Confirm these boundaries and currency assumptions against the deployed formula before production use.

## 4. Airtable Lead fields to verify

The implementation record identifies the following Lead fields for review:

- Lead ID
- Company
- Contact
- Lead Status
- Lead Source
- Services Requested
- Estimated Annual Revenue
- Number of Employees
- Current Accounting Software
- Budget
- Urgency
- Decision Maker Confirmed
- Qualification Score
- Qualification Status
- Qualification Reason
- AI Recommendation
- AI Summary
- Qualification Date
- Assigned Consultant
- Consultation Booked
- Calendly Booking
- Notes
- Linked Qualifications, Meetings, Activities, and Workflow Logs

The presence of a field in this list does not prove that it exists in the current Airtable base or is mapped by Make. Confirm field types, linked-record configuration, select options, and required status from the live base.

## 5. Mapping evidence to add

For each mapping, capture:

1. Source application, module, and field.
2. Destination application, module, table, and field.
3. Exact Make mapping expression or formula.
4. Default and missing-value behaviour.
5. Validation and error route.
6. Evidence reference (sanitised blueprint, screenshot, or test record).

Do not place real customer data, tokens, or credentials in evidence committed to Git.

---

© Lewis Systems. All rights reserved.
