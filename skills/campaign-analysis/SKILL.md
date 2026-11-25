---
name: campaign-analysis
description: Use when a user asks why a selected advertising campaign performed as it did or wants campaign-level observations.
---

# Campaign analysis

## Workflow

Select an account and campaign from `list_ad_accounts` and `list_campaigns`; then call `get_campaign` with `{ "provider": "GOOGLE_ADS", "account_id": "<selected string>", "campaign_id": "<returned string>", "start_date": "YYYY-MM-DD", "end_date": "YYYY-MM-DD" }`. When needed, `get_campaign_structure` takes the same provider/account_id/campaign_id. Use `get_basic_metrics` only with a selected account and required start_date/end_date. Do not treat campaign structure or status as evidence of performance. Identify observations, interpretations and missing evidence separately.

## User request

> Analyze the selected campaign for the last 14 days; what changed?

## Expected answer

Account/campaign, dates and currency; observed metrics, supported comparison, cautious hypotheses, next read-only check.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence.

## Safety and failures

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.
