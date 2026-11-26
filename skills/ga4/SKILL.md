---
name: ga4
description: Use when the user asks about GA4 traffic, acquisition, pages or events in an enabled property.
---

# GA4

## Workflow

Call `google_analytics_list_properties` with `{}` and let the user select an enabled `property_id` string. For traffic use `google_analytics_traffic_overview`; for sources use `google_analytics_acquisition`; for pages use `google_analytics_landing_pages` or `google_analytics_pages`; for events use `google_analytics_events` or `google_analytics_key_events`. Each preset needs `property_id` and can take paired `start_date`/`end_date` and `limit` up to 1000. For `google_analytics_compare_periods`, supply the current start and end as YYYY-MM-DD. The previous period is the immediately preceding interval of equal length. November 8–14 compares with November 1–7. For two custom periods, use separate `google_analytics_run_report` reads with identical dimensions and metrics. GA4 events are not identical to Google Ads conversions; do not merge them without a verified link and matching definitions.

## User request

> Which landing pages drove engaged sessions last month?

## Expected answer

Property, date range, selected dimensions/metrics, observed figures, attribution limits and practical next checks.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence.

## Safety and failures

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.
