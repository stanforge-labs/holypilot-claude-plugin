---
name: keywords
description: Use when the user asks for Google Ads positive keyword inventory and period metrics for a selected client account.
---

# Keywords

## Workflow

Select a Google Ads client, then call `google_ads_list_keywords` with `account_id` as the returned 10-digit string; optional `campaign_ids`/`ad_group_ids` are arrays of returned ID strings, optional `since` and `until` must be supplied together, `statuses` may contain ENABLED/PAUSED/REMOVED, and `limit` is 1–500. Follow `cursor` for more rows. The tool can include zero-traffic keywords: do not drop them silently. Do not recommend a pause based solely on a short window or low volume.

## User request

> Find expensive keywords with weak observed results this month.

## Expected answer

Keyword/match/status table, spend and outcomes if returned, currency, window, limitations and review suggestions only.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence.

## Safety and failures

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.
