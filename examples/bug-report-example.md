# Bug Report Example

```yaml
bug_id: "БАГ-ЭПИК-04-001"
title: "Problem generation не использует релевантные chunks из SimpleRetriever"
parent_epic_id: "ЭПИК-04"
parent_epic_title: "RAG-based problem generation"
parent_task_id: "TASK-04-07"
parent_task_title: "Generate problem from retrieved context"
affected_area: "LLM/RAG"
severity: "High"
priority: "P1"
environment: "local QA / test dataset"
steps_to_reproduce:
  - "Загрузить test corpus с явно релевантным chunk."
  - "Запустить generation flow."
  - "Сравнить prompt/context с returned chunks SimpleRetriever."
actual_result: "Generated problem не опирается на top relevant chunks."
expected_result: "Generated problem использует релевантные chunks и сохраняет source trace."
evidence:
  - "retriever log: top chunk содержит нужный факт"
  - "generated output не содержит факт"
regression_risk: "High"
linked_pr: ""
linked_test_case: "test_problem_generation_uses_retrieved_chunks"
recommended_owner_agent: "ai-llm-rag-engineer"
blocks_epic_completion: true
requires_product_review: false
requires_security_review: false
requires_release_review: false
definition_of_done_for_fix:
  - "Generation prompt получает top chunks."
  - "Source trace сохраняется."
  - "Добавлен regression test."
  - "QA verification passed."
```
