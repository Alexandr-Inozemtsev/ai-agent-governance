# Preflight для AI Discovery Platform

Перед любой задачей по проекту AI Discovery Platform нужно выполнить preflight в governance-репозитории `ai-agent-governance`.

1. Прочитать global policies из `global/`.
2. Прочитать domain policy `domains/ai-rag-platform-policy.yaml`.
3. Прочитать project override `project-overrides/ai-discovery-platform-policy.yaml`.
4. Выполнить preflight по `prompt-templates/agent-preflight-prompt.md`.
5. Если результат `ALLOWED` - выполнять задачу в рамках разрешенного owner agent и действующих quality gates.
6. Если результат `BLOCKED` - остановиться и указать нарушенное правило.
7. Если результат `NEEDS_APPROVAL` - указать, чье согласование нужно, например `ai-product-orchestrator`, профильного owner agent, security review, license review или ADR approval.

Запрещено в рамках preflight-задач менять production-код AI Discovery Platform, репозиторий AI Discovery Platform, Trello-доску, GitHub issues/PR и runtime-зависимости без отдельного разрешения.
