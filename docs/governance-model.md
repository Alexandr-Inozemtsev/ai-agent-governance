# Governance Model

1. Пользовательский запрос поступает `ai-product-orchestrator`.
2. Orchestrator запускает preflight.
3. Запрос классифицируется по task type.
4. Выбираются owner agent и contributor agents.
5. Проверяются skills, artifacts, actions, repo, branch, Trello, dependency, DB, security, QA, release и bug rules.
6. Агент выполняет только разрешенную часть.
7. Результат возвращается по output contract.
8. Quality gate проверяет DoD, tests, docs, risks и policy compliance.
9. Trello update делает `ai-trello-analyst`.
10. GitHub PR проходит review и QA.
11. Bug report создает `ai-qa-engineer` или `ai-test-automation-engineer`, если дефект выявлен автоматизированным тестом.
12. `ai-test-automation-engineer` выполняет автотесты и передает результат `ai-qa-engineer`.
13. `ai-qa-engineer` принимает QA gate и проверяет баги.
14. Test automation не равен QA approval: успешный прогон автотестов не закрывает QA gate без `ai-qa-engineer`.
15. Release decision принимает `ai-release-manager`.
