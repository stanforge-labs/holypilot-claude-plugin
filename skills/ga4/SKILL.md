---
name: ga4
description: Аналитика Google Analytics 4. Use when the user asks about GA4 traffic, acquisition, pages or events in an enabled property.
---

# ga4 / HolyPilot

## English workflow

Call `google_analytics_list_properties` with `{}` and let the user select an enabled `property_id` string. For traffic use `google_analytics_traffic_overview`; for sources use `google_analytics_acquisition`; for pages use `google_analytics_landing_pages` or `google_analytics_pages`; for events use `google_analytics_events` or `google_analytics_key_events`. Each preset needs `property_id` and can take paired `start_date`/`end_date` and `limit` up to 1000. For period changes use `google_analytics_compare_periods` only with its advertised live schema. GA4 events are not identical to Google Ads conversions; do not merge them without a verified link and matching definitions.

## Русский сценарий

Сначала выберите свойство через `google_analytics_list_properties`, затем вызовите тематический инструмент с `property_id` и периодом. Источники трафика, страницы и события анализируйте раздельно. События GA4 не считайте автоматически конверсиями Google Ads.

## User request / Пример запроса

> Which landing pages drove engaged sessions last month? / Какие посадочные страницы привели вовлечённые сеансы за месяц?

## Expected answer / Ожидаемый ответ

Property, date range, selected dimensions/metrics, observed figures, attribution limits and practical next checks.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence. / Для каждого численного вывода укажите ресурс, даты, валюту, источник и provenance; отделяйте факты от интерпретации.

## Safety and failures / Безопасность и ошибки

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.

Используйте только реально выданные инструменты. При MCC выберите клиентский кабинет с пользователем; при истёкшем OAuth предложите владельцу переподключение. Отсутствующие данные не заменяйте выдуманными.
