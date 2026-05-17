# Request Allowed

## Запрос

`ai-backend-developer`, исправь approved task `TASK-42` в parent epic `ЭПИК-04`. Статус карточки: `Готово к разработке`. Acceptance criteria и DoD приложены. Dependencies и DB не меняются.

## Preflight

```json
{
  "status": "ALLOWED",
  "agent": "ai-backend-developer",
  "task_type": "backend",
  "allowed_actions": ["modify_backend_code", "add_backend_tests"],
  "blocked_actions": [],
  "required_approvals": [],
  "recommended_next_step": "Выполнить backend patch и передать на code review + QA."
}
```
