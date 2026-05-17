# Пример: dual-language planning

## English technical implementation plan

```markdown
## Technical Plan

1. Split the feature into backend, frontend, test automation, QA, and documentation subtasks.
2. Implement backend API changes behind the approved task boundary.
3. Add unit, integration, API, and regression tests.
4. Run automated tests before manual QA.
5. Hand off test results to QA for the final QA gate.
```

## Russian user_review_summary_ru

```yaml
user_review_summary_ru:
  goal: "Разбить задачу на безопасные этапы и не начинать реализацию без preflight."
  scope: "Планирование backend/frontend/test automation/QA/docs без изменения production-кода."
  changed_files: []
  not_changed:
    - "Production-код"
    - "Trello"
    - "GitHub issues/PR"
  risks:
    - "Если required agent недоступен, его часть будет заблокирована."
  tests:
    - "Автотесты должны быть выполнены до ручного QA для существующего функционала."
  test_automation_status: "Ожидается handoff к ai-test-automation-engineer."
  QA_gate_status: "Не начат; владелец ai-qa-engineer."
  required_user_check:
    - "Подтвердить русское summary и decomposition."
  next_step: "После подтверждения выполнять подзадачи по owner agents."
```

## Правило

English technical plan допустим для AI-workers. Пользователь подтверждает только русское summary.
