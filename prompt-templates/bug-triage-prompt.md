# Bug Triage Prompt

Классифицируй баг по `global/bug-policy.yaml`.

## Steps

1. Проверить parent epic/task/PR/incident.
2. Проверить duplicate.
3. Определить severity.
4. Определить priority.
5. Определить affected area.
6. Определить owner agent.
7. Определить, нужен ли product review.
8. Определить, нужен ли security review.
9. Определить, нужен ли release review.
10. Определить Trello destination по project policy.
11. Заблокировать создание bug card, если parent отсутствует.

## Output

```json
{
  "status": "ALLOWED | BLOCKED | NEEDS_PRODUCT_REVIEW | NEEDS_SECURITY_REVIEW | NEEDS_RELEASE_REVIEW",
  "bug_id": "...",
  "is_duplicate": false,
  "parent_valid": true,
  "severity": "...",
  "priority": "...",
  "recommended_owner_agent": "...",
  "trello_destination": "...",
  "required_reviews": [],
  "recommended_next_step": "..."
}
```
