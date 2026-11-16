# ClientPilot Data Model

**Document Version:** 2.3  
**Product Version:** 0.3.0  
**Status:** Conceptual Model Approved – Implementation Verification Required  
**Company:** Lewis Systems  
**Product:** ClientPilot  
**Author:** La-eeq Lewis  
**Phase:** Phase 3 – MVP Implementation  
**Last Updated:** 16 November 2026

---

## 1. Purpose

This document defines ClientPilot's logical business entities, attributes, relationships, identifier conventions, and current Airtable implementation notes.

It distinguishes the intended conceptual model from the current MVP configuration. A conceptual entity or attribute is not proof that a corresponding Airtable table or field exists.

## 2. Design Principles

- Business-first and technology-independent definitions.
- Clear ownership and relationships between records.
- Unique logical identifiers for integration and migration.
- Data integrity and auditability.
- Minimum necessary collection of personal information.
- Tenant isolation as a requirement before multi-customer deployment.
- Native linked-record relationships where supported by the platform.

## 3. Entity Overview

The conceptual model includes:

- Organization
- User
- Company
- Contact
- Lead
- Qualification
- Meeting
- AI Summary
- Activity
- Workflow Execution (implemented conceptually as Workflow Logs)

The current Airtable MVP operational tables are recorded as Companies, Contacts, Leads, Qualifications, Meetings, Activities, Workflow Logs, and Settings. Organization and User are not currently represented as fully implemented core tables. AI Summary is stored in fields rather than a separate table.

## 4. Entity Definitions

### 4.1 Organization

Represents a firm using ClientPilot.

**Logical identifier:** Organization ID  
**Attributes:** Organization Name, Industry, Country, Time Zone, Status, Created Date, Last Updated.

**Implementation:** No dedicated Organization table is recorded in the current MVP. Organization ID is present only in selected locations. Full tenant ownership on every record is a future requirement.

### 4.2 User

Represents a person authorised to use a firm's ClientPilot workspace.

**Logical identifier:** User ID  
**Relationship:** belongs to one Organization.  
**Attributes:** First Name, Last Name, Email, Role, Status, Last Login.

**Implementation:** A complete User table and user-management feature are not part of the current MVP.

### 4.3 Company

Represents the business that submits or is associated with an enquiry.

**Logical identifier:** Company ID  
**Relationships:** belongs to an Organization; may have multiple Contacts and Leads.  
**Attributes:** Company Name, Industry, Annual Revenue, Employee Count, Website, Country, Province, City.

**Implementation:** Airtable Companies table. Company links should use Airtable Linked Record fields.

### 4.4 Contact

Represents a person associated with a company and a lead.

**Logical identifier:** Contact ID  
**Relationships:** belongs to one Company and one Organization; may be associated with multiple Leads.  
**Attributes:** First Name, Last Name, Email, Phone Number, Job Title, Decision Maker, Preferred Contact Method.

**Implementation:** Airtable Contacts table, linked to Companies.

### 4.5 Lead

Represents a prospective-client enquiry.

**Logical identifier:** Lead ID  
**Relationships:** belongs to an Organization; links to one Company and one primary Contact; may have Qualifications, Meetings, Activities, and Workflow Logs.

**Attributes:** Lead Status, Lead Source, Services Requested, Estimated Annual Revenue, Number of Employees, Current Accounting Software, Budget, Urgency, Decision Maker Confirmed, Qualification Score, Qualification Status, Qualification Reason, AI Recommendation, AI Summary, Qualification Date, Assigned Consultant, Consultation Booked, Calendly Booking, Notes, Created Time.

**Implementation:** Airtable Leads table, linked to Companies and Contacts. Some attributes may be blank or not yet populated by the current form/workflow. AI Recommendation and AI Summary are future-use fields until the AI module is implemented.

### 4.6 Qualification

Stores an assessment of a lead.

**Logical identifier:** Qualification ID  
**Relationship:** belongs to one Lead.  
**Attributes:** Revenue Score, Service Score, Employee Score, Urgency Score, Budget Score, Total Score, Qualification Result, Assessment Status, Qualification Reason, AI Recommendation, Confidence Score, Manual Override, Reviewed By, Review Date.

**Implementation:** Airtable Qualifications table. The current rule-based version uses revenue, service, employee, and urgency scoring. Budget is documented as zero because it is not collected by the current form. Dedicated component score fields and exact mappings must be checked against the live base. AI-related attributes are reserved for future use.

### 4.7 Meeting

Represents a consultation associated with a lead.

**Logical identifier:** Meeting ID  
**Relationships:** belongs to an Organization and Lead; may link to Company, Contact, and Qualification.  
**Attributes:** Meeting Name, Meeting Type, Meeting Date, Meeting Time, Calendly Event ID, Assigned Consultant, Meeting Status, Meeting Notes, AI Meeting Brief, Outcome.

**Implementation:** Airtable Meetings table. The documented workflow may create a record with status Awaiting Booking before a confirmed booking exists. A booking link being sent is not the same as a meeting being booked.

### 4.8 AI Summary

Stores an AI-generated preparation brief.

**Logical identifier:** Summary ID  
**Relationship:** associated with a Meeting and its Lead.  
**Attributes:** Executive Summary, Client Background, Suggested Services, Potential Risks, Questions to Ask, Opportunities, Confidence Score.

**Implementation:** No separate AI Summary table is recorded. Fields exist or are planned on Leads and Meetings. Generation is planned for the AI module.

### 4.9 Activity

Stores an audit record of an important business or workflow event.

**Logical identifier:** Activity ID  
**Relationships:** belongs to an Organization and may link to a Lead.  
**Attributes:** Activity Type, Description, Created By, Created Date, Status.

**Implementation:** Airtable Activities table. Confirm exact fields and links during implementation verification.

### 4.10 Workflow Execution

Stores execution and diagnostic information for an automated workflow.

**Logical identifier:** Workflow Log ID (WFL prefix)  
**Relationships:** belongs to an Organization and may reference a Lead.  
**Attributes:** Workflow Name, Scenario / Workflow ID, Execution Status, Start Time, End Time, Duration, Error Message, Retry Count.

**Implementation:** Airtable Workflow Logs table. Confirm whether Make execution identifiers, retry counts, and error details are actually mapped.

### 4.11 Settings

Stores firm-specific workflow configuration.

**Logical identifier:** Settings record / configured setting key (implementation-specific).  
**Attributes recorded in the current design:** Setting Group, Company Name, Default Consultant, Qualification Threshold, Booking Link, notification switches, OpenAI Model.

**Implementation:** Airtable Settings table. Values must describe the customer firm, not Lewis Systems. Dynamic threshold retrieval is planned; the current WF-001B is documented as using fixed threshold values.

## 5. Relationships

| Parent | Cardinality | Child | Notes |
| --- | --- | --- | --- |
| Organization | 1 to many | Users | Conceptual; not fully implemented |
| Organization | 1 to many | Companies | Tenant ownership requirement |
| Organization | 1 to many | Leads | Tenant ownership requirement |
| Company | 1 to many | Contacts | A company can have multiple contacts |
| Company | 1 to many | Leads | A company may generate multiple enquiries |
| Contact | 1 to many | Leads | A contact may submit multiple enquiries |
| Lead | 1 to many | Qualifications | Keep assessment history; identify the current result |
| Lead | 1 to many | Meetings | A lead may have consultations over time |
| Lead | 1 to many | Activities | Record important events |
| Lead | 1 to many | Workflow Logs | Record workflow executions |
| Meeting | 0 or 1 | AI Summary | Planned; no separate summary table in MVP |

## 6. Airtable Implementation Notes

The following describe the documented implementation and outstanding verification items:

- Current operational tables: Companies, Contacts, Leads, Qualifications, Meetings, Activities, Workflow Logs, Settings.
- Organization is not a dedicated table. Organization ID is recorded only in selected locations; full tenant separation is not implemented.
- Settings is described as a configuration table containing firm-specific details, booking link, thresholds, notification switches, and AI model configuration.
- Industry uses a controlled single-select list shared by the form, Airtable, and Make. Confirm exact option spelling against the live services before changing it.
- Consent is validated by the workflow but is not recorded on the Lead in the documented design. Review whether a consent timestamp/version and source should be retained to provide appropriate evidence.
- Referral Source is collected by the form but is not currently stored; Lead Source is set to Google Forms in the documented mapping.
- Qualification thresholds exist in Settings, but WF-001B is documented as using fixed thresholds (64 and 40). Reading thresholds dynamically is outstanding.
- Select values are written with typecast disabled, so each option must exist in Airtable with matching spelling.
- Airtable linked-record fields should be used for Company, Contact, Lead, Qualification, and Meeting relationships where applicable.

## 7. Business Rules and Integrity Constraints

1. Every logical record must have a stable identifier appropriate to its entity.
2. Every production customer record must belong to exactly one customer organization once multi-tenancy is implemented.
3. Every Lead must link to one Company and one primary Contact.
4. Every Contact must link to a Company.
5. A Lead may have multiple historical Qualification records, but only one current assessment.
6. A Meeting must reference the relevant Lead.
7. A meeting should only be confirmed for a lead eligible under the firm's booking policy.
8. An Awaiting Booking record must not be represented as a confirmed appointment.
9. Every Activity must include a timestamp.
10. Workflow logs should identify the workflow, execution status, and relevant lead where available.
11. Retried workflow operations must avoid unintended duplicate records or communications.
12. Personal data must be limited to what is necessary for the stated purpose and protected from unauthorised access.

## 8. Identifier Standards

| Entity | Prefix | Example |
| --- | --- | --- |
| Organization | ORG | ORG-000001 |
| User | USR | USR-000001 |
| Company | COM | COM-000001 |
| Contact | CON | CON-000001 |
| Lead | LED | LED-000001 |
| Qualification | QLF | QLF-000001 |
| Meeting | MTG | MTG-000001 |
| AI Summary | AIS | AIS-000001 |
| Activity | ACT | ACT-000001 |
| Workflow Log | WFL | WFL-000001 |

Logical identifiers are distinct from Airtable's internal record IDs. Do not assume a prefix-based identifier is automatically generated until its generation mechanism is implemented and tested.

## 9. Security and Privacy Requirements

- Do not expose one firm's records to another firm.
- Implement tenant identifiers and access enforcement before multi-customer shared deployment.
- Restrict access to customer records and connected accounts.
- Do not place credentials or sensitive personal information in source control.
- Define data retention, correction, and deletion processes before production use.
- Use synthetic or anonymised records in repository test fixtures.

## 10. Future Entities

Potential future entities include Proposal, Invoice, Client Portal Account, Subscription, Document, Task, Email Campaign, WhatsApp Conversation, and Voice Call. These are not part of the current MVP data implementation.

## 11. Implementation Verification Checklist

The Airtable implementation must be checked against the live base before this document is used as a field-by-field build specification:

- Confirm each of the eight operational tables exists.
- Confirm logical ID fields and uniqueness approach.
- Confirm all Linked Record relationships and reciprocal fields.
- Confirm Lead fields and current form mappings.
- Confirm Qualification component score fields and calculation.
- Confirm Meeting status and booking fields.
- Confirm Activity and Workflow Log fields.
- Confirm Settings structure and actual threshold source.
- Record any differences and update this document.

**Current record:** The project documentation reports the eight operational tables and initial QA as implemented. This has not been independently verified against the live Airtable base during this documentation update.

---

© Lewis Systems. All rights reserved.
