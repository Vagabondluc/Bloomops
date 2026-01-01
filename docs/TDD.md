# TDD: BloomOps System

## Scope
Tests cover BloomOps doc parsing, Layer 2 generation, Layer 3 worker execution, and the v0.1 book workflow.

## Test Matrix

### 1) BloomOps Markdown to JSON/YAML
ID: TDD-001  
Given a BloomOps Markdown doc, when the parser runs, then a JSON/YAML file is generated with matching `source_hash`.

ID: TDD-002  
Given duplicate section IDs, when validation runs, then it fails with a clear error.

ID: TDD-003  
Given a BloomOps section without inputs or outputs, when validation runs, then it fails.

### 2) Traceability
ID: TDD-010  
Given a PRD requirement, it must include `trace_ids` that exist in BloomOps.

ID: TDD-011  
Given a spec item with `trace_ids`, all IDs must resolve to a BloomOps section or user story.

### 3) Assumptions
ID: TDD-020  
Given missing required inputs, Layer 2 generates an assumption entry and alerts the user.

ID: TDD-021  
Assumption entries include reason, impact, and trace IDs.

### 4) Critique Pass
ID: TDD-030  
Given a non-testable requirement, the critique pass flags it and suggests a fix.

ID: TDD-031  
Given missing trace IDs, the critique pass reports the missing links.

### 5) Book Workflow (v0.1)
ID: TDD-040  
Given `book/Jason's Prompts.md`, the system maps each step to Bloom verbs as specified in `docs/specs/04-book-workflow.md`.

ID: TDD-041  
Given the call sheet prompt inputs, the output matches the required Markdown format.

ID: TDD-042  
Given character and worldbuilding inputs, the outline output includes chapter summaries with 200-250 words each.

### 6) Worker Interface
ID: TDD-050  
Given a worker input payload, the worker returns `output.json` and `log.json`.

ID: TDD-051  
Worker logs include command, model, and duration.

### 7) Smoke Tests
ID: TDD-060  
Run a minimal end-to-end book workflow: outline -> scene brief -> draft chapter -> improvement plan -> apply edits. Each step emits artifacts and logs.

ID: TDD-061  
Any failed step halts execution and reports the last successful artifact.

