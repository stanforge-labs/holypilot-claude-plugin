---
name: campaign-overview
description: Use when the user asks to list, filter, or page through campaigns in a selected accessible advertising account. Обзор кампаний.
---

# campaign overview / HolyPilot

## English workflow

Use `list_ad_accounts` then `list_campaigns` with `{ "provider": "GOOGLE_ADS", "account_id": "<selected string>", "start_date": "YYYY-MM-DD", "end_date": "YYYY-MM-DD", "limit": 25 }`. Dates are supplied together, maximum 366 inclusive days; `limit` is 1–500. For Google Ads only, optional `statuses` is an array of ENABLED, PAUSED, REMOVED. Follow the returned `cursor` only when the user wants more rows. Explain whether the response is a partial page. If the account is manager/MCC and returns `google_ads_manager_metrics_unsupported`, request selection of a listed client account; never pick one on behalf of the user.

## Русский сценарий

Для выбранного кабинета вызовите `list_campaigns` с `provider`, строковым `account_id`, парой `start_date`/`end_date` и `limit`. По `cursor` переходите только если нужна следующая страница. Отдельно отмечайте неполную выборку и MCC-ограничение.

## User request / Пример запроса

> List the first 25 enabled campaigns last week. / Покажи первые 25 активных кампаний за прошлую неделю.

## Expected answer / Ожидаемый ответ

Account, exact dates, campaign names/statuses and available metrics, page count/cursor status, provider provenance.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence. / Для каждого численного вывода укажите ресурс, даты, валюту, источник и provenance; отделяйте факты от интерпретации.

## Safety and failures / Безопасность и ошибки

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.

Используйте только реально выданные инструменты. При MCC выберите клиентский кабинет с пользователем; при истёкшем OAuth предложите владельцу переподключение. Отсутствующие данные не заменяйте выдуманными.
