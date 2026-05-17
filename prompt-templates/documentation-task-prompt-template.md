# Documentation Task Prompt Template

Используй для docs-only задач.

## Mandatory checks

- Производственный код не менять.
- Документация на русском языке, если проект русскоязычный.
- Технические имена можно оставлять на английском.
- Документ должен содержать дату, статус, owner, scope и связанные эпики, если применимо.
- ADR/БТ/ТЗ редактирует только соответствующий owner-agent или approved contributor.

## Output

Вернуть `changed_files`, `scope_boundary`, `source_artifacts`, `risks`, `next_handoff`.
