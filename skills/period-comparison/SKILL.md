---
name: period-comparison
description: Сравнение периодов. Use when the user requests a comparison of two advertising periods for the same selected account.
---

# period comparison / HolyPilot

## English workflow

Call `compare_periods` with `provider`, string `account_id`, `current_start_date`, `current_end_date`, `previous_start_date`, `previous_end_date`. Each inclusive range must be valid and no longer than 366 days. Select comparable lengths and explain when seasonality or attribution makes comparison weak. Use the returned `changes` and metrics; do not infer causal impact from coincident changes.

## Русский сценарий

Для `compare_periods` передайте четыре даты с префиксами `current_` и `previous_`, а также точные provider/account_id. Сравнивайте однотипные интервалы и поясняйте ограничения атрибуции и сезонности.

## User request / Пример запроса

> Compare this 7-day period with the preceding 7 days. / Сравни последние 7 дней с предыдущими 7 днями.

## Expected answer / Ожидаемый ответ

Two dated columns, absolute and relative changes where computable, currency, provenance, non-causal interpretation.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence. / Для каждого численного вывода укажите ресурс, даты, валюту, источник и provenance; отделяйте факты от интерпретации.

## Safety and failures / Безопасность и ошибки

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.

Используйте только реально выданные инструменты. При MCC выберите клиентский кабинет с пользователем; при истёкшем OAuth предложите владельцу переподключение. Отсутствующие данные не заменяйте выдуманными.
