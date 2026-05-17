# Пример: Gantt update

## Сценарий

В `ЭПИК-04` появился P1 bug или failed required autotests.

## Trigger

```yaml
delivery_status_update:
  gantt_update_required: true
  delivery_plan_changed: true
  dependency_changes: []
  blocker_changes:
    - "ЭПИК-04 blocked by failed required autotests"
  test_automation_blockers:
    - "Regression tests failed before manual QA"
  QA_gate_blockers:
    - "QA gate cannot be PASSED"
  release_impact: "Release candidate delayed until regression fixed or approved exception exists."
  next_delivery_review: "Следующий статус после bug triage и повторного test automation run."
```

## Owner

Gantt update выполняет `ai-delivery-project-manager`. Trello status update выполняет `ai-trello-analyst`. QA gate остаётся у `ai-qa-engineer`.
