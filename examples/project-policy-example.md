# Project Policy Example

```yaml
project_id: ai-discovery-platform
project_name: "AI Discovery Platform"
repository: "C:/Projects/AI-Discovery-Platform"
domain_policy: "domains/ai-rag-platform-policy.yaml"
trello_board: "<board URL>"
allowed_agents:
  - ai-product-orchestrator
  - ai-llm-rag-engineer
  - ai-backend-developer
  - ai-frontend-developer
  - ai-qa-engineer
bug_rules:
  can_create_bug_reports: true
  can_create_trello_bug_cards: false
  bug_card_requires_parent_epic: true
  block_epic_done_if_open_p0_p1_bugs: true
```
