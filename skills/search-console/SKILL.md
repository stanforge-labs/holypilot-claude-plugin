---
name: search-console
description: Use when the user asks about organic search queries, pages, clicks, impressions or CTR from an authorized Search Console property.
---

# Search Console

## Workflow

Call `list_search_console_properties` with `{}` and let the user select a returned property. Then call `get_search_console_report` with `{ "site_url": "<exact selected property>", "days": 28 }` (`days` 1–365). Report clicks, impressions, CTR and average position only if present; distinguish query and page dimensions. Search Console numbers may differ from GA4 sessions because their measurement methods differ. Do not claim indexing, ranking cause, or a live connection from a database-only status.

## User request

> Show organic queries and pages with declining clicks over 28 days.

## Expected answer

Property, period, measured search dimensions/metrics, limitations and prioritized inspection suggestions.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence.

## Safety and failures

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.
