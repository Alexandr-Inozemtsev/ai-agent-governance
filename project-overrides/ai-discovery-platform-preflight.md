# Preflight для AI Discovery Platform

Перед любой задачей по проекту AI Discovery Platform нужно выполнить preflight в governance-репозитории `ai-agent-governance`.

1. Прочитать global policies из `global/`.
2. Прочитать domain policy `domains/ai-rag-platform-policy.yaml`.
3. Прочитать project override `project-overrides/ai-discovery-platform-policy.yaml`.
4. Выполнить preflight по `prompt-templates/agent-preflight-prompt.md`.
5. Проверить доступность required/optional агентов:
   - required agent missing блокирует принадлежащую ему часть;
   - optional agent missing допускает partial execution с risk;
   - если нужны автотесты, required agent = `ai-test-automation-engineer`;
   - если нужен QA gate, required agent = `ai-qa-engineer`.
6. Определить сложность задачи:
   - `simple` можно выполнять inline;
   - `medium` требует short plan;
   - `large` требует decomposition plan;
   - `critical` требует decomposition plan, approvals и checkpoints.
7. Проверить необходимость декомпозиции:
   - 5+ агентов;
   - 3+ зон ответственности;
   - backend + frontend + database;
   - security, dependency, DB migration, release, Trello restructure, Gantt/roadmap changes;
   - QA gate или failed required autotests.
8. Проверить Trello status sync impact:
   - Trello меняет только `ai-trello-analyst`;
   - остальные агенты возвращают `proposed_status_update`;
   - status update требует evidence.
9. Проверить Gantt impact:
   - Gantt owner = `ai-delivery-project-manager`;
   - Gantt update нужен при blocker, dependency, due date, release impact, P0/P1 bug, failed/missing required autotests.
10. Проверить QA Automation Gate:
    - existing functionality manual regression допускается только после релевантных автотестов;
    - failed/missing required autotests блокируют QA pass;
    - test automation owner = `ai-test-automation-engineer`;
    - QA gate owner = `ai-qa-engineer`.
11. Проверить dual-language planning:
    - English technical plan допустим для AI-workers;
    - если он создан, обязателен русский `user_review_summary_ru`.
12. Если результат `ALLOWED` - выполнять задачу в рамках разрешенного owner agent и действующих quality gates.
13. Если результат `PARTIAL_ALLOWED` - выполнять только allowed_task_parts и явно указать blocked_task_parts.
14. Если результат `BLOCKED` - остановиться и указать нарушенное правило.
15. Если результат `NEEDS_APPROVAL` - указать, чье согласование нужно, например `ai-product-orchestrator`, профильного owner agent, security review, license review или ADR approval.
16. Если результат `NEEDS_USER_REVIEW_SUMMARY` - вернуть русское summary до дальнейшего выполнения.

Запрещено в рамках preflight-задач менять production-код AI Discovery Platform, репозиторий AI Discovery Platform, Trello-доску, GitHub issues/PR и runtime-зависимости без отдельного разрешения.
