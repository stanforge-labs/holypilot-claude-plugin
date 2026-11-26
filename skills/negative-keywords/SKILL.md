---
name: negative-keywords
description: Use when reviewing existing Google Ads negative keywords or checking a proposed negative for conflicts, without writing.
---

# Negative keywords

## Workflow

Call `google_ads_list_negatives` with selected 10-digit string `account_id`; optional `campaign_ids`, `levels` (campaign, ad_group, shared_list), `limit` 1–500, and `cursor`. For a proposed negative supplied by the user, `google_ads_check_negative_conflicts` requires `account_id`, `campaign_ids` and `negatives` (array of `{text, match_type}` where match_type is BROAD, PHRASE or EXACT). Explain match type and conflict results; never add a negative automatically. A conflict check is READ only, not a preview or commit.

## User request

> Would adding the phrase negative “free trial” conflict with enabled keywords?

## Expected answer

Existing negative inventory, conflict findings and scope, with a clearly uncommitted recommendation.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence.

## Safety and failures

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.
