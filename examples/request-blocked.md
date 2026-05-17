# Request Blocked

## Backend пытается изменить Trello

```json
{
  "status": "BLOCKED_BY_AGENT_POLICY",
  "agent": "ai-backend-developer",
  "reason": "Trello mutation belongs to ai-trello-analyst.",
  "violated_policy": "global/trello-policy.yaml",
  "blocked_instruction": "Изменить Trello card.",
  "required_owner_agent": "ai-trello-analyst",
  "recommended_next_step": "Передать approved backlog/card update ai-trello-analyst."
}
```

## QA пытается создать bug card без parent epic

См. `prompt-templates/blocked-response-template.md`.

## Frontend пытается изменить БД

```json
{
  "status": "BLOCKED_BY_AGENT_POLICY",
  "agent": "ai-frontend-developer",
  "reason": "Database changes require ai-database-engineer and migration plan.",
  "violated_policy": "global/blocked-actions.yaml",
  "blocked_instruction": "Изменить schema из frontend task.",
  "required_owner_agent": "ai-database-engineer",
  "recommended_next_step": "Создать DB migration request с migration plan."
}
```
