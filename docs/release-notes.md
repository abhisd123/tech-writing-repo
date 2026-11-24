
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

!!! info "Important Release Notices"
    Please review the following items before deploying version 2.4.0 to your production environment:

    1. **Known Issue & Workaround:** If your Oracle to SQL Server migration hangs at 99% during a batched upload, manually restarting the background worker service will force the final commit to execute. A permanent fix is scheduled for v2.4.1.
    2. **Upcoming Deprecation:** The `GET /v1/charges` endpoint will be fully retired in the next major release (expected Q1 2027). Please migrate your integration to `GET /v1/payment_intents` to prevent future service disruptions.
    3. **Phased Rollout:** The new Webhooks Dashboard is currently rolling out gradually across all server regions. If you do not see the dashboard in your Developer Console today, it will be available by Friday.
    4. **Pro Tip (Faster Bulk Uploads):** With the new batching engine introduced in this release, you can now send up to 1,000 records per API request instead of 100. Update your payload limits to take advantage of the reduced latency.
