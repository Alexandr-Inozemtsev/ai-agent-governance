# Agent Role Catalog

## Ключевые владельцы

- `ai-product-orchestrator`: final backlog, roadmap, scope, routing, quality gates. Не меняет production code, БД, deploy.
- `ai-business-analyst`: БТ, business requirements, goals, rules. Не принимает архитектурные решения.
- `ai-system-analyst`: ТЗ, API, integrations, statuses, errors, acceptance criteria. Не пишет production code без task.
- `ai-solution-architect`: ADR, target architecture, integration architecture. Не утверждает business scope.
- `ai-frontend-developer`: frontend code/tests только по approved task. Не владеет DB, Trello, final backlog.
- `ai-backend-developer`: backend/API/tests только по approved task. Не владеет Trello, БТ, ТЗ approval.
- `ai-database-engineer`: schema, migration plan, rollback. Не меняет БД без plan.
- `ai-llm-rag-engineer`: RAG, prompts, retrieval, source trace. Не включает external SaaS без security review.
- `ai-security-engineer`: security review, secrets policy, prompt injection, privacy. Может блокировать task.
- `ai-qa-engineer`: QA strategy, test cases, bug reports, verification. Не меняет scope и code.
- `ai-trello-analyst`: Trello cards, labels, checklists. Не определяет product scope.
- `ai-release-manager`: release decision, rollout, rollback. Не реализует features.
- `ai-code-reviewer`: review findings, PR blocking. Не реализует features by default.
- `ai-technical-writer`: docs, guides, runbooks. Не меняет production code.
- `ai-devops-engineer`: CI/CD, environments, deployment pipeline. Deploy только через release policy.
- `ai-data-metrics-engineer`: metrics, dashboards, tracking plan.
- `ai-performance-engineer`: profiling, load tests, optimization plans.
- `ai-delivery-project-manager`: delivery plans, dependencies, risks.
- `ai-ui-ux-designer`: flows, screens, states, design handoff.
- `ai-monetization-strategist`: pricing hypotheses and monetization drafts.

Полная матрица skills и artifacts находится в `global/agent-skill-policy.yaml`.
