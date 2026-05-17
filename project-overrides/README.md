# Project Overrides

Project override уточняет global и domain policy для конкретного репозитория, Trello-доски и delivery-контекста.

Главное правило: project override не может ослаблять global policy. Если правило проекта конфликтует с global policy, побеждает global policy. Ослабление возможно только через явное approval `ai-product-orchestrator` и owner-агента соответствующей зоны.

Порядок подключения проекта:

1. Выбрать domain policy.
2. Скопировать `project-policy-template.yaml`.
3. Заполнить `project_id`, repository, Trello board и allowed agents.
4. Указать project-specific restrictions.
5. Настроить bug rules.
6. Запустить preflight по `prompt-templates/agent-preflight-prompt.md`.
