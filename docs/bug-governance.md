# Bug Governance

## Bug report

Bug report — QA artifact, который фиксирует дефект, parent, severity, priority, environment, steps, actual/expected result, evidence, regression risk и recommended owner.

## Trello bug card

Trello bug card — operational card для tracking. Ее создает `ai-trello-analyst`, кроме fast mode, где project policy явно разрешает QA создавать bug cards.

## Parent обязателен

Баг должен быть связан с epic/task/PR/test case/release candidate/incident. Для плановой разработки основной parent — epic.

## Как баг блокирует эпик

Parent epic checklist `Баги / дефекты` должен содержать открытые bug cards. Epic нельзя закрыть при открытых P0/P1/Critical/High bugs, security blockers или failed acceptance criteria.

## Закрытие бага

Баг закрывается только после implemented fix, tests added/updated, QA verification passed, regression risk assessed и обновления Trello/epic checklist.

## Bug vs change request

Если исправление требует нового поведения, изменения требований, бизнес-логики или UX scope, статус становится `NEEDS_PRODUCT_REVIEW`, owner — `ai-product-orchestrator`.
