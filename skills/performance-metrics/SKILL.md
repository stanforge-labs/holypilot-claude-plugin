---
name: performance-metrics
description: Use when the user asks for spend, clicks, conversions, CPA, ROAS, or a performance breakdown from an accessible ad account. Показатели эффективности.
---

# performance metrics / HolyPilot

## English workflow

After selecting the account, call `get_basic_metrics` or `get_performance_report` with exact `provider`, string `account_id`, and required `start_date`/`end_date` (YYYY-MM-DD, at most 366 days). `get_performance_report` also reads campaigns and may fail if the selected Google account is MCC. Calculate derived ratios only from compatible returned numerators/denominators, explain zero denominator and conversion definitions, and state currency. Do not invent revenue, conversions, or ROAS.

## Русский сценарий

Укажите кабинет и обязательный период, затем получите `get_basic_metrics` или `get_performance_report`. CPA/ROAS рассчитывайте лишь при наличии совместимых фактических величин. Валюту и определения конверсии показывайте отдельно; отсутствующие значения не превращайте в нули.

## User request / Пример запроса

> How did clicks, spend, and conversions perform last month? / Как изменились клики, расход и конверсии за прошлый месяц?

## Expected answer / Ожидаемый ответ

Metric table with exact period, units/currency, tool provenance, coverage limitations and a few evidence-backed insights.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence. / Для каждого численного вывода укажите ресурс, даты, валюту, источник и provenance; отделяйте факты от интерпретации.

## Safety and failures / Безопасность и ошибки

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.

Используйте только реально выданные инструменты. При MCC выберите клиентский кабинет с пользователем; при истёкшем OAuth предложите владельцу переподключение. Отсутствующие данные не заменяйте выдуманными.
