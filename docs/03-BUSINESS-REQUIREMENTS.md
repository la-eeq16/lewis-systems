# ClientPilot Business Requirements Document (BRD)

**Document Version:** 2.2  
**Product Version:** 0.3.0  
**Status:** Active – MVP Development  
**Company:** Lewis Systems  
**Product:** ClientPilot  
**Author:** La-eeq Lewis  
**Last Updated:** 16 November 2026

---

## 1. Purpose

This document defines the business problem, intended customer value, business objectives, operating assumptions, and commercial context for ClientPilot. The Product Requirements Document defines the product capabilities; this document explains why those capabilities matter.

## 2. Executive Summary

ClientPilot is the first product being developed by Lewis Systems. It is intended to help small accounting firms in South Africa manage prospective-client enquiries more consistently, reduce manual qualification work, and progress suitable leads towards consultations.

Lewis Systems has a broader business direction: deliver custom systems and automation services to small businesses, while identifying repeatable solutions that may become reusable products. ClientPilot is the first focused product experiment within that wider strategy.

## 3. Business Opportunity and Problem

Small accounting firms may rely on manual processes to receive enquiries, collect information, determine whether a prospect fits their services, and coordinate follow-up. These activities can consume time, create inconsistent handling, and make it difficult to prioritise suitable prospects.

ClientPilot seeks to improve this process by connecting intake, CRM record management, rule-based qualification, and follow-up in a documented workflow.

The problem and proposed value must be validated with real accounting-firm users during discovery and pilot activity; the assumptions in this document are not evidence of proven market demand.

## 4. Target Customer

### Initial customer segment

Small accounting firms operating in South Africa, particularly firms that:

- Have limited administrative capacity.
- Receive enquiries through online or manual channels.
- Need to assess service fit before booking consultations.
- Maintain prospect information in spreadsheets or lightweight CRM tools.
- Want practical automation without adopting a large enterprise platform.

### Future expansion

Other service industries may be considered after ClientPilot's initial workflow is validated. Expansion is not assumed for the first release.

## 5. Stakeholders

| Stakeholder | Business interest |
| --- | --- |
| Firm owner / decision-maker | Better use of staff time and improved enquiry handling |
| Administrator | Less repetitive capture and follow-up |
| Accountant / consultant | Better visibility of prospect needs and suitability |
| Prospective client | Clear and timely communication |
| Lewis Systems | Deliver a reliable solution, learn from deployment, and build reusable capability |

## 6. Business Objectives

- Reduce repetitive administrative effort in the enquiry process.
- Improve consistency of lead information.
- Make lead qualification more transparent.
- Reduce avoidable delays in responding to prospects.
- Improve visibility of enquiry status and next actions.
- Establish a repeatable implementation that can be supported and maintained.
- Validate whether the solution creates sufficient customer value to justify continued investment.

## 7. Business Requirements

| ID | Business requirement | Measure / evidence |
| --- | --- | --- |
| BR-001 | The firm must be able to capture prospect enquiries consistently. | Successful test submissions and mapped CRM records |
| BR-002 | Staff must be able to identify the company and contact associated with each lead. | Correct linked-record checks |
| BR-003 | Staff must be able to understand why a lead received its qualification outcome. | Score and reason review |
| BR-004 | Suitable prospects should be directed towards the firm's consultation process. | Booking-link hand-off test |
| BR-005 | Staff should be able to identify failed or incomplete workflow executions. | Failure log and alert/recovery test |
| BR-006 | The implementation must be affordable and maintainable for a small firm. | Documented operating cost and support assessment |
| BR-007 | Customer data must be handled securely and only for authorised business purposes. | Access review and data-handling checks |

## 8. Value Proposition

ClientPilot aims to provide the accounting firm with:

- More consistent enquiry capture.
- Less repetitive data entry.
- A structured view of companies, contacts, and leads.
- Transparent initial lead scoring.
- A clearer route from enquiry to consultation.
- Better traceability when workflow steps fail.

The value proposition should be evaluated through pilot feedback, processing metrics, and evidence of time saved—not assumed solely from successful automation runs.

## 9. Commercial Model

### Initial delivery approach

Lewis Systems may charge for:

- Initial setup and implementation.
- Workflow customisation.
- CRM configuration and data mapping.
- Staff onboarding and training.
- Ongoing support or maintenance, where agreed.

Pricing, support commitments, service levels, and ownership of third-party subscriptions must be agreed with each customer before deployment.

### Potential future revenue

- Recurring managed automation or support services.
- Product subscriptions.
- Premium integrations and AI-assisted capabilities.
- Custom development and reporting.

These are potential models, not confirmed current revenue streams.

## 10. Business Success Measures

During discovery and pilot, record a baseline and evaluate:

- Average time spent processing an enquiry.
- Time from submission to first response.
- Percentage of enquiries with complete records.
- Staff agreement with qualification outcomes.
- Consultation booking rate.
- Workflow error rate and time to recovery.
- Customer satisfaction and willingness to continue using the system.

No numerical performance target is set until baseline information is available.

## 11. Assumptions to Validate

- Accounting firms experience meaningful friction in manual enquiry handling.
- The firm's enquiry volume and process justify automation.
- Staff will use a structured CRM workflow.
- The qualification criteria reflect the firm's actual ideal-client profile.
- Faster and more consistent handling can improve the customer experience.
- The cost of implementation and ongoing tools is acceptable to the customer.

## 12. Business Risks and Mitigation

| Risk | Mitigation |
| --- | --- |
| Market need is weaker than expected | Interview target firms and run a limited pilot |
| Qualification rules do not reflect firm policy | Agree criteria with the customer and retain manual review |
| Staff resist a new process | Keep the workflow simple and provide onboarding |
| Third-party platform costs or limits change | Monitor costs and document alternatives |
| Customer data is mishandled | Define access, retention, consent, and incident procedures |
| Customisation makes support difficult | Document configuration and separate reusable components |

## 13. Version 1 Business Scope

### Included in the current MVP build

- Enquiry capture.
- Company, contact, and lead record management.
- Rule-based lead qualification.
- Qualification outcome and reason storage.
- Initial follow-up / booking-link hand-off where configured.

### Planned extensions

- OpenAI-assisted qualification and meeting preparation.
- Slack notifications.
- Automated Calendly booking synchronisation.
- Enhanced failure alerts and end-to-end operational monitoring.

### Not included in the initial business scope

- Billing or payment processing.
- Full client portal.
- Custom CRM platform.
- Mobile application.
- Full tenant self-service administration.

## 14. Relationship to Lewis Systems Strategy

Lewis Systems is not limited to accounting firms. Its wider strategy is to build custom systems for small businesses and convert validated, repeatable solutions into reusable products. ClientPilot's initial accounting-firm focus is a deliberate product validation choice, not the company's permanent market boundary.

## 15. Approval and Change Control

Business requirements should be reviewed with the pilot customer before production use. Changes to the target customer, value proposition, commercial commitments, or business scope must be recorded and reflected in the PRD and Project Status document.

---

© Lewis Systems. All rights reserved.
