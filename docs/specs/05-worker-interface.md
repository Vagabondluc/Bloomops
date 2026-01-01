# Spec 05: Worker Interface

## Purpose
Define the standard interface for worker scripts used by the Layer 3 agent.

## Contract
Each worker must accept:
- `input.json` (task payload)
- `context.json` (trace IDs, constraints, prior outputs)

Each worker must return:
- `output.json` (artifact or status)
- `log.json` (commands, model used, timings)

## Minimal Input Schema
```json
{
  "task_id": "TASK-001",
  "action": "generate-outline",
  "inputs": {
    "braindump": "...",
    "genre_tropes": "..."
  },
  "constraints": {
    "format": "markdown"
  },
  "trace_ids": ["BO-CREATE-001"]
}
```

## Minimal Output Schema
```json
{
  "task_id": "TASK-001",
  "status": "success",
  "artifact_path": "artifacts/outline.md",
  "summary": "Generated outline for <book title>"
}
```

