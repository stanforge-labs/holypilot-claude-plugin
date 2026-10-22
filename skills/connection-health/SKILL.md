---
name: connection-health
description: Состояние подключения. Use when a HolyPilot account connection fails, access is uncertain, or the user asks whether stored status proves live access.
---

# connection health / HolyPilot

## English workflow

First select the account via `list_connected_resources`; then call `get_account_status` with `{ "provider": "GOOGLE_ADS", "account_id": "<selected string>" }`. This reads stored database status, with source `v2_database_provider_account`; DB active does not prove live provider OAuth. The public connector does not expose live connection diagnostics. If the user also requests specific provider data, use only the relevant public READ tool for their selected account and report whether that particular request succeeded, with its returned provenance. Do not infer general connection health from stored status or a different account's result.

## Русский сценарий

Сначала выберите ресурс через `list_connected_resources`, затем вызовите `get_account_status` с точным `provider` и строковым `account_id`. Статус БД не означает действующий OAuth. Публичный коннектор не предоставляет live-диагностику. Если пользователь также просит конкретные данные провайдера, используйте соответствующий публичный READ-инструмент только для выбранного аккаунта и сообщите результат именно этого запроса и его provenance. Не делайте вывод о живом подключении по статусу БД или другому аккаунту.

## User request / Пример запроса

> What does HolyPilot know about this Google Ads connection, and can you read its campaigns for the last seven completed days? / Какой статус этого Google Ads подключения хранится в HolyPilot и доступны ли кампании за последние семь завершённых дней?

## Expected answer / Ожидаемый ответ

Stored DB status, source and `live_connection_checked=false`; if a separately requested provider READ succeeds, report only that operation's result and provenance. Otherwise state that live access remains unverified or provide the safe error code and next action. Do not expose credentials.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence. / Для каждого численного вывода укажите ресурс, даты, валюту, источник и provenance; отделяйте факты от интерпретации.

## Safety and failures / Безопасность и ошибки

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.

Используйте только реально выданные инструменты. При MCC выберите клиентский кабинет с пользователем; при истёкшем OAuth предложите владельцу переподключение. Отсутствующие данные не заменяйте выдуманными.
