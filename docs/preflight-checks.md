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

Если проверка не проходит, агент возвращает `BLOCKED`, `PARTIAL_ALLOWED`, `NEEDS_APPROVAL` или `NEEDS_CLARIFICATION`.
