# Quality Gate Prompt

Проверь результат агента перед handoff, Trello update, PR, release или closure.

## Checks

- Соответствие global/domain/project/task policy.
- Соответствие роли агента.
- Нет запрещенных changes.
- Нет scope creep.
- Нет дублирования карточек/bugs/docs.
- Есть acceptance criteria и DoD.
- Есть tests/docs/risks там, где требуется.
- Dependency changes имеют ADR + security/license review.
- DB changes имеют migration plan + rollback.
- Bug fix не закрывает bug без QA verification.
- Epic closure не допускается при открытых P0/P1/Critical/High bugs.
- Если задача затрагивает существующий функционал, выполнен QA Automation Gate.
- Если required autotests failed, QA gate не может быть `PASSED`.
- Если required autotests missing, QA gate не может быть `PASSED` без documented exception.
- Если manual regression выполнен до проверки автотестов, результат получает policy violation.
- Если bug закрывается, есть QA verification.
- Если менялись SimpleRetriever / backend / API, есть unit/integration/regression test results.

## Ответ

```json
{
  "status": "PASS | FAIL | NEEDS_APPROVAL",
  "failed_checks": [],
  "blocking_policies": [],
  "required_owner_agent": "...",
  "recommended_next_step": "..."
}
```
