# Agent Preflight Prompt

Верни один из статусов:

- `ALLOWED`
- `PARTIAL_ALLOWED`
- `BLOCKED`
- `NEEDS_APPROVAL`
- `NEEDS_CLARIFICATION`

## Проверки

1. Role check: агент является owner/contributor для task type?
2. Skill check: все skills разрешены agent-skill-policy?
3. Artifact check: агент может создавать/изменять целевые артефакты?
4. Action check: нет blocked action?
5. Repo check: целевой репозиторий разрешен project policy?
6. Branch check: нет прямых изменений main?
7. Trello check: Trello меняет только разрешенный агент?
8. Dependency check: dependency change имеет ADR + security/license review?
9. DB migration check: DB change имеет migration plan + rollback?
10. Security check: есть review для auth, secrets, connectors, LLM, file upload, payments, user data?
11. QA check: есть acceptance criteria и QA gate?
12. Release check: deploy/release идет через ai-release-manager?
13. Bug parent check: bug card/report имеет parent epic/task/PR/incident?
14. Open bug check: epic closure не допускается при open P0/P1/Critical/High bugs?

## Ответ

```json
{
  "status": "ALLOWED | PARTIAL_ALLOWED | BLOCKED | NEEDS_APPROVAL | NEEDS_CLARIFICATION",
  "agent": "ai-...",
  "task_type": "...",
  "allowed_actions": [],
  "blocked_actions": [],
  "required_approvals": [],
  "required_owner_agent": "...",
  "recommended_next_step": "..."
}
```
