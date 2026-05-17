# Пример: missing required agent

## Сценарий

Задача требует ручной QA gate и regression по существующему функционалу, но `ai-qa-engineer` недоступен.

## Preflight result

```yaml
agent_availability_check:
  status: BLOCKED_MISSING_AGENT
  required_agents:
    - ai-test-automation-engineer
    - ai-qa-engineer
  optional_agents:
    - ai-code-reviewer
  available_agents:
    - ai-test-automation-engineer
  missing_required_agents:
    - ai-qa-engineer
  missing_optional_agents: []
  blocked_task_parts:
    - QA_gate
    - manual_regression
    - bug_QA_verification
  allowed_task_parts:
    - automated_test_run
    - test_results_report
  next_required_handoff:
    - ai-qa-engineer
  recommended_next_step: "Выполнить только automated test report и дождаться ai-qa-engineer для QA gate."
```

## Решение

`ai-test-automation-engineer` может подготовить test results. QA gate не закрывается, пока `ai-qa-engineer` не подключится.
