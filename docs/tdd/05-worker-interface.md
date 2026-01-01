# TDD 05: Worker Interface

## Coverage
- TDD-050, TDD-051, TDD-052, TDD-053, TDD-054, TDD-055, TDD-056, TDD-057

## Worker I/O and Logs

ID: TDD-050  
Given a worker input payload, the worker returns `output.json` and `log.json`.

ID: TDD-051  
Worker logs include command, model, and duration.

ID: TDD-052  
Worker logs include timestamp, inputs used, and trace IDs.

ID: TDD-053  
Worker logs include provider and model identifier for LLM calls (e.g., `ollama:llama3`).

ID: TDD-054  
Given `derive-scene-list`, output contains ordered scene IDs matching BloomOps `scene_plan`.

ID: TDD-055  
Append is idempotent for `scene_id` and `chapter_id`.

ID: TDD-056  
Worker returns `status: failure` with error details when an input is missing.

ID: TDD-057  
Given a worker action, required inputs and outputs match the action I/O contract.

## QA Checklist
Inputs:
- Valid/invalid worker payloads
Steps:
1. Execute worker with valid payload.
2. Execute worker with missing inputs.
Expected:
- `output.json`/`log.json` always produced.
- Logs include provider/model and trace IDs.
- Missing inputs return structured failure.
