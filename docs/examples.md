# Examples

## Разрешенный запрос

Approved backend task со статусом `Готово к разработке`, acceptance criteria, parent epic и тестовыми ожиданиями направляется `ai-backend-developer`. Trello не меняется, dependency не добавляется, DB не меняется.

## Заблокированный запрос

Если `ai-frontend-developer` просит изменить schema, preflight возвращает `BLOCKED_BY_AGENT_POLICY`, потому что DB owner — `ai-database-engineer`, а DB change требует migration plan.

## Частично разрешенный запрос

Если запрос содержит "создай bug report и сразу закрой epic несмотря на P1 bug", QA может создать bug report, но closure epic блокируется.
