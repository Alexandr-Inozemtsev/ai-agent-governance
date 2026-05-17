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
11. Bug report создает `ai-qa-engineer`.
12. Release decision принимает `ai-release-manager`.
