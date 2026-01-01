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

## Action I/O Requirements (v0.1)
- `generate-callsheet` inputs: `braindump`, `genre_tropes`; outputs: `callsheet_path`
- `generate-characters` inputs: `braindump`, `callsheet`, `genre_tropes`; outputs: `characters_path`
- `generate-worldbuilding` inputs: `braindump`, `callsheet`, `genre_tropes`; outputs: `worldbuilding_path`
- `generate-outline` inputs: `worldbuilding`, `characters`, `braindump`, `genre_tropes`, `outline_template`; outputs: `outline_path`
- `generate-style-sheet` inputs: `writing_samples`; outputs: `style_sheet_path`
- `generate-scene-brief` inputs: `outline`, `characters`, `worldbuilding`, `previous_scene_text`, `chapter_label`; outputs: `scene_brief_path`
- `draft-scene` inputs: `scene_brief`, `style_sheet`, `prose_style_example`, `prohibited_words`, `context`; outputs: `draft_path`
- `critique-scene` inputs: `draft`, `scene_brief`, `style_sheet`, `prose_style_example`, `prohibited_words`; outputs: `improvement_plan_path`
- `apply-scene-improvement` inputs: `draft`, `improvement_plan`; outputs: `revised_path`
- `copyproof-scene` inputs: `revised`; outputs: `copyproof_path`
- `tighten-scene-pass-1` inputs: `copyproof`; outputs: `tighten1_path`
- `tighten-scene-pass-2` inputs: `tighten1`; outputs: `final_path`
- `append-scene` inputs: `chapter_path`, `scene_path`, `scene_id`; outputs: `chapter_path`, `chapter_checksum`
- `compile-chapter` inputs: `chapter_path`, `scene_paths[]`; outputs: `chapter_path`
- `append-chapter` inputs: `manuscript_path`, `chapter_path`, `chapter_id`; outputs: `manuscript_path`, `manuscript_checksum`
