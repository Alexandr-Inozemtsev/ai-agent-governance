# Policy Inheritance

## Слои

- Global Policy: базовые запреты и permissions.
- Domain Policy: уточнения для домена.
- Project Policy: ограничения конкретного репозитория.
- Task Policy: временные ограничения запроса.

## Conflict resolution

Если lower layer конфликтует с higher layer, побеждает более строгий запрет. Allow не может отменить deny.

## Override rules

Project override не может ослаблять global policy. Ослабление требует approval `ai-product-orchestrator` и owner-agent, но даже тогда должно быть documented exception, а не silent bypass.

## Deny precedence

Deny by default применяется для неописанных actions, skills и artifacts.
