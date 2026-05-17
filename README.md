# ai-agent-governance

`ai-agent-governance` — глобальный governance-пакет для AI-разработки в Codex Desktop / Codex CLI. Он не является project-specific policy одного репозитория: правила распространяются на все AI-агенты, все будущие проекты, Trello-доски, GitHub-репозитории и платформы.

## Почему пакет отдельный

Governance не должен жить внутри product repo, потому что он управляет многими проектами одновременно: AI Discovery Platform, gaming_platform, StreamIQ, AI Delivery Control Center, game/web/mobile/analytics/enterprise платформами и будущими репозиториями.

## Source of truth

- `global/agent-registry.yaml` — реестр ролей и зон владения.
- `global/agent-skill-policy.yaml` — матрица skills, permissions и запретов.
- `global/agent-routing-policy.yaml` — маршрутизация task types.
- `global/agent-availability-policy.yaml` — проверка required/optional agents перед выполнением.
- `global/task-decomposition-policy.yaml` — правила разбиения large/critical multi-agent задач.
- `global/status-sync-policy.yaml` — владельцы и события синхронизации статусов.
- `global/gantt-policy.yaml` — правила Gantt/delivery-plan как projection layer.
- `global/qa-automation-gate-policy.yaml` — automation-first QA gate перед ручным regression существующего функционала.
- `global/blocked-actions.yaml` — глобальные блокировки.
- `global/bug-policy.yaml` — правила bug reports и Trello bug cards.
- `project-overrides/project-policy-template.yaml` — шаблон подключения проекта.

## Глобальные агенты

Пакет включает 21 глобального агента, включая отдельного `ai-test-automation-engineer` для автотестов. `ai-test-automation-engineer` отвечает за unit, integration, API, e2e, mocks, fixtures, regression suites, flaky test analysis, CI test commands и coverage analysis. QA gate и bug verification остаются у `ai-qa-engineer`.

## QA Automation Gate

Для старого или существующего функционала ручной regression начинается только после проверки релевантных автотестов: `Code ready -> automated tests -> QA reviews test results -> manual testing -> QA gate`.

`ai-test-automation-engineer` пишет, поддерживает и анализирует автотесты, но не закрывает QA gate. `ai-qa-engineer` проверяет automated test results, выполняет ручное acceptance/regression/exploratory testing и принимает QA gate. Если required autotests failed или missing без documented exception, QA gate не может быть `PASSED`.

## Большие задачи, Trello, Gantt, автотесты и язык планов

Большие задачи разбиваются до выполнения. Decomposition обязателен, если запрос требует 5+ агентов, 3+ зон ответственности, backend + frontend + database, security review, dependency changes, DB migration, release/deploy, Trello/Gantt/roadmap changes или QA gate.

Trello обновляется по событиям и только владельцем `ai-trello-analyst`: task started, code review requested, automated tests started/failed/passed, qa started/failed/passed, blocker found/resolved, done. Остальные агенты возвращают `proposed_status_update` с evidence.

Gantt обновляет `ai-delivery-project-manager`. Он обновляется по событиям, которые влияют на сроки, dependencies, blockers, P0/P1/Critical/High bugs, failed/missing required autotests, release date или scope, а также регулярно: в конце активной Codex-сессии/рабочего дня, еженедельно и перед release candidate.

Английские technical plans допустимы для AI-workers: implementation, architecture, test automation, QA, release и worker task plans. Для пользователя всегда обязателен русский `user_review_summary_ru`; пользователь подтверждает только русскоязычное summary.

Owners процесса:

- Scope и decomposition: `ai-product-orchestrator`.
- Trello status: `ai-trello-analyst`.
- Gantt/delivery status: `ai-delivery-project-manager`.
- Test automation status: `ai-test-automation-engineer`.
- QA status / QA gate: `ai-qa-engineer`.
- Release status: `ai-release-manager`.

## Подключённые проекты

| Проект | Repository | Domain policy | Project override | Статус |
|---|---|---|---|---|
| AI Discovery Platform | `Alexandr-Inozemtsev/AI-Discovery-Platform` | `domains/ai-rag-platform-policy.yaml` | `project-overrides/ai-discovery-platform-policy.yaml` | `READY_FOR_PREFLIGHT` |

## Inheritance

Правила наследуются так:

`Global Policy -> Domain Policy -> Project Policy -> Task Policy`

Project Policy и Task Policy могут только ужесточать global rules. Если есть конфликт, побеждает запрет.

## Как использовать с Codex Desktop

1. Перед задачей укажи, что работает `ai-product-orchestrator`.
2. Попроси прочитать `ai-agent-governance/global/*`.
3. Укажи domain policy.
4. Укажи project override.
5. Запусти preflight по `prompt-templates/agent-preflight-prompt.md`.
6. Только после `ALLOWED` назначай owner agent.

## Как подключить новый проект

1. Выбрать domain policy.
2. Скопировать `project-overrides/project-policy-template.yaml`.
3. Заполнить repository, Trello board, allowed agents.
4. Указать data sensitivity, LLM provider rules, code/release/bug rules.
5. Запустить quality gate.

## Bug policy

QA может создавать bug reports. `ai-test-automation-engineer` тоже может создать bug report, если дефект выявлен автоматизированным тестом. Trello bug card создается только с parent epic/task/PR/incident. Для плановой разработки основной parent — epic. Родительский epic должен видеть открытые баги в checklist `Баги / дефекты`. Epic нельзя закрыть при открытых P0/P1/Critical/High bugs. Bug нельзя закрыть без QA verification.

## Soft и hard enforcement

Сейчас пакет задает soft enforcement: prompts, YAML policies, docs и templates для Codex. Будущий hard enforcement описан в `scripts/validate-policy-pseudocode.md`: validator будет программно блокировать запрещенные actions.
