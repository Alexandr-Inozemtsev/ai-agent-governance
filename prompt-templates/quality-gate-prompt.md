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
- Если задача large/critical, был decomposition plan.
- Если required agent missing, его часть не была выполнена.
- Если был status change, есть `proposed_status_update`.
- Если изменились сроки/зависимости/блокеры, есть Gantt impact.
- Если Trello update required, указан `ai-trello-analyst`.
- Если Gantt update required, указан `ai-delivery-project-manager`.
- Если task touches existing functionality, учтён QA Automation Gate.
- Если required autotests failed/missing, QA gate не может быть `PASSED`.
- Если epic закрывается, нет открытых P0/P1/Critical/High bugs.
- Если technical plan на английском, есть `user_review_summary_ru`.
- Если пользователю предоставлен только английский план, результат `BLOCKED` или `NEEDS_USER_REVIEW_SUMMARY`.

## Ответ

```json
{
  "status": "PASS | FAIL | NEEDS_APPROVAL | NEEDS_USER_REVIEW_SUMMARY",
  "failed_checks": [],
  "blocking_policies": [],
  "required_owner_agent": "...",
  "recommended_next_step": "..."
}
```
