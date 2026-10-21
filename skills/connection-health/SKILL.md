---
name: connection-health
description: Use when a HolyPilot account connection fails, access is uncertain, or the user asks whether data is live. Диагностика подключения.
---

# connection health / HolyPilot

## English workflow

First select the account via `list_connected_resources`; then call `get_account_status` with `{ "provider": "GOOGLE_ADS", "account_id": "<selected string>" }`. This is a database status, with source `v2_database_provider_account`; DB active does not prove live provider OAuth. If asked for a live check, call `run_connection_diagnostics` with the same provider and account_id only when authorized and available. Distinguish database inventory from a successful provider response and give the returned provenance.

## Русский сценарий

Сначала выберите ресурс, затем вызовите `get_account_status` с точным `provider` и строковым `account_id`. Статус БД не означает действующий OAuth. Только успешный `run_connection_diagnostics` подтверждает отдельную проверку провайдера; укажите источник результата.

## User request / Пример запроса

> Is this Google Ads connection working now? / Работает ли сейчас это подключение Google Ads?

## Expected answer / Ожидаемый ответ

DB status and any separate live diagnostic, timestamps, safe error code, next action; do not expose credentials.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence. / Для каждого численного вывода укажите ресурс, даты, валюту, источник и provenance; отделяйте факты от интерпретации.

## Safety and failures / Безопасность и ошибки

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.

Используйте только реально выданные инструменты. При MCC выберите клиентский кабинет с пользователем; при истёкшем OAuth предложите владельцу переподключение. Отсутствующие данные не заменяйте выдуманными.
