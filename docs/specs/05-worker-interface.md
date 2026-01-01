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

## LLM Providers
- Workers may use Ollama as an LLM provider.
- Logs must include the provider name and model identifier (e.g., `ollama:llama3`).

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

## Book Worker Actions (v0.1)
Required actions for the book pipeline:
- `generate-callsheet`
- `generate-characters`
- `generate-worldbuilding`
- `generate-outline`
- `generate-style-sheet`
- `derive-scene-list`
- `generate-scene-brief`
- `draft-scene`
- `critique-scene`
- `apply-scene-improvement`
- `copyproof-scene`
- `tighten-scene-pass-1`
- `tighten-scene-pass-2`
- `append-scene`
- `compile-chapter`
- `append-chapter`

## Append Worker Requirements
- Input includes `manuscript_path`, `chapter_path`, and `chapter_id` for chapter append.
- Input includes `chapter_path`, `scene_path`, and `scene_id` for scene append.
- Output includes target path and a checksum.
- Append is idempotent per `chapter_id` or `scene_id` to avoid duplicates.

## derive-scene-list Requirements
- Input includes `scene_plan` from BloomOps JSON/YAML.
- Output emits an ordered list of scene IDs and labels for the chapter.
