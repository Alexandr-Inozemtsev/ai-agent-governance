# Trello Task Prompt Template

Используй только для `ai-trello-analyst` или разрешенного project-policy exception.

## Mandatory checks

- Есть approved backlog или approved bug report.
- Scope подтвержден `ai-product-orchestrator`.
- Нет duplicate card.
- Card содержит owner, labels, acceptance criteria, DoD, dependencies.
- Bug card содержит parent epic/task/PR/incident.
- Parent epic checklist `Баги / дефекты` обновляется.

## Output

Вернуть proposed/actual Trello changes по output contract. Если Trello mutation запрещена, вернуть `BLOCKED_BY_AGENT_POLICY`.
