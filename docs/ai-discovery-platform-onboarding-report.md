# AI Discovery Platform: отчёт о подключении

## Статус

`READY_FOR_PREFLIGHT`

Проект AI Discovery Platform подключен к governance-пакету `ai-agent-governance` через project override:

- `project-overrides/ai-discovery-platform-policy.yaml`
- `project-overrides/ai-discovery-platform-preflight.md`

## Доменная политика

Используется domain policy `domains/ai-rag-platform-policy.yaml` для AI/RAG-платформ.

## Разрешенные агенты

- `ai-product-orchestrator`
- `ai-trello-analyst`
- `ai-business-analyst`
- `ai-system-analyst`
- `ai-solution-architect`
- `ai-ui-ux-designer`
- `ai-frontend-developer`
- `ai-backend-developer`
- `ai-database-engineer`
- `ai-data-metrics-engineer`
- `ai-llm-rag-engineer`
- `ai-security-engineer`
- `ai-devops-engineer`
- `ai-qa-engineer`
- `ai-test-automation-engineer`
- `ai-code-reviewer`
- `ai-release-manager`
- `ai-technical-writer`
- `ai-delivery-project-manager`
- `ai-performance-engineer`
- `ai-monetization-strategist`

## Запрещенные действия

- Менять production-код AI Discovery Platform без approved task.
- Менять репозиторий AI Discovery Platform в рамках governance-задачи.
- Менять Trello-доску без `ai-trello-analyst`.
- Создавать GitHub issues или PR без отдельного approval.
- Добавлять runtime-зависимости без ADR, security review и license review.
- Отправлять sensitive data во внешний LLM без project approval.
- Отключать `source_trace` для AI-generated artifacts.
- Менять scope без `ai-product-orchestrator`.

## Правила по багам

- `ai-qa-engineer` может создавать bug report.
- `ai-test-automation-engineer` может создавать bug report, если failed automation test выявил дефект.
- Trello bug card создает только `ai-trello-analyst`.
- QA не может напрямую создавать Trello bug card.
- Bug card требует parent epic.
- Parent epic должен вести checklist `Баги / дефекты`.
- Epic нельзя закрыть при открытых P0/P1/Critical/High bugs.
- Bug нельзя закрыть без QA verification.

## Test automation

- `ai-test-automation-engineer` подключён к AI Discovery Platform.
- Агент отвечает за автотесты backend/frontend/API/e2e.
- QA gate остается за `ai-qa-engineer`.
- Для `SimpleRetriever` автотесты должны покрывать unit, integration и regression сценарии.
- Для `SimpleRetriever` и backend/API изменений ручной QA разрешён только после unit/integration/regression тестов.
- Для backend/API изменений перед manual QA требуются unit, integration, API и regression results.
- Failed tests могут создавать bug report, но `ai-test-automation-engineer` не закрывает bug.
- Если failed test связан с flaky behavior, сначала создается flaky test report.
- QA gate не может быть `PASSED` при failed required autotests.
- Если required autotests отсутствуют, нужен handoff к `ai-test-automation-engineer`; conditional QA gate возможен только по exception от `ai-product-orchestrator` и `ai-qa-engineer`, а для release impact также от `ai-release-manager`.

## Как запускать preflight

1. Прочитать global policies из `global/`.
2. Прочитать `domains/ai-rag-platform-policy.yaml`.
3. Прочитать `project-overrides/ai-discovery-platform-policy.yaml`.
4. Выполнить preflight по `prompt-templates/agent-preflight-prompt.md`.
5. При `ALLOWED` выполнять задачу.
6. При `BLOCKED` остановиться и указать нарушенное правило.
7. При `NEEDS_APPROVAL` указать, чье согласование требуется.
