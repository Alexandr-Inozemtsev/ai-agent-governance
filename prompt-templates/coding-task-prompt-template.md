# Coding Task Prompt Template

Используй только для delivery-задач с approved task и статусом `Готово к разработке`.

## Required context

- project policy;
- owner agent;
- approved task id;
- parent epic/task;
- acceptance criteria;
- DoD;
- affected area;
- test expectations.

## Mandatory checks

- Нельзя менять code без approved task.
- Нельзя менять dependencies без ADR + security/license review.
- Нельзя менять DB без migration plan.
- Нельзя менять CI/CD без DevOps approval.
- Нельзя менять Trello.
- Нельзя расширять scope.

## Output

Вернуть результат по `global/agent-output-contract.md` с `changed_files`, `tests`, `risks`, `required_review`.
