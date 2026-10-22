---
name: campaign-analysis
description: Анализ конкретной кампании. Use when a user asks why a selected advertising campaign performed as it did or wants campaign-level observations.
---

# campaign analysis / HolyPilot

## English workflow

Select an account and campaign from `list_ad_accounts` and `list_campaigns`; then call `get_campaign` with `{ "provider": "GOOGLE_ADS", "account_id": "<selected string>", "campaign_id": "<returned string>", "start_date": "YYYY-MM-DD", "end_date": "YYYY-MM-DD" }`. When needed, `get_campaign_structure` takes the same provider/account_id/campaign_id. Use `get_basic_metrics` only with a selected account and required start_date/end_date. Do not treat campaign structure or status as evidence of performance. Identify observations, interpretations and missing evidence separately.

## Русский сценарий

Выберите кабинет и кампанию из READ-ответов. Для `get_campaign` передайте точные `provider`, `account_id`, `campaign_id` и период; для структуры используйте `get_campaign_structure`. Отделяйте факты метрик от гипотез о причинах.

## User request / Пример запроса

> Analyze the selected campaign for the last 14 days; what changed? / Разбери выбранную кампанию за 14 дней: что изменилось?

## Expected answer / Ожидаемый ответ

Account/campaign, dates and currency; observed metrics, supported comparison, cautious hypotheses, next read-only check.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence. / Для каждого численного вывода укажите ресурс, даты, валюту, источник и provenance; отделяйте факты от интерпретации.

## Safety and failures / Безопасность и ошибки

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.

Используйте только реально выданные инструменты. При MCC выберите клиентский кабинет с пользователем; при истёкшем OAuth предложите владельцу переподключение. Отсутствующие данные не заменяйте выдуманными.
