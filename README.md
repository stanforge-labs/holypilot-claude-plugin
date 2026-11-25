# HolyPilot for Claude

HolyMedia maintains this guide for the remote **HolyMedia MCP Connector**, listed in Claude as **HolyPilot**, and for the separate **HolyPilot Claude Plugin Bundle**. The connector gives Claude read access to the marketing accounts and analytics properties you have connected to HolyPilot. The plugin adds 15 marketing Skills and a configuration for that same connector.

## HolyMedia MCP Connector

### Connect and choose an account

1. In Claude, open **Settings → Connectors**, select **HolyPilot** and choose **Connect**. Where custom connectors are available, the remote HTTP URL is `https://mcp.holymedia.kz/mcp/public`.
2. Sign in to HolyPilot in the browser. Review the workspace and the public connector's `adforge:mcp:read` permission. Existing workspace membership, provider access and reporting entitlements determine which resources can be read. Keep provider passwords and OAuth tokens out of chat.
3. Ask “Which advertising accounts and analytics properties can I access?” Choose the returned account or property by name. For Google Ads campaign metrics, select a client account under the manager account.
4. Ask a question about that resource. Specify dates and the business outcome you want to measure. Reports identify the source, currency and reporting period. Missing conversions, withheld queries and incomplete pages affect what a comparison can establish.

### Primary use cases

- “Which five campaigns in my Google Ads account drove the most conversions over the last seven completed days?”
- “Compare spend, clicks and cost per click in my Meta Ads account across the last two completed 14-day periods.”
- “Which campaigns spent the most last month with few reported conversions? Show the numbers behind each finding.”
- “Prepare a monthly marketing report for my account. Summarize spend, conversions and the largest changes from the previous month.”
- “Which landing pages had the most sessions in my connected GA4 property last month?”

### Supported sources and operations

| Source | What you can read |
| --- | --- |
| Google Ads | Campaign performance, spend, conversions, keywords, search terms and existing negatives. You can also check a proposed negative for conflicts. |
| Meta Ads | Account and campaign insights and available permission information for the selected ad account. |
| Google Analytics 4 | Acquisition, landing pages, events, property metadata and reports with compatible dimensions and metrics. |
| Google Search Console | Search traffic for an authorized site, including available query and page data. |

TikTok Ads and Yandex Direct may appear in account inventory. Provider-backed flexible insights are available for Google Ads and Meta Ads. The public catalog reviewed for this version exposed 41 read-only tools. It offers no ad creation, bid changes or campaign pausing. `get_account_status` reads stored status. `run_connection_diagnostics` can refresh and persist credentials and is outside this public catalog.

### Advertising insights

For `get_flexible_insights`, supply `provider` and the exact string `account_id` selected from the workspace. The public schema lists `GOOGLE_ADS`, `META_ADS`, `TIKTOK_ADS` and `YANDEX_DIRECT`. The two reporting adapters documented above serve live insights. Inventory visibility alone does not establish reporting support.

| Optional input | Meaning |
| --- | --- |
| `start_date`, `end_date` | Preferred pair of inclusive calendar dates in `YYYY-MM-DD` format. The range is 1–366 days. |
| `since`, `until` | Alternative complete pair with the same limits. On Google Ads and Meta Ads these take precedence if both complete pairs are supplied. The synthetic reviewer rejects mixed pairs. Send just one pair. |
| `date_preset` | Alternative to explicit dates. Use `last_7d`, `last_14d` or `last_30d`; combining a preset with explicit dates is rejected. With no dates, provider-backed reads default to the last 30 completed UTC days. The synthetic reviewer fixture defaults to 14. |
| `level`, `campaign_id` | The default level is `account`; `campaign` requests rows. An optional campaign ID can narrow Meta insights or Google aggregate metrics. Google campaign-level listing pages through the account's campaigns and does not apply this filter. |
| `limit`, `cursor` | Page size 1–500 and an opaque cursor returned by a previous page. Use these for paginated rows. |
| `connection_id` | Optional Google Ads connection UUID bound to the selected account and workspace, useful when several authorized connections contain that account. |

Example arguments using a placeholder for the selected account:

```json
{"provider":"META_ADS","account_id":"<selected-account-id>","level":"campaign","start_date":"2026-11-01","end_date":"2026-11-14","limit":25}
```

Meta returns dated rows in `items`, the period, the level and information on returned metrics. Google returns an aggregate at account level or campaign `items` with available metrics, currency, provenance and a `nextCursor` when another page exists. Preserve missing metrics as missing. Custom `metrics` and `breakdowns` are not inputs of this public tool.

### Compare GA4 periods

`google_analytics_compare_periods` requires one enabled `property_id` as a string. Supply the optional `start_date` and `end_date` together in `YYYY-MM-DD` format for the **first (current) period**. Omitting both selects the last 30 completed UTC days for a live property. The synthetic reviewer fixture defaults to 14.

The **second (previous) period** ends the day before the current period starts and has the same inclusive length. The published schema has no second start or end parameter. For two independently chosen periods, use `google_analytics_run_report` once per range with the same property, dimensions and metrics.

```json
{"property_id":"<property-id>","start_date":"2026-11-08","end_date":"2026-11-14","metrics":["sessions"],"dimensions":["landingPage"],"limit":25}
```

This compares November 8–14 with November 1–7. The result identifies the property and carries both `current` and `previous` reports. Optional `dimensions` (up to 9), `metrics` (up to 10) and `limit` (1–1000) apply to both reports. Use compatible dimensions and metrics. The published schema also lists singular `dimension`; this comparison reads the plural `dimensions` array.

### Data, troubleshooting and disconnecting

Claude receives the results of authorized tool calls. Depending on the question, these may contain account names, campaign results, search terms or analytics data. HolyPilot manages provider credentials on the server. A stored connection status cannot confirm a live provider request. An empty result and zero measured conversions have different meanings.

If an account is missing, check the signed-in workspace and selected provider. For `provider_auth_expired`, the connection owner can reconnect in HolyPilot. For `permission_denied`, check the workspace grant. For `quota_exceeded` or `billing_unavailable`, check the reporting entitlement. For `rate_limited`, try again later. Report the safe error code to support without tokens or customer exports.

To stop Claude access, disconnect HolyPilot in Claude's connector settings. To disconnect an underlying data source, remove that connection in HolyPilot or revoke the provider grant with the provider. Removing the plugin removes its Skills from that client. HolyMedia handles support, privacy and deletion requests through its published channels. [Support](https://mcp.holymedia.kz/support) · [Privacy policy](https://mcp.holymedia.kz/privacy) · [Terms](https://mcp.holymedia.kz/terms)

## Claude Plugin Bundle

Install the bundle when you want the 15 guided workflows. In Claude Code, open the downloaded repository folder and start `claude --plugin-dir .`. In clients that support plugin uploads, choose **Customize → Plugins → Add → Upload plugin** and select the packaged plugin. Connect **HolyPilot** through the browser when prompted. The bundle discovers its remote HTTP server from the root `.mcp.json`. Installing the standalone connector supplies the tools only.

| Task | Skills |
| --- | --- |
| Choose an accessible resource and interpret stored status | `account-selection`, `connection-health` |
| Browse campaigns and investigate performance | `campaign-overview`, `campaign-analysis`, `performance-metrics` |
| Review spending and compare reporting windows | `spend-and-budgets`, `period-comparison` |
| Review search campaigns | `keywords`, `search-terms`, `negative-keywords` |
| Prioritize findings and prepare reports | `optimization-opportunities`, `report-preparation` |
| Analyze a connected source | `meta-ads`, `ga4`, `search-console` |

Ask in your preferred language, for example “Prepare a report on last month's campaign spending.” The report Skill summarizes the returned data and states any coverage limits. The monthly report tool returns its report in the response.

### Reviewer test instructions

Use the isolated synthetic reviewer workspace. Ask for accessible accounts, select the demo client explicitly, list five campaigns for a specified week, then compare two stated periods. Confirm the selected resource, dates and returned synthetic provenance in each result. Keep synthetic results separate from live provider results.

### Release notes · 1.0.2

Removed the unused SVG and retained the declared PNG icon. Added HolyMedia's connector guide, user-facing use cases and examples for advertising and GA4 period comparisons. Updated the English metadata and instructions for all 15 Skills. The MCP endpoint and OAuth scope are unchanged.
