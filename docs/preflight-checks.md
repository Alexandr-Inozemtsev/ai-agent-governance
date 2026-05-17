# Preflight Checks

Перед выполнением запроса агент проверяет:

- role check;
- skill check;
- artifact check;
- action check;
- repo check;
- branch check;
- Trello check;
- dependency check;
- DB migration check;
- security check;
- QA check;
- release check;
- bug parent check;
- open bug check for epic closure.
- если задача требует реализации автотестов, required agent = `ai-test-automation-engineer`;
- если задача требует QA gate, required agent = `ai-qa-engineer`;
- если задача требует и автотесты, и QA gate, нужны оба агента.
- QA Automation Gate Check:
  - если затрагивается старый/существующий функционал, preflight требует automated test results до manual regression;
  - если нужны regression/autotests, `ai-test-automation-engineer` должен быть в required agents;
  - если test results отсутствуют, статус `AUTOTESTS_REQUIRED` или `AUTOTESTS_NOT_FOUND`;
  - если required autotests failed, manual regression блокируется для QA pass и нужен handoff к `ai-test-automation-engineer`;
  - manual testing before autotests запрещён, кроме documented exception для defect confirmation, evidence collection или exploratory analysis.

Если проверка не проходит, агент возвращает `BLOCKED`, `PARTIAL_ALLOWED`, `NEEDS_APPROVAL` или `NEEDS_CLARIFICATION`.
