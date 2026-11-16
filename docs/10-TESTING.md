# ClientPilot Testing Strategy

Document Version: 1.1

Product Version: 0.3.0

Status: Active

Company: Lewis Systems

Product: ClientPilot

Author: La-eeq Lewis

Last Updated: 16 November 2026

---

# 1. Purpose

This document defines the testing strategy for ClientPilot.

Testing ensures that all business processes, workflows, AI prompts, integrations, and user-facing functionality perform reliably before release.

---

# 2. Testing Principles

Testing at Lewis Systems follows these principles:

- Test early.
- Test often.
- Automate where practical.
- Document all defects.
- Verify fixes before release.

---

# 3. Testing Levels

ClientPilot uses the following testing levels:

- Unit Testing
- Integration Testing
- Workflow Testing
- AI Prompt Testing
- User Acceptance Testing (UAT)
- Regression Testing

---

# 4. Test Coverage

The following components must be tested:

- Lead Capture
- Qualification Workflow
- AI Responses
- Airtable Integration
- Calendly Booking
- Slack Notifications
- Error Handling
- Security Controls

---

# 5. Test Environment

Environment:

Development

Tools:

- Make (MVP; n8n planned)
- Airtable
- OpenAI
- Calendly
- Slack

---

# 6. Defect Management

Each defect should record:

- Defect ID
- Description
- Severity
- Status
- Owner
- Date Reported
- Resolution

---

# 7. Acceptance Criteria

A release is approved when:

- Critical defects are resolved.
- Core workflows succeed.
- AI outputs are validated.
- Documentation is current.

---

# 8. WF-001 Test Scenarios (Make)

Run in the Make scenarios WF-001A and WF-001B using the Google Form. Use your own email address for test submissions.

| Scenario | Expected result |
|---|---|
| Strong lead (score ≥ 64) | Lead Qualified; Meeting created as *Awaiting Booking*; booking email received with the client firm's details and booking link |
| Weak lead (score < 40) | Lead Status *Not Qualified*; polite follow-up email received |
| Middle lead (40–63) | Qualification Result *Review Required*; no email, no meeting |
| Invalid submission (missing field, bad email) | No CRM records; Workflow Log *Failed* ("Validation failed…") |
| New industry from the standard list | Company created with that Industry |
| Industry not on the list | Company Industry *Other*; original text appended to the lead notes |
| Existing company / existing contact | No duplicates created; lead linked to the existing records |
| Airtable error | Failed Workflow Log written; execution stored for retry (3 attempts, 10 minutes apart) |

Delete stored incomplete executions after fixing a scenario; they keep the old settings.

---

# 9. Current Status

Phase

Testing Strategy

Status

🟢 Active Development