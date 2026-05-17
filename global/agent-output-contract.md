# Agent Output Contract

Любой агент обязан возвращать результат в формате, совместимом с этим контрактом. Если часть работы заблокирована policy, это отражается явно.

## Общий контракт

```json
{
  "status": "COMPLETED | PARTIAL | BLOCKED_BY_AGENT_POLICY | NEEDS_ORCHESTRATOR_REVIEW | FAILED",
  "agent_name": "ai-...",
  "role": "...",
  "task_type": "...",
  "policy_version": "1.0",
  "domain_policy_version": "1.0",
  "project_policy_version": "1.0",
  "used_skills": [],
  "blocked_skills": [],
  "input_summary": "...",
  "scope_boundary": "...",
  "output_artifacts": [],
  "changed_files": [],
  "proposed_files": [],
  "trello_changes": [],
  "github_changes": [],
  "bug_reports": [],
  "risks": [],
  "assumptions": [],
  "policy_violations": [],
  "unresolved_questions": [],
  "next_handoff": {
    "next_agent": "...",
    "reason": "...",
    "required_inputs": []
  },
  "required_review": [],
  "recommended_next_step": "..."
}
```

## Дополнительные поля для bug report

```json
{
  "bug_id": "БАГ-ЭПИК-04-001",
  "parent_epic_id": "ЭПИК-04",
  "parent_epic_title": "...",
  "parent_task_id": "...",
  "parent_task_title": "...",
  "severity": "Critical | High | Medium | Low",
  "priority": "P0 | P1 | P2 | P3",
  "affected_area": "Backend | Frontend | LLM/RAG | Data | Security | DevOps | UX | Docs | Other",
  "environment": "...",
  "steps_to_reproduce": [],
  "actual_result": "...",
  "expected_result": "...",
  "evidence": [],
  "regression_risk": "Low | Medium | High",
  "linked_pr": "...",
  "linked_test_case": "...",
  "recommended_owner_agent": "ai-...",
  "blocks_epic_completion": true,
  "requires_product_review": false,
  "requires_security_review": false,
  "requires_release_review": false
}
```

## Дополнительные поля для test automation результатов

```yaml
test_automation_result:
  test_scope: ""
  test_types:
    - unit
    - integration
    - API
    - e2e
    - mocks
    - regression
  changed_test_files: []
  changed_fixture_files: []
  changed_mock_files: []
  test_commands: []
  tests_passed: 0
  tests_failed: 0
  tests_skipped: 0
  coverage_summary: ""
  flaky_tests_detected: []
  bug_reports_created: []
  requires_qa_verification: true
  next_handoff:
    next_agent: ai-qa-engineer
    reason: "QA gate / defect verification"
```

## Дополнительные поля для QA Automation Gate

```yaml
qa_automation_gate:
  status: "AUTOTESTS_REQUIRED | AUTOTESTS_NOT_FOUND | AUTOTESTS_PASSED | AUTOTESTS_FAILED | AUTOTESTS_FLAKY | MANUAL_TESTING_ALLOWED | MANUAL_TESTING_BLOCKED | QA_GATE_PASSED | QA_GATE_FAILED | QA_GATE_CONDITIONAL | NEEDS_TEST_AUTOMATION_REVIEW"
  existing_functionality_impacted: true
  impacted_areas: []
  required_test_types: []
  test_commands: []
  test_results:
    passed: 0
    failed: 0
    skipped: 0
    warnings: []
  failed_tests: []
  flaky_tests: []
  missing_tests: []
  manual_testing_started: false
  manual_testing_allowed: false
  manual_testing_block_reason: ""
  bug_reports_created: []
  required_handoff:
    next_agent: ""
    reason: ""
  QA_gate_decision: ""
  QA_gate_owner: ai-qa-engineer
  test_automation_owner: ai-test-automation-engineer
```
