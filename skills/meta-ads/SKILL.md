---
name: meta-ads
description: Use when the user requests Meta Ads campaign or insights analysis from an authorized connected Meta account. Аналитика Meta Ads.
---

# meta ads / HolyPilot

## English workflow

Select a Meta account via `list_ad_accounts` with `{ "provider": "META_ADS" }`; use `get_meta_oauth_permissions` with `{ "account_id": "<selected string>" }` if access needs explanation. `get_meta_ads_detailed_report` reads the selected account and report type only as shown in its live schema; otherwise prefer `get_performance_report` with `provider: META_ADS`, string `account_id`, and required dates. `get_flexible_insights` supports `level: account | campaign` and provider-specific filters. Do not assume Business, Page or Instagram permissions from ad-account access alone. The public plugin performs READ; it does not create or modify Meta campaigns.

## Русский сценарий

Выберите Meta-кабинет, при проблемах прочитайте `get_meta_oauth_permissions`. Для показателей передайте `provider: META_ADS`, строковый `account_id` и период в `get_performance_report`; расширенные breakdowns используйте только по текущей схеме `get_flexible_insights`. Не смешивайте разрешения Business/Page/Instagram.

## User request / Пример запроса

> Summarize Meta campaign performance for the selected account. / Сводка эффективности Meta по выбранному кабинету.

## Expected answer / Ожидаемый ответ

Account and authorization scope, dated metrics with currency, breakdown limitations and grounded recommendations.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence. / Для каждого численного вывода укажите ресурс, даты, валюту, источник и provenance; отделяйте факты от интерпретации.

## Safety and failures / Безопасность и ошибки

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.

Используйте только реально выданные инструменты. При MCC выберите клиентский кабинет с пользователем; при истёкшем OAuth предложите владельцу переподключение. Отсутствующие данные не заменяйте выдуманными.
