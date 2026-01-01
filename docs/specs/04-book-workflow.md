# Spec 04: Book Workflow (BloomOps Mapping)

## Purpose
Define the v0.1 end-to-end book workflow using `book/Jason's Prompts.md` and map each step to Bloom verbs.

## Source
- `book/Jason's Prompts.md`

## Bloom Mapping
- Brainstorming a series: CREATE (generate ideas), UNDERSTAND (summarize tropes)
- Call sheet: ANALYZE (decompose needs), APPLY (format checklist)
- Characters: CREATE (character details), APPLY (format)
- Worldbuilding: CREATE (settings), APPLY (format)
- Outline: CREATE (chapter summaries)
- Style sheet: ANALYZE (derive style rules)
- Scene brief: ANALYZE (decompose scene), APPLY (format)
- First draft: CREATE (chapter text)
- Improvement plan: EVALUATE (critique)
- Implement plan: APPLY (edit within constraints)

## Required Artifacts
- series outline
- callsheet
- character list
- worldbuilding list
- full outline
- style sheet
- scene briefs (per scene)
- scene drafts (per scene)
- scene improvement plan (per scene)
- scene revised (per scene)
- scene copyproof (per scene)
- scene tighten pass 1 (per scene)
- scene tighten pass 2 (per scene)
- compiled chapter (per chapter, from scenes)
- compiled manuscript (all chapters in order, from compiled chapters)

## Workflow Contract
- Each artifact has a required input list and output format.
- Each step must reference prior artifacts via trace IDs.
- Any missing input triggers an assumption log entry.
- Chapter processing is a nested loop: for each chapter, iterate through its scenes and generate scene brief, draft, critique, edit, copyproof, tighten, then append scene to chapter.
- After all scenes in a chapter are appended, compile the chapter and append to manuscript.
- Append operations must be clean and deterministic (no edits to prior scenes/chapters unless explicitly requested).

## Chapter + Scene Loop (v0.1)
For each chapter in outline order:
1. Derive scene list for the chapter (from outline summary and BloomOps `scene_plan` captured with the user).
2. For each scene in scene order:
   1. Build scene brief (uses outline, characters, worldbuilding, previous chapter/scene text).
   2. Draft scene (uses scene brief + style sheet + prohibited words + context).
   3. Generate improvement plan (critique pass).
   4. Apply improvement plan (edit pass).
   5. Copyproof pass (grammar/consistency/cliches/AI-isms).
   6. Tighten pass 1 (line tightening).
   7. Tighten pass 2 (final polish).
   8. Append scene to chapter (append-only).
3. Compile chapter from appended scenes.
4. Append chapter to manuscript (append-only).
