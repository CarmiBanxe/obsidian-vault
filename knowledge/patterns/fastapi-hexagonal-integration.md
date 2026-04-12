---
tags: [pattern, fastapi, hexagonal, pydantic, testing]
date: 2026-04-08
related: [[sessions/2026-04-08]], [[knowledge/decisions/systemd-vs-crontab]]
il: IL-046
---
# Паттерн: FastAPI поверх Hexagonal Architecture

## Контекст
banxe-emi-stack: domain ports (Protocol ABC) → services → mock adapters.
Нужен REST слой не нарушающий гексагональный контракт.

## Решение

```
HTTP Request
    ↓
Pydantic v2 model (api/models/)      ← validation boundary
    ↓
Router function (api/routers/)       ← orchestration
    ↓
DI: Depends(get_service) → Port      ← dependency inversion
    ↓
Domain dataclass                     ← never crosses HTTP boundary
    ↓
Service / MockAdapter                ← business logic unchanged
```

## Ключевые правила

1. **Pydantic ≠ domain**: никогда не возвращать domain dataclass напрямую — только через `_result_to_response()` helper
2. **Amounts = string**: `amount: str` в Pydantic, `Decimal` в domain (I-05)
3. **Enums**: проверяй реальные enum values перед использованием — `RiskLevel.LOW = "low"` (lowercase!)
4. **DI override в тестах**: `app.dependency_overrides[get_service] = lambda: FreshInstance()` — изолирует тесты
5. **autouse fixture для reset**: service с @lru_cache нужно сбрасывать через override, не cache_clear

## Частые gotchas
- `BankAccount(holder_name=...)` → ошибка; правильно: `account_holder_name=`
- `PaymentDirection.OUT` → ошибка; правильно: `PaymentDirection.OUTBOUND`
- `KYCType.KYC` → ошибка; правильно: `KYCType.INDIVIDUAL` или `KYCType.BUSINESS`
- Unused `import pytest` в тестах без fixtures → ruff F401

## Тестовый шаблон

```python
@pytest.fixture(autouse=True)
def fresh_service():
    svc = MyService()
    app.dependency_overrides[get_my_service] = lambda: svc
    yield svc
    app.dependency_overrides.clear()
```

## Связанные заметки
- [[sessions/2026-04-08]]
