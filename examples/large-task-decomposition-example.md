# Пример: large task decomposition

## Запрос

"Разработать новый модуль с backend, frontend, DB, security, test automation, QA и docs."

## Классификация

```yaml
task_complexity: large
decomposition_required: true
required_agents:
  - ai-product-orchestrator
  - ai-solution-architect
  - ai-backend-developer
  - ai-frontend-developer
  - ai-database-engineer
  - ai-security-engineer
  - ai-test-automation-engineer
  - ai-qa-engineer
  - ai-technical-writer
optional_agents:
  - ai-delivery-project-manager
```

## Decomposition plan

```yaml
parent_task: "Новый модуль"
subtasks:
  - id: ST-01
    title: Analysis
    owner_agent: ai-system-analyst
    expected_artifacts: [TZ, acceptance_criteria]
  - id: ST-02
    title: Architecture / ADR
    owner_agent: ai-solution-architect
    dependencies: [ST-01]
    expected_artifacts: [ADR, architecture_spec]
  - id: ST-03
    title: Backend
    owner_agent: ai-backend-developer
    dependencies: [ST-02]
    expected_artifacts: [backend_patch, backend_tests]
  - id: ST-04
    title: Frontend
    owner_agent: ai-frontend-developer
    dependencies: [ST-02]
    expected_artifacts: [frontend_patch, frontend_tests]
  - id: ST-05
    title: Database
    owner_agent: ai-database-engineer
    dependencies: [ST-02]
    expected_artifacts: [migration_plan, rollback_plan]
  - id: ST-06
    title: Security
    owner_agent: ai-security-engineer
    dependencies: [ST-02, ST-03, ST-04, ST-05]
    expected_artifacts: [security_review]
  - id: ST-07
    title: Test Automation
    owner_agent: ai-test-automation-engineer
    dependencies: [ST-03, ST-04, ST-05]
    expected_artifacts: [test_automation_plan, test_results]
  - id: ST-08
    title: QA Gate
    owner_agent: ai-qa-engineer
    dependencies: [ST-07]
    expected_artifacts: [QA_gate_result]
  - id: ST-09
    title: Documentation
    owner_agent: ai-technical-writer
    dependencies: [ST-08]
    expected_artifacts: [documentation_patch]
  - id: ST-10
    title: Trello update
    owner_agent: ai-trello-analyst
    dependencies: [ST-01, ST-08]
    expected_artifacts: [trello_status_update]
  - id: ST-11
    title: Gantt update
    owner_agent: ai-delivery-project-manager
    dependencies: [ST-01, ST-10]
    expected_artifacts: [gantt_plan_update]
parallel_groups:
  - [ST-03, ST-04, ST-05]
approval_gates:
  - ai-product-orchestrator
  - ai-solution-architect
  - ai-security-engineer
  - ai-qa-engineer
```
