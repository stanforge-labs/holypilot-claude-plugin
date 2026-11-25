---
name: optimization-opportunities
description: Use when the user wants a ranked list of advertising optimization opportunities grounded in actual HolyPilot READ data.
---

# Optimization opportunities

## Workflow

Select one account, then use `get_top_performers` with `provider`, string `account_id`, `metric` (spend, impressions, clicks, conversions, conversionValue), and `limit` 1–100. Cross-check with `get_performance_report` or `get_basic_metrics` for a dated period. Rank opportunities by observed impact and confidence, not by an invented score. Distinguish spend concentration, quality, and tracking gaps. A high spend alone does not establish waste or causation. No preview or commit is available through this READ workflow.

## User request

> Where should our analyst look first this week?

## Expected answer

Ranked observations, evidence, confidence/limitations and next read-only checks; no claimed automatic optimization.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence.

## Safety and failures

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.
