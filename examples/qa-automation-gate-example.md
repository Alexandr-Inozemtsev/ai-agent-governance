# Пример: QA Automation Gate

## Сценарий

Изменён backend `SimpleRetriever`.

## Порядок

1. `ai-test-automation-engineer` запускает или описывает approved commands для unit, integration и regression tests.
2. `ai-test-automation-engineer` передаёт `test_results` в `ai-qa-engineer`.
3. `ai-qa-engineer` проверяет test results перед ручным QA.
4. Если tests passed, `ai-qa-engineer` выполняет ручную проверку Problem generation и принимает QA gate по acceptance criteria.
5. Если tests failed, создаётся bug report или flaky test report. Ручное тестирование разрешено только для defect confirmation, exploratory analysis или evidence collection. QA gate не может быть `PASSED`.
6. Если tests missing, выполняется handoff к `ai-test-automation-engineer` на создание или обновление автотестов. QA gate может быть только `QA_GATE_CONDITIONAL` при documented exception.

## Output

```yaml
qa_automation_gate:
  status: "AUTOTESTS_PASSED"
  existing_functionality_impacted: true
  impacted_areas:
    - SimpleRetriever
    - Problem generation
  required_test_types:
    - unit
    - integration
    - regression
  test_commands:
    - "pytest tests/unit -k SimpleRetriever"
    - "pytest tests/integration -k SimpleRetriever"
    - "pytest tests/regression -k problem_generation"
  test_results:
    passed: 42
    failed: 0
    skipped: 1
    warnings: []
  failed_tests: []
  flaky_tests: []
  missing_tests: []
  manual_testing_started: true
  manual_testing_allowed: true
  manual_testing_block_reason: ""
  bug_reports_created: []
  required_handoff:
    next_agent: ""
    reason: ""
  QA_gate_decision: "Manual QA allowed after required autotests passed."
  QA_gate_owner: ai-qa-engineer
  test_automation_owner: ai-test-automation-engineer
```
