
# Release Notes Sample
A clean, scannable changelog demonstrating semantic versioning and categorization.

```markdown
# Release Notes

## Version 2.4.0
**Release Date:** October 24, 2026

### 🚀 New Features
* **Webhooks Dashboard:** You can now monitor webhook delivery statuses, view request payloads, and manually retry failed events directly from the Developer Console.
* **Idempotency Keys:** The Payments API now supports `Idempotency-Key` headers to safely retry requests without accidentally performing the same operation twice.

### 🐛 Bug Fixes
* **Data Migration:** Resolved an issue where legacy database migrations from Oracle to SQL Server occasionally dropped the `timestamp` column on batched uploads.
* **Authentication:** Fixed a token-refresh bug that caused active sessions to timeout prematurely after 24 hours instead of the configured 48 hours.

### ⚠️ Deprecations
* The `GET /v1/charges` endpoint is now officially deprecated. Please migrate to the `GET /v1/payment_intents` endpoint by Q1 2027.
