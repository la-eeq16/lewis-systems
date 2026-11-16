# n8n Future Migration Plan

**Document Version:** 1.0  
**Product Version:** 0.3.0  
**Status:** Future option – not current MVP implementation  
**Last Updated:** 16 November 2026

## 1. Purpose

Define the conditions and safeguards for considering a future migration of ClientPilot workflows from Make to n8n.

## 2. Current decision

Make is the selected automation platform for the current MVP. n8n is not the current execution platform. Existing n8n material under [the legacy module directory](../../module-03-n8n/README.md) is retained for historical reference and must not be read as evidence of a deployed n8n implementation.

## 3. Migration triggers

Reconsider n8n only when a concrete business or technical reason exists, such as:
- Make operating costs materially constrain delivery or margins.
- A client requirement needs capabilities or control not practical in Make.
- Hosting, data residency, or deployment control justifies the operational burden.
- The team can support n8n maintenance, monitoring, backups, upgrades, and security.

A migration should not be undertaken merely because another platform is available.

## 4. Migration prerequisites

- Stable, tested platform-independent workflow specifications.
- Versioned and verified Make scenario exports.
- Documented field mappings and business rules.
- Representative synthetic test fixtures.
- Defined error, retry, idempotency, and logging behaviour.
- Cost and operational comparison, including hosting and maintenance.
- A rollback plan and a period of controlled parallel validation where appropriate.

## 5. Migration approach

1. Reconfirm the business case and target hosting model.
2. Map each Make workflow to n8n nodes and credentials by environment.
3. Rebuild WF-001A and WF-001B without changing business rules unintentionally.
4. Run both implementations against the same synthetic test cases.
5. Compare records, scores, statuses, error behaviour, and notifications.
6. Validate duplicate prevention and recovery.
7. Obtain acceptance before switching production triggers.
8. Retain a rollback path until the new implementation is stable.

## 6. Security and operations

Use environment-managed credentials, least-privilege service accounts, protected webhook endpoints, secure backups, monitored execution logs, and documented upgrade procedures. Never commit credentials or production customer data.

## 7. Decision record

No migration date or commitment is approved. Revisit this plan only after a documented cost, client, or technical trigger is met.

---

© Lewis Systems. All rights reserved.
