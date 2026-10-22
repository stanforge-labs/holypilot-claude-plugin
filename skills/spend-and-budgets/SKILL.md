---
name: spend-and-budgets
description: Расходы и бюджеты без изменения ставок. Use when a user asks how much an account spent or which campaigns may need budget attention; read-only planning.
---

# spend and budgets / HolyPilot

## English workflow

Call `get_spend_overview` with the selected `provider`, string `account_id`, and optionally `start_date`/`end_date` together. Use `get_campaign_structure` for a specific `campaign_id` if budget configuration is needed. Report observed spend separately from budget settings; estimate remaining budget only if the returned data and time basis allow it, labeling the estimate. Do not call budget preview or commit tools and never imply a recommended budget has been applied.

## Русский сценарий

Запросите `get_spend_overview` для выбранного кабинета и периода; при необходимости прочитайте структуру отдельной кампании. Фактический расход и установленный бюджет — разные величины. Рекомендации не являются изменениями.

## User request / Пример запроса

> Show spending pressure this month without changing budgets. / Покажи расход и возможные риски бюджета без изменений.

## Expected answer / Ожидаемый ответ

Spend facts, dates/currency, budget context if present, labeled estimates, recommended human review.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence. / Для каждого численного вывода укажите ресурс, даты, валюту, источник и provenance; отделяйте факты от интерпретации.

## Safety and failures / Безопасность и ошибки

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.

Используйте только реально выданные инструменты. При MCC выберите клиентский кабинет с пользователем; при истёкшем OAuth предложите владельцу переподключение. Отсутствующие данные не заменяйте выдуманными.
