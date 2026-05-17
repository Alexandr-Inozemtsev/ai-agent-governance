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
15. QA Automation Gate Check:
    - затрагивается ли старый/существующий функционал;
    - требуются ли regression/autotests;
    - есть ли `ai-test-automation-engineer` среди `required_agents`;
    - есть ли automated test results;
    - можно ли начинать manual testing;
    - требуется ли handoff к `ai-test-automation-engineer`.

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
  "qa_automation_gate_check": {
    "existing_functionality_impacted": true,
    "required_before_manual_testing": true,
    "required_agent": "ai-test-automation-engineer",
    "qa_gate_owner": "ai-qa-engineer",
    "automated_test_results_required": true,
    "manual_testing_allowed_before_autotests": false,
    "status": "AUTOTESTS_REQUIRED | AUTOTESTS_PASSED | AUTOTESTS_FAILED | AUTOTESTS_NOT_FOUND | NEEDS_TEST_AUTOMATION_REVIEW",
    "recommended_next_step": ""
  },
  "recommended_next_step": "..."
}
```
