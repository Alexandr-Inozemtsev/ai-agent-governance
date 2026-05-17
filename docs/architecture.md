# Архитектура Agent Policy Engine

## Назначение

Agent Policy Engine — глобальный governance-layer для Codex Desktop / Codex CLI. Он задает роли агентов, permissions, routing, блокировки и quality gates для всех проектов.

## Компоненты

- `global/` — базовые rules и source of truth.
- `domains/` — доменные уточнения: web, AI/RAG, game, mobile, analytics, enterprise, docs-only.
- `project-overrides/` — project-specific restrictions.
- `prompt-templates/` — prompts для preflight, routing, blocked response, QA и handoff.
- `docs/` — объяснение operating model.
- `examples/` — демонстрационные сценарии.
- `scripts/validate-policy-pseudocode.md` — будущий hard validator.

## Policy inheritance

Правила применяются как `Global -> Domain -> Project -> Task`. Любой нижний слой может только ужесточать. Deny имеет приоритет над allow.

## Soft enforcement сейчас

Codex читает policy-файлы и применяет их через preflight, routing prompts и output contract.

## Hard enforcement в будущем

Validator сможет классифицировать запросы, обнаруживать actions/skills/artifacts и блокировать нарушения до выполнения tool call.

## Интеграции

С репозиториями policy связывается через project override. С Trello — через `global/trello-policy.yaml` и bug policy. С GitHub — через branch/PR/review/release rules. С Codex Desktop — через orchestrator prompt и preflight prompt.
