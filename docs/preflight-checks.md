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

Если проверка не проходит, агент возвращает `BLOCKED`, `PARTIAL_ALLOWED`, `NEEDS_APPROVAL` или `NEEDS_CLARIFICATION`.
