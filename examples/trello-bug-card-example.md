# Trello Bug Card Example

## Название

`БАГ-ЭПИК-04-001: Problem generation не использует релевантные chunks из SimpleRetriever`

## Labels

- Баг
- QA
- ЭПИК-04
- Severity:High
- Priority:P1
- Area:LLM/RAG

## Description

- Parent epic: `ЭПИК-04 — RAG-based problem generation`
- Parent task: `TASK-04-07`
- Severity: High
- Priority: P1
- Environment: local QA / test dataset
- Actual result: generated problem не опирается на top relevant chunks.
- Expected result: generated problem использует relevant chunks и source trace.
- Owner agent: `ai-llm-rag-engineer`

## Checklist: DoD

- Fix implemented.
- Regression test added.
- Source trace verified.
- QA verification passed.
- Parent epic checklist `Баги / дефекты` updated.
