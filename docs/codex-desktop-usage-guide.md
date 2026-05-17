# Codex Desktop Usage Guide

## Куда положить governance repo

Рекомендуемый отдельный репозиторий: `ai-agent-governance`. Временно пакет может лежать в текущей governance-папке.

## Как ссылаться в запросах

Пиши: "Ты `ai-product-orchestrator`. Перед выполнением прочитай `ai-agent-governance/global/*`, domain policy и project override."

## Как добавлять project override

Скопируй `project-overrides/project-policy-template.yaml`, заполни project id, repository, Trello board, domain policy, allowed agents и bug rules.

## Как запускать preflight

Используй `prompt-templates/agent-preflight-prompt.md`. Без `ALLOWED` агент не должен менять code, Trello, GitHub, DB, CI/CD, dependencies или release state.

## Как блокировать нарушение

Верни JSON по `prompt-templates/blocked-response-template.md`, укажи violated policy и безопасный следующий шаг.

## Как создавать bug reports

QA использует `prompt-templates/bug-report-template.md`. Trello bug card создается только с parent epic/task/PR/incident и по project policy.

## Как запускать test automation

Для задач вида "добавь автотесты", "обнови e2e", "проверь coverage" или "разбери flaky test" preflight должен выбирать `task_type: test_automation` и owner `ai-test-automation-engineer`. Результат автотестов передается `ai-qa-engineer`; сам test automation не закрывает QA gate и не закрывает bugs.

## Как запускать QA Automation Gate

Перед ручным тестированием старого функционала сначала прогнать или проверить релевантные автотесты. Например: "Перед ручным regression Problem generation проверь unit/integration/regression результаты SimpleRetriever; если failed или missing, не ставь QA gate PASSED и передай `ai-test-automation-engineer`."

`ai-qa-engineer` может продолжить ручную проверку при failed autotests только для defect confirmation, evidence collection или exploratory analysis. Такой результат не закрывает QA gate.

## Практический сценарий большой задачи

1. Пользователь даёт большой запрос, например backend + frontend + DB + security + QA.
2. `ai-product-orchestrator` определяет `complexity = large`.
3. Orchestrator создаёт decomposition plan с owner agents, dependencies, Trello mapping, Gantt impact и approval gates.
4. Orchestrator не пишет код сразу и не меняет Trello/Gantt напрямую.
5. Пользователь проверяет русское `user_review_summary_ru`.
6. После approval задачи выполняются частями с checkpoint.
7. Автотесты выполняет или анализирует `ai-test-automation-engineer`.
8. QA gate выполняет `ai-qa-engineer`.
9. Trello обновляет `ai-trello-analyst` по `proposed_status_update`.
10. Gantt обновляет `ai-delivery-project-manager`, если изменились сроки, dependencies, blockers, critical bugs, release impact или required autotest status.

English technical plans допустимы для AI-workers, но пользовательское summary всегда должно быть на русском языке.
