# Lewis Systems – Repository and Application Security Standards

**Document Version:** 1.0  
**Product Version:** 0.3.0  
**Status:** Active  
**Last Updated:** 16 November 2026

## 1. Secrets
Never commit API keys, passwords, access tokens, refresh tokens, private keys, OAuth credential references, production webhook secrets, or unredacted workflow connection metadata. Use provider-managed connections or approved secret storage. If a secret is committed, revoke or rotate it immediately; a later deletion does not remove it from Git history.

## 2. Customer and personal information
- Use synthetic data in repository examples and tests.
- Do not commit real prospect/customer names, emails, phone numbers, financial details, or form responses.
- Minimise personal information in workflow logs and staff notifications.
- Restrict Airtable, Make, Google Workspace, Gmail, and connected-app access to authorised users.
- Define retention, correction, and deletion procedures before live customer deployment.

## 3. Workflow and integration security
- Use least-privilege permissions.
- Validate inbound values before CRM writes or AI processing.
- Prevent retries from creating duplicate records or duplicate messages.
- Do not treat a sent booking link as proof of a confirmed meeting.
- Review and sanitise workflow exports before committing.

## 4. Multi-tenancy boundary
Treat the current MVP as a single-customer deployment until tenant isolation is designed, implemented, and tested. The conceptual Organization entity is not itself a security control.

## 5. Repository handling
Keep `.gitignore` current, review staged files, use synthetic test data, and avoid committing credentials, personal data, or unsanitised exports. Do not add a software licence without an explicit legal/business decision.

## 6. Incident response
1. Restrict access to the affected resource where possible.
2. Revoke or rotate exposed credentials immediately.
3. Identify affected commits, files, integrations, and data.
4. Remove exposed Git history if necessary, coordinating with collaborators.
5. Assess notification obligations for affected account or customer owners.
6. Record corrective actions without reproducing the secret.

Review before the first external pilot and after material changes to hosting, AI processing, authentication, or tenant architecture.
