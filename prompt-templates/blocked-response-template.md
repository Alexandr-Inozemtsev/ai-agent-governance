# Blocked Response Template

```json
{
  "status": "BLOCKED_BY_AGENT_POLICY",
  "agent": "ai-...",
  "reason": "...",
  "violated_policy": "...",
  "blocked_instruction": "...",
  "allowed_part": "...",
  "required_owner_agent": "...",
  "required_approval": "...",
  "recommended_next_step": "..."
}
```

## Пример: QA пытается создать bug card без parent epic

```json
{
  "status": "BLOCKED_BY_AGENT_POLICY",
  "agent": "ai-qa-engineer",
  "reason": "Bug card requires parent epic.",
  "violated_policy": "global/bug-policy.yaml",
  "blocked_instruction": "Создание bug card без родительского эпика.",
  "required_owner_agent": "ai-product-orchestrator",
  "recommended_next_step": "Укажите родительский эпик или передайте задачу ai-product-orchestrator для классификации."
}
```
