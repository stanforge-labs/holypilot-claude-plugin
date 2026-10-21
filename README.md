# HolyPilot for Claude — v1.0.0

HolyPilot is a HolyMedia product for company and agency workflows across authorized advertising and analytics resources. This plugin pairs 15 bilingual analytical Skills with HolyMedia's existing remote, OAuth-protected MCP connector. It is an independent third-party plugin, not an Anthropic product or Anthropic endorsement.

The bundle contains human-readable Markdown, JSON and the official SVG mark only. It does not run local code, install packages, collect Claude conversation history, or contain credentials. HolyMedia operates the remote service at `https://mcp.holymedia.kz/mcp/public`.

## What it can do / Возможности

| Workflow / Сценарий | Skills |
| --- | --- |
| Select accessible accounts, diagnose connections / Выбор ресурсов и диагностика | `account-selection`, `connection-health` |
| List, inspect and analyze campaigns / Обзор и анализ кампаний | `campaign-overview`, `campaign-analysis` |
| Explain results, spend and period changes / Метрики, расходы и сравнение | `performance-metrics`, `spend-and-budgets`, `period-comparison` |
| Review Google Ads queries and keywords / Ключи, запросы и минус-слова | `keywords`, `search-terms`, `negative-keywords` |
| Prioritize observations and prepare management reports / Приоритеты и отчёты | `optimization-opportunities`, `report-preparation` |
| Analyze connected Meta, GA4 and Search Console / Meta, GA4 и SEO | `meta-ads`, `ga4`, `search-console` |

Availability depends on the authenticated workspace, provider connection, billing entitlement and tools actually exposed in the current session. Listing an account is a database read, not proof that live provider OAuth works. A Google Ads manager (MCC) account cannot provide client campaign metrics directly; select an authorized client account explicitly. TikTok Ads and Yandex Direct can appear in account inventory, but this plugin makes no claim that their live campaign reads have passed provider acceptance.

## Install and connect / Установка и подключение

1. In Claude chat, open **Customize → Plugins → Add → Upload plugin**, and select a ZIP containing the `holypilot` folder. In Claude Code, use `claude --plugin-dir ./holypilot` from this repository. Cowork uses the same plugin upload when available in the account.
2. Open the plugin's **Connectors** tab. Add/connect **HolyPilot** if it is not connected. The MCP URL is `https://mcp.holymedia.kz/mcp/public`; sign in through the browser OAuth flow and grant only the scopes shown for your own account. Do not paste tokens into Claude or into this package.
3. Confirm the connector shows **Connected**. Ask “Which advertising accounts can I access in my HolyPilot workspace?” Select a specific account before requesting metrics. For a Google Ads MCC, select a client account from your own authorized inventory.
4. Ask a dated READ question. Verify the returned account, period, currency, provenance and limitations. A failed provider call should be reported by its safe machine code, not disguised as a successful report.

Русский порядок: установите ZIP в **Настроить → Плагины**, подключите HolyPilot на вкладке коннекторов, войдите в собственную учётную запись через OAuth, затем запросите список доступных кабинетов. Выберите конкретный клиентский аккаунт и период до запроса метрик. Пароли и OAuth-токены не передавайте в чат.

## Three reviewer workflows / Три сценария для проверки

These require an authorized reviewer account with isolated **synthetic** data. No live customer account is needed for review. Expected result descriptions are contracts, not fabricated example numbers.

1. **Inventory and status.** Ask: “List the advertising accounts I can access and check the selected account's status.” Expected calls: `list_connected_resources` or `list_ad_accounts`, then `get_account_status` with exact `provider` and string `account_id`. The answer distinguishes `v2_database_provider_account` status from live provider connectivity. / Список кабинетов и статус БД, без ложного подтверждения OAuth.
2. **Campaign READ.** Ask: “Show five campaigns in the selected Google Ads client account for the last seven completed days; include dates and currency.” Expected call: `list_campaigns` with selected client `account_id`, `provider: GOOGLE_ADS`, paired `start_date`/`end_date`, `limit: 5`. The answer reports pagination and provenance. MCC metrics error must prompt client selection; it must not silently switch account. / Пять кампаний только выбранного клиента, без WRITE.
3. **Analytical summary.** Ask: “Compare two consecutive periods for that account and prepare a short management summary using only returned data.” Expected calls: `compare_periods` and, if available, `generate_monthly_ads_report` or `get_performance_report`. The response separates observed metrics from interpretation, says whether a real report artifact was returned, and does not invent PDF/DOCX output. / Сравнение периодов и управленческая сводка по фактическим данным.

Additional provider-specific Skills need their respective connected demo provider or remain unverified at provider level; synthetic offline tests do not establish live Meta, GA4 or Search Console availability.

## Safe interpretation and failures / Безопасность и ошибки

The 15 plugin Skills use advertising and analytics READ workflows and do not invoke advertising WRITE. `run_connection_diagnostics` performs a live provider check and can refresh and persist an expiring OAuth credential server-side; its MCP annotations correctly do not mark it read-only or idempotent. The public registry may also include gated Meta preview/commit tools in other configurations. Production Google Ads WRITE remains disabled. The v0.1 preview and change-verification guidance is retained here: any future supported change requires a server-created preview, separate OWNER browser approval, and a later explicit one-time commit. Claude's permission prompt never replaces HolyPilot approval. Do not retry an uncertain commit blindly. None of this grants permission to change advertising data through v1.0.0.

When `google_ads_manager_metrics_unsupported` is returned, choose an authorized client account with the user. `provider_auth_expired` requires reconnection by the account owner; `permission_denied` requires an authorized grant; `account_unavailable` requires checking workspace/account selection; `rate_limited` calls for a later READ; `provider_unavailable` means the requested source was not obtained. Do not fabricate data or leak raw upstream error payloads. Always state currency for monetary values, exact dates, returned `provenance`, pagination coverage and data limits. A recommendation is an interpretation, not a provider mutation or proven cause.

При ошибке MCC не подбирайте дочерний аккаунт автоматически. Если OAuth истёк, попросите владельца переподключить источник. Если прав нет, остановите запрос. Неполную пагинацию и отсутствие данных отмечайте явно.

## Data and privacy / Данные и конфиденциальность

The remote MCP service receives authenticated requests and returns only data authorized for the user's HolyPilot workspace. Depending on the selected tool, this can include account names/IDs, campaigns, spend, performance, search terms, GA4 traffic and Search Console queries/pages. HolyPilot stores accounts, connections, reports and security records on its service under its published retention policy; OAuth credentials are stored server-side and are not included in the plugin or MCP responses. Claude receives requested tool results when a connected user asks it to process them. The plugin's instructions themselves send data to no additional endpoint.

HolyMedia's [Privacy Policy](https://mcp.holymedia.kz/privacy) explains collection, retention, revocation and deletion requests. [Terms](https://mcp.holymedia.kz/terms) govern use. [Support](https://mcp.holymedia.kz/support) and `mcp@holymedia.kz` handle product/security concerns. These published policies use purpose-based retention rather than a fixed number of days; do not enter a numerical retention period in a directory form without owner/legal verification. Disconnect a provider in HolyPilot or revoke its grant with that provider; ask support for account deletion. Use Anthropic's own privacy terms for Claude-side processing.

## Troubleshooting / Помощь

If the connector is not connected, complete browser OAuth. If accounts are absent, check the current workspace and connection in HolyPilot. If campaign metrics fail for an MCC, select an accessible client account. If the tool is missing or returns `billing_unavailable` or `quota_exceeded`, do not bypass the entitlement. If data is empty, report an empty result rather than a zero-valued finding. For help, contact [HolyPilot Support](https://mcp.holymedia.kz/support) without sending passwords, tokens or customer exports.

The `LICENSE` is HolyMedia's existing v0.1.0 bundle license, explicitly confirmed by the owner for this release. The HolyPilot name and mark remain HolyMedia property.
