# Пример: ai-test-automation-engineer

## Запрос

"Добавь автотесты для SimpleRetriever."

## Preflight

- `task_type`: `test_automation`
- `owner_agent`: `ai-test-automation-engineer`
- `required_agents`:
  - `ai-test-automation-engineer`
  - `ai-qa-engineer`
- `optional_agents`:
  - `ai-backend-developer`
- `allowed_actions`:
  - modify test files
  - create mocks/fixtures
  - run pytest
- `blocked_actions`:
  - change production code
  - close QA gate
  - modify Trello

## Output

- `test_patch`
- `test_results`
- `coverage_report`
- handoff to `ai-qa-engineer`

## Handoff

`ai-test-automation-engineer` передает результаты `ai-qa-engineer` для QA gate и defect verification. Если автотест выявил дефект, создается bug report с parent epic/task/PR/test case. Если дефект похож на flaky behavior, сначала создается flaky test report.
