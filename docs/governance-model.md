# Governance Model

1. Пользовательский запрос поступает `ai-product-orchestrator`.
2. Orchestrator запускает preflight.
3. Запрос классифицируется по task type.
4. Выбираются owner agent и contributor agents.
5. Проверяются skills, artifacts, actions, repo, branch, Trello, dependency, DB, security, QA, release и bug rules.
6. Агент выполняет только разрешенную часть.
7. Результат возвращается по output contract.
8. Quality gate проверяет DoD, tests, docs, risks и policy compliance.
9. Trello update делает `ai-trello-analyst`.
10. GitHub PR проходит review и QA.
11. Bug report создает `ai-qa-engineer` или `ai-test-automation-engineer`, если дефект выявлен автоматизированным тестом.
12. `ai-test-automation-engineer` выполняет автотесты и передает результат `ai-qa-engineer`.
13. `ai-qa-engineer` принимает QA gate и проверяет баги.
14. Test automation не равен QA approval: успешный прогон автотестов не закрывает QA gate без `ai-qa-engineer`.
15. Release decision принимает `ai-release-manager`.

## QA Automation Gate процесс

Для существующего функционала действует порядок:

`Code ready -> automated tests -> QA reviews test results -> manual testing -> QA gate`

`ai-test-automation-engineer` пишет, поддерживает, запускает или описывает автотесты и передает `test_results` в QA. `ai-qa-engineer` проверяет результаты автотестов перед ручным regression testing. Если required autotests failed, ручное тестирование может продолжаться только для defect confirmation, exploratory analysis или evidence collection, но QA gate не может быть `PASSED`.

## Большие multi-agent задачи

Большой запрос не выполняется одним agent-run. `ai-product-orchestrator` сначала определяет complexity, required/optional agents, доступность агентов, dependencies, Trello mapping, Gantt impact и approval gates. Large/critical задачи превращаются в decomposition plan с подзадачами: analysis, architecture/ADR, backend, frontend, database, security, test automation, QA gate, documentation, Trello update и Gantt update.

Запрос разбивается, если требует 5+ агентов, 3+ зон ответственности, одновременно backend + frontend + database, security review, dependency changes, database migration, release/deploy, Trello restructuring, Gantt/roadmap changes или создание BT + TZ + ADR + implementation в одном запросе.

Если required agent недоступен, принадлежащая ему часть блокируется и возвращается `BLOCKED_MISSING_AGENT` или `NEEDS_ORCHESTRATOR_REVIEW`. Если optional agent недоступен, разрешается partial execution с явным risk и status `PARTIAL_ALLOWED`.

## Status Sync, Trello и Gantt

Trello обновляет только `ai-trello-analyst`, кроме project-policy exceptions. Остальные агенты возвращают `proposed_status_update` с evidence, checklist updates, bug updates, test automation updates, QA gate updates и target owner.

Gantt/delivery-plan обновляет `ai-delivery-project-manager`. Gantt не является независимой правдой: scope берётся из approved backlog, execution status из Trello, test automation status из reports, QA status из QA gate reports, даты и зависимости из delivery plan.

Gantt обновляется по событиям: task approved, dependency changed, blocker found/resolved, P0/P1/Critical/High bug, failed required autotests, missing required autotests для release-critical scope, epic completed, release date changed. Регулярно Gantt обновляется в конце активной Codex-сессии/рабочего дня, раз в неделю и перед release candidate.

## Язык планов

Английский technical plan допустим для AI-workers, если это повышает качество implementation, architecture, test automation, QA или release planning. Пользователь подтверждает только русскоязычный `user_review_summary_ru`, где указаны цель, scope, changed/not changed, risks, tests, test automation status, QA gate status и next step.
