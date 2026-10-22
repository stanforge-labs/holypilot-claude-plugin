---
name: account-selection
description: Выбор доступного кабинета или ресурса. Use when a user needs to find and select one accessible HolyPilot workspace advertising account or analytics resource before analysis.
---

# account selection / HolyPilot

## English workflow

Call `list_connected_resources` with `{}` to inventory only the authenticated workspace. For advertising accounts, `list_ad_accounts` accepts `{}` or `{ "provider": "GOOGLE_ADS" | "META_ADS" | "TIKTOK_ADS" | "YANDEX_DIRECT" }`. Show the provider, display name, exact returned `account_id` as a string, and any returned account type. Ask the user to choose when several accounts match. A manager/MCC Google Ads account is not a client metrics account; never select a child account automatically. Do not infer access from an ID supplied in chat.

## Русский сценарий

Получите `list_connected_resources` с `{}` для текущего workspace. Для рекламы используйте `list_ad_accounts` с `{}` либо допустимым `provider`. Покажите доступные названия и типы; если кандидатов несколько, попросите выбрать. `account_id` всегда строка. MCC не подменяйте дочерним кабинетом автоматически.

## User request / Пример запроса

> Which Google Ads client account in my workspace can I analyze? / Какой клиентский Google Ads кабинет моего workspace можно анализировать?

## Expected answer / Ожидаемый ответ

A short selection table: provider, account, type, eligibility for metrics, source tool; no cross-workspace data and no guessed ID.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence. / Для каждого численного вывода укажите ресурс, даты, валюту, источник и provenance; отделяйте факты от интерпретации.

## Safety and failures / Безопасность и ошибки

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.

Используйте только реально выданные инструменты. При MCC выберите клиентский кабинет с пользователем; при истёкшем OAuth предложите владельцу переподключение. Отсутствующие данные не заменяйте выдуманными.
