# Spec 02: Layer 2 Generator (PRD/Specs/TDD)

## Purpose
Define how Layer 2 converts BloomOps docs into PRD, specs, and TDD artifacts, including assumption logging and critique steps.

## Inputs
- BloomOps Markdown (authoritative)
- BloomOps JSON/YAML (derived)
- Prompt library (e.g., `book/Jason's Prompts.md`)

## Outputs
- `docs/PRD.md`
- `docs/specs/*.md`
- `docs/TDD.md`
- `docs/assumptions.md`
- `docs/critiques/*.md`

## Normative Rules
- No new requirements may be introduced without a trace to a BloomOps ID.
- Every requirement in PRD/specs/TDD includes `trace_ids`.
- Any missing data must generate an assumption entry and a user-facing notice.
- Critiques must identify gaps, contradictions, and testability issues.
- Layer 2 must refuse to run unless `doctrine_frozen` is true.
- Layer 2 must refuse to run unless `run_snapshot.source_hash` matches the current BloomOps `source_hash`.
- Assumptions require explicit user acceptance before downstream generation continues.

## Assumption Log Format
```md
# Assumptions
- AS-001
  - reason: missing constraint for chapter length
  - impact: TDD word-count test uses default 3000 words
  - trace_ids: [BO-APPLY-001]
```

## Critique Pass
Layer 2 runs a critique prompt against PRD/specs/TDD with the following rules:
- Identify missing trace IDs.
- Identify ambiguous requirements.
- Identify non-testable statements.
- Provide a fix list with exact sections to change.
- Critique must use a distinct model or a deterministic lint pass from the generation model.

## Traceability
Each requirement in PRD/specs/TDD includes:
```md
trace_ids: [BO-ANALYZE-002, US-003]
```
