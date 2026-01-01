# Spec 07: Book Pipeline Nodes and Artifacts

## Purpose
Define the concrete node chain for generating a full book with per-chapter loops and multi-pass edits.

## Inputs
- BloomOps docs (Markdown + JSON/YAML)
- `docs/book/Jason's Prompts.md`
- Optional reference prompts in `docs/book/Novel Crafter/`

## Global Artifacts
- `artifacts/series-outline.md`
- `artifacts/callsheet.md`
- `artifacts/characters.md`
- `artifacts/worldbuilding.md`
- `artifacts/outline.md`
- `artifacts/style-sheet.md`
- `artifacts/prohibited-words.txt`
- `artifacts/manuscript.md`

## Per-Chapter Artifacts
For each chapter `CH-###`:
- `artifacts/chapters/CH-###/scenes/SC-###/scene-brief.md`
- `artifacts/chapters/CH-###/scenes/SC-###/draft.md`
- `artifacts/chapters/CH-###/scenes/SC-###/improvement-plan.md`
- `artifacts/chapters/CH-###/scenes/SC-###/revised.md`
- `artifacts/chapters/CH-###/scenes/SC-###/copyproof.md`
- `artifacts/chapters/CH-###/scenes/SC-###/tighten-1.md`
- `artifacts/chapters/CH-###/scenes/SC-###/tighten-2.md`
- `artifacts/chapters/CH-###/scenes/SC-###/final.md`
- `artifacts/chapters/CH-###/chapter.md`

## Node Chain (Global)
1. `generate-callsheet`
2. `generate-characters`
3. `generate-worldbuilding`
4. `generate-outline`
5. `generate-style-sheet`

## Node Chain (Per Chapter)
1. `derive-scene-list` (reads `scene_plan` from BloomOps JSON/YAML)
2. For each scene:
   1. `generate-scene-brief`
   2. `draft-scene`
   3. `critique-scene`
   4. `apply-scene-improvement`
   5. `copyproof-scene`
   6. `tighten-scene-pass-1`
   7. `tighten-scene-pass-2`
   8. `append-scene`
3. `compile-chapter`
4. `append-chapter`

## Append and Progression Rules
- `append-scene` uses `final.md` for each scene.
- `compile-chapter` concatenates scenes in order to `chapter.md`.
- `append-chapter` uses `chapter.md` for each chapter.
- Chapter order is derived from the outline.
- The loop advances only after append succeeds.
- Previous scene text is passed into the next scene brief and draft nodes.
- Previous chapter text is passed into the first scene of the next chapter.

## Correction and Rollback
- If a scene fails validation after append, mark it invalid and regenerate the scene.
- Regenerated scenes must create a new versioned artifact and re-append.
- Chapter compilation must use the latest valid version of each scene.

## Verification Hooks
- Each node emits a summary and checksum for its output.
- Each chapter includes word count, POV, and prohibited word checks.
