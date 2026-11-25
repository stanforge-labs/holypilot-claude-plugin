---
name: search-terms
description: Use when the user asks which real Google Ads search queries triggered ads and where spend may be wasted.
---

# Search terms

## Workflow

Call `google_ads_search_terms` for the selected Google Ads client with `{ "account_id": "<10-digit string>", "since": "YYYY-MM-DD", "until": "YYYY-MM-DD", "limit": 100, "format": "json" }`. Optional `campaign_ids`, `min_cost`, `contains`, `only_not_added`, and `cursor` follow the advertised schema. CSV file delivery is unavailable: use JSON pagination only. Search terms may be privacy-limited and the response may omit triggered keyword attribution; disclose both. Suggestions for negatives are not write operations.

## User request

> Review costly search terms not yet added as keywords.

## Expected answer

Query evidence with spend/outcomes if returned, exact dates and currency, coverage, candidate actions as uncommitted suggestions.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence.

## Safety and failures

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.
