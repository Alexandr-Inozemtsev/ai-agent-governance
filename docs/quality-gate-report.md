# Quality Gate Report

Дата: 2026-05-18

Статус: `PASS_WITH_FIXES`

Owner: `ai-product-orchestrator`

Scope: глобальный governance-пакет `ai-agent-governance`

## Что проверено

- Полнота структуры `ai-agent-governance`.
- Согласованность `global/agent-registry.yaml`, `global/agent-skill-policy.yaml` и `global/agent-routing-policy.yaml`.
- Отсутствие незарегистрированных агентов в routing.
- Отсутствие пересечений между `allowed_skills` и `denied_skills` в skill policy.
- Согласованность `blocked-actions`, `bug-policy`, `trello-policy`, `release-policy`.
- Правило, что project override не может ослаблять global policy.
- Bug governance:
  - bug report создает `ai-qa-engineer`;
  - `ai-test-automation-engineer` может создавать bug report, если дефект выявлен автоматизированным тестом;
  - Trello bug card требует parent epic/task/PR/incident;
  - плановый баг связан с parent epic;
  - parent epic ведет checklist `Баги / дефекты`;
  - epic нельзя закрыть при открытых P0/P1/Critical/High bugs;
  - bug нельзя закрыть без QA verification.
- Prompt templates требуют preflight до назначения агента.
- README объясняет использование governance repo в будущих Codex-запросах.

## Найденные конфликты

### 1. `ai-ui-ux-designer` отсутствовал в skill policy

`ai-ui-ux-designer` был зарегистрирован в `agent-registry.yaml` и использовался в routing, но не имел отдельного блока permissions в `agent-skill-policy.yaml`.

Риск: агент мог работать без явной матрицы allowed/denied skills.

Исправление: добавлен блок `ai-ui-ux-designer` в `global/agent-skill-policy.yaml`.

### 2. Routing ссылался на незарегистрированного `ai-test-automation-engineer`

`agent-routing-policy.yaml` использовал `ai-test-automation-engineer` в task types `qa` и `testing`, но этот агент не входит в текущий registry этого governance-пакета.

Риск: preflight мог назначить contributor agent, которого нет в global registry/skill policy.

Исправление: `ai-test-automation-engineer` зарегистрирован как отдельный глобальный агент, добавлен в skill policy и назначен owner для `testing`/`test_automation`. QA gate остается за `ai-qa-engineer`.

### 3. `release-policy.yaml` содержал неоднозначное поле `open_bug_report`

В `required_release_inputs` поле `open_bug_report` могло читаться как требование иметь открытый bug report для release.

Риск: release policy была семантически неоднозначной.

Исправление: поле заменено на `open_bug_status_report`, чтобы release gate требовал отчет о состоянии открытых багов, а не наличие открытого бага.

### 4. Project override template требовал более явной защиты от ослабления global deny

В `project-policy-template.yaml` было правило, что extra allow не может нарушать global, но не было отдельного validation rule.

Риск: project override мог быть прочитан как возможность расширять skills без явного blocked check.

Исправление: добавлено правило `validation_rule`: конфликт `allow_extra_skills` с global `denied_skills` или `blocked_actions` блокирует запрос.

### 5. README требовал более явного preflight workflow

README говорил запускать preflight, но не описывал поведение для `PARTIAL_ALLOWED` и `BLOCKED`.

Риск: будущий Codex-запрос мог назначить агента после неполного preflight.

Исправление: README расширен шагами: читать orchestrator prompt, запускать preflight, назначать owner только после `ALLOWED`, блокировать forbidden part при `PARTIAL_ALLOWED`, не выполнять task при `BLOCKED`.

## Исправленные файлы

- `global/agent-skill-policy.yaml`
- `global/agent-registry.yaml`
- `global/agent-routing-policy.yaml`
- `global/agent-output-contract.md`
- `global/bug-policy.yaml`
- `global/release-policy.yaml`
- `project-overrides/project-policy-template.yaml`
- `README.md`
- `docs/quality-gate-report.md`

## Результаты контрольных проверок

- Expected structure: `PASS`.
- Registry agents count: `21`.
- Skill policy agents count: `21`.
- Routing referenced registered agents count: `21`.
- Registry not in skill policy: `0`.
- Skill policy not in registry: `0`.
- Registry not in routing: `0`.
- Routing agents not in registry: `0`.
- `allowed_skills` / `denied_skills` overlap: `0`.
- Поиск незарегистрированных ссылок `ai-test-automation-engineer`: `0`.
- Поиск устаревшего `open_bug_report`: `0`.

## Решение quality gate

Глобальный governance-пакет можно использовать как soft-enforcement source of truth для будущих Codex-запросов.

Для production hard enforcement пока требуется отдельный validator по `scripts/validate-policy-pseudocode.md`.

## Готовность для AI Discovery Platform

Статус: `READY_FOR_PROJECT_ONBOARDING`

Можно подключать AI Discovery Platform через:

- `domains/ai-rag-platform-policy.yaml`;
- `project-overrides/ai-discovery-platform-policy.example.yaml`;
- `prompt-templates/global-orchestrator-prompt.md`;
- `prompt-templates/agent-preflight-prompt.md`.

Перед любыми изменениями production-кода AI Discovery Platform обязателен preflight, approved task, owner routing и соответствующий quality gate.

## Следующий запрос

Рекомендуемый следующий запрос:

```text
Ты — ai-product-orchestrator. Подключи AI Discovery Platform к ai-agent-governance: создай рабочий project override на основе project-overrides/ai-discovery-platform-policy.example.yaml, проверь domain policy ai-rag-platform, настрой bug rules, LLM/security/data правила и подготовь preflight-инструкцию для будущих Codex-задач. Production-код не менять, Trello/GitHub не менять.
```
