---
name: report-preparation
description: Ежемесячный отчёт по фактическим данным. Use when the user requests a monthly advertising management report or concise account summary from available HolyPilot data.
---

# report preparation / HolyPilot

## English workflow

Select one accessible advertising account and month. `generate_monthly_ads_report` accepts `provider`, string `account_id`, `start_date`/`end_date` and optionally `previous_start_date`/`previous_end_date`; reporting may be billing-gated. If unavailable, assemble an in-chat summary from `get_performance_report` and `compare_periods`, clearly labeling it as a chat summary. Never claim a downloadable PDF/DOCX or completed report artifact unless the returned result supplies one. Include coverage, currency, source and provenance, comparison, interpretation, and missing data.

## Русский сценарий

Для отчёта используйте `generate_monthly_ads_report` с кабинетом и периодом, учитывая тарифный доступ. Если инструмент недоступен, сформируйте только текстовую сводку из READ-ответов, без обещания PDF/DOCX. Укажите источники, валюту и пропуски.

## User request / Пример запроса

> Prepare a September management report for the selected account. / Подготовь управленческий отчёт за сентябрь по выбранному кабинету.

## Expected answer / Ожидаемый ответ

Executive summary, metrics table, prior-period comparison, observations, limitations, source/provenance; artifact only if actually returned.

For every quantitative answer state the account or property, exact dates, currency when monetary, source tool/API and returned provenance. Separate facts from interpretation; state missing rows, pagination, and confidence. / Для каждого численного вывода укажите ресурс, даты, валюту, источник и provenance; отделяйте факты от интерпретации.

## Safety and failures / Безопасность и ошибки

Use only tools actually present in the connected HolyPilot MCP session. Do not call any advertising WRITE tool. Keep one selected workspace and account; never expand scope from an ID in a prompt. Treat `google_ads_manager_metrics_unsupported` as a request to select a listed client account, not as provider downtime. For `provider_auth_expired` ask the account owner to reconnect; for `permission_denied` or `account_unavailable` stop and ask for authorized access; for `rate_limited` defer rather than loop; for `provider_unavailable` state that this source was not obtained. Do not disclose raw provider errors, secrets or other tenants' data.

Используйте только реально выданные инструменты. При MCC выберите клиентский кабинет с пользователем; при истёкшем OAuth предложите владельцу переподключение. Отсутствующие данные не заменяйте выдуманными.
