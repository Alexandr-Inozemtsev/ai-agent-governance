# Agent Preflight Prompt

Верни один из статусов:

- `ALLOWED`
- `PARTIAL_ALLOWED`
- `BLOCKED`
- `NEEDS_APPROVAL`
- `NEEDS_CLARIFICATION`
- `NEEDS_USER_REVIEW_SUMMARY`

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
16. Agent Availability Check:
    - определены ли required_agents и optional_agents;
    - доступен ли owner agent;
    - missing required agent блокирует принадлежащую ему часть;
    - missing optional agent допускает partial execution с risk/NEEDS_REVIEW;
    - если availability неизвестна, явно указать uncertainty.
17. Task Complexity Check:
    - simple: 1-2 агента, 1 домен, inline allowed;
    - medium: 3-4 агента, 1-2 домена, short plan required;
    - large: 5+ агентов или 3+ домена, mandatory decomposition;
    - critical: security/database_migration/dependency_update/release/production_hotfix/trello_board_restructure/QA_gate/failed_required_autotests.
18. Multi-Agent Decomposition Check:
    - large/critical задачи требуют decomposition plan;
    - нельзя сразу писать код, менять Trello/БД/dependencies/release;
    - для existing functionality включить test automation subtask и QA gate subtask.
19. Status Sync Impact Check:
    - нужен ли proposed_status_update;
    - кто target_owner_agent;
    - Trello status owner = `ai-trello-analyst`.
20. Gantt Impact Check:
    - меняются ли сроки, dependencies, blockers, release impact, P0/P1 bugs, required autotest status;
    - Gantt owner = `ai-delivery-project-manager`.
21. Dual-Language Planning Check:
    - если создан English technical plan, есть ли русский `user_review_summary_ru`;
    - если русского summary нет, статус `NEEDS_USER_REVIEW_SUMMARY`.
22. QA Automation Gate Awareness Check:
    - test automation owner = `ai-test-automation-engineer`;
    - QA gate owner = `ai-qa-engineer`;
    - required autotests failed/missing блокируют QA pass.

## Ответ

```json
{
  "preflight_status": "ALLOWED | PARTIAL_ALLOWED | BLOCKED | NEEDS_APPROVAL | NEEDS_CLARIFICATION | NEEDS_USER_REVIEW_SUMMARY",
  "agent": "ai-...",
  "task_type": "...",
  "task_complexity": "simple | medium | large | critical",
  "decomposition_required": true,
  "agent_availability_status": "...",
  "required_agents": [],
  "optional_agents": [],
  "available_agents": [],
  "missing_required_agents": [],
  "missing_optional_agents": [],
  "blocked_task_parts": [],
  "allowed_task_parts": [],
  "trello_update_required": true,
  "gantt_update_required": true,
  "status_sync_owner": "ai-trello-analyst",
  "gantt_owner": "ai-delivery-project-manager",
  "test_automation_owner": "ai-test-automation-engineer",
  "QA_gate_owner": "ai-qa-engineer",
  "qa_automation_gate_required": true,
  "english_technical_plan_allowed": true,
  "russian_user_summary_required": true,
  "user_review_summary_ru_present": true,
  "recommended_execution_mode": "inline | split_requests | subagent_driven | blocked",
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
