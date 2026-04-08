---
tags: [decision, systemd, crontab, safeguarding, fca, cass-15]
date: 2026-04-08
related: [[sessions/2026-04-08]], [[knowledge/patterns/spec-first-methodology]]
il: IL-043
---
# ADR: systemd timer вместо crontab для Safeguarding Recon

## Контекст
FCA CASS 7.15.17R требует ежедневной автоматической сверки safeguarding счетов.
Предыдущее решение: crontab entry в `deploy-sprint9.sh`.

## Проблема с crontab
- При пропуске запуска (сервер был недоступен) → задача теряется, нет retry
- Нет journald audit trail (FCA требует доказуемость)
- Нет зависимостей от других сервисов (ClickHouse должен быть запущен)

## Решение: systemd timer
```ini
[Timer]
OnCalendar=Mon-Fri *-*-* 07:00:00 UTC
Persistent=true          # Запуск при пропуске (FCA audit requirement)
RandomizedDelaySec=120   # Нет thundering herd
```

## Преимущества
- `Persistent=true`: при пропуске (сервер был down) → запуск при следующем старте
- `After=clickhouse-server.service`: гарантия порядка запуска
- `journald`: полный audit trail (FCA CASS 7.15.29R)
- Exit codes 0/1/2/3 → systemd знает что считать успехом
- `SuccessExitStatus=0 1 2`: только код 3 (FATAL infra) = failure

## Результат
- Timer активен: `banxe-recon.timer` — active (waiting), следующий: 07:00 UTC Thu
- Tests: 13/13 PASS
- FCA compliance: CASS 7.15.17R ✅, CASS 7.15.29R (n8n pending) ⏳
