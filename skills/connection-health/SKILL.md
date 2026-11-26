---
name: connection-health
description: Use when a HolyPilot account connection fails, access is uncertain, or the user asks whether stored status proves live access.
---

# Connection health

## Workflow

First select the account via `list_connected_resources`; then call `get_account_status` with `{ "provider": "GOOGLE_ADS", "account_id": "<selected string>" }`. For a real account this reads stored database status (`v2_database_provider_account`); a demo result has synthetic provenance. DB active does not prove live provider OAuth. The public connector does not expose live connection diagnostics. If the user also requests specific provider data, use only the relevant public READ tool for their selected account and report whether that particular request succeeded, with its returned provenance. Do not infer general connection health from stored status or a different account's result.

## User request

> What does HolyPilot know about this Google Ads connection, and can you read its campaigns for the last seven completed days?

## Expected answer

Stored DB status, source and `live_connection_checked=false`; if a separately requested provider READ succeeds, report only that operation's result and provenance. Otherwise state that live access remains unverified or provide the safe error code and next action. Do not expose credentials.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence.

## Safety and failures

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.
