# Preflight Checks

Перед выполнением запроса агент проверяет:

- role check;
- skill check;
- artifact check;
- action check;
- repo check;
- branch check;
- Trello check;
- dependency check;
- DB migration check;
- security check;
- QA check;
- release check;
- bug parent check;
- open bug check for epic closure.
- если задача требует реализации автотестов, required agent = `ai-test-automation-engineer`;
- если задача требует QA gate, required agent = `ai-qa-engineer`;
- если задача требует и автотесты, и QA gate, нужны оба агента.
- QA Automation Gate Check:
  - если затрагивается старый/существующий функционал, preflight требует automated test results до manual regression;
  - если нужны regression/autotests, `ai-test-automation-engineer` должен быть в required agents;
  - если test results отсутствуют, статус `AUTOTESTS_REQUIRED` или `AUTOTESTS_NOT_FOUND`;
  - если required autotests failed, manual regression блокируется для QA pass и нужен handoff к `ai-test-automation-engineer`;
  - manual testing before autotests запрещён, кроме documented exception для defect confirmation, evidence collection или exploratory analysis.
- Agent Availability Check:
  - owner agent определён;
  - required_agents и optional_agents перечислены;
  - missing required agent блокирует owned part;
  - missing optional agent допускает partial execution;
  - uncertainty по availability указывается явно.
- Task Complexity Check:
  - simple: 1-2 агента, 1 домен;
  - medium: 3-4 агента, 1-2 домена;
  - large: 5+ агентов или 3+ домена;
  - critical: security, DB migration, dependency update, release, hotfix, Trello restructure, QA gate, failed required autotests.
- Decomposition Required Check:
  - large/critical задачи требуют decomposition plan;
  - execution без checkpoint запрещён;
  - existing functionality требует test automation и QA gate subtasks.
- Status Sync Impact Check:
  - есть ли status change;
  - нужен ли `proposed_status_update`;
  - Trello owner = `ai-trello-analyst`.
- Gantt Impact Check:
  - меняются ли сроки, dependencies, blockers, release impact или required autotest status;
  - Gantt owner = `ai-delivery-project-manager`.
- Dual-Language Planning Check:
  - English technical plan allowed для agents;
  - русский `user_review_summary_ru` обязателен для пользователя;
  - отсутствие русского summary даёт `NEEDS_USER_REVIEW_SUMMARY`.
- QA Automation Gate Awareness Check:
  - `ai-test-automation-engineer` владеет automated test status;
  - `ai-qa-engineer` владеет QA gate;
  - failed/missing required autotests блокируют QA pass.

Если проверка не проходит, агент возвращает `BLOCKED`, `PARTIAL_ALLOWED`, `NEEDS_APPROVAL`, `NEEDS_CLARIFICATION` или `NEEDS_USER_REVIEW_SUMMARY`.
