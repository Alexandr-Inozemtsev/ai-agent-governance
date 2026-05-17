# Пример: status sync

## Сценарий

Backend agent завершил implementation. Нужно пройти автотесты, QA gate и обновить Trello.

## Flow

1. `ai-backend-developer` возвращает implementation summary и `proposed_status_update`.
2. `ai-test-automation-engineer` запускает автотесты и возвращает automated test status.
3. `ai-qa-engineer` выполняет QA gate после test results.
4. `ai-trello-analyst` применяет Trello transition только при наличии evidence.

## Proposed status update

```yaml
proposed_status_update:
  source_agent: ai-backend-developer
  task_id: TASK-42
  parent_epic_id: EPIC-04
  previous_status: "In Progress"
  proposed_status: "Automated Tests Requested"
  reason: "Backend implementation completed; required autotests must run before QA."
  evidence:
    - changed_files
    - implementation_summary
  checklist_updates:
    - "Implementation completed"
  bug_updates: []
  test_automation_updates:
    - "Request unit/integration/API/regression tests"
  QA_gate_updates:
    - "QA gate blocked until automated test results"
  risk_updates: []
  gantt_impact: "No date change unless tests fail."
  required_approvals: []
  target_owner_agent: ai-trello-analyst
```

## Правило

`ai-backend-developer` не двигает карточку сам. Trello update выполняет только `ai-trello-analyst`.
