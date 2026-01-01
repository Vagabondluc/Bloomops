# TDD: BloomOps System

## Scope
Tests cover BloomOps doc parsing, Layer 2 generation, Layer 3 worker execution, and the v0.1 book workflow.

## Test Matrix

### 1) BloomOps Markdown to JSON/YAML
ID: TDD-001  
Given a BloomOps Markdown doc, when the parser runs, then a JSON/YAML file is generated with matching `source_hash`.

ID: TDD-001a  
Given an updated BloomOps Markdown doc, when the parser runs, then JSON/YAML content and `source_hash` change to match the new Markdown.

ID: TDD-002  
Given duplicate section IDs, when validation runs, then it fails with a clear error.

ID: TDD-003  
Given a BloomOps section without inputs or outputs, when validation runs, then it fails.

ID: TDD-004  
Given missing `scene_plan` entries or malformed scene IDs, validation fails and reports the invalid items.

### 1a) Layer 1 LLM Client
ID: TDD-005  
Given a user session, the client generates BloomOps Markdown only after explicit user confirmation.

ID: TDD-006  
Given outline guidance, the client records changes to BloomOps and updates JSON/YAML.

ID: TDD-007  
Given scene planning guidance, the client stores scene guidance under the BloomOps doc and updates JSON/YAML.

ID: TDD-008  
Given a request to run Layer 2 with `doctrine_frozen: false`, generation is blocked with a clear error.

### 2) Traceability
ID: TDD-010  
Given a PRD requirement, it must include `trace_ids` that exist in BloomOps.

ID: TDD-010a  
Given an untraceable requirement, validation fails and reports the missing BloomOps/User Story IDs.

ID: TDD-011  
Given a spec item with `trace_ids`, all IDs must resolve to a BloomOps section or user story.

### 3) Assumptions
ID: TDD-020  
Given missing required inputs, Layer 2 generates an assumption entry and alerts the user.

ID: TDD-021  
Assumption entries include reason, impact, and trace IDs.

ID: TDD-022  
Assumption notifications are emitted to CLI output and a generated file.

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

ID: TDD-043  
Given style sheet inputs, the output includes all required sections and example snippets.

ID: TDD-044  
Given scene brief inputs, the output includes all required fields (POV, beats, setting, conflict, continuity).

ID: TDD-045  
Given scene draft inputs, the output respects prohibited words, POV, and word-count constraints.

ID: TDD-046  
Given an improvement plan prompt, the output includes a clear, ordered edit plan referencing the scene brief.

ID: TDD-047  
Given an improvement plan and draft, the edit pass updates only the specified issues and preserves scene structure.

ID: TDD-048  
Given a revised scene, the copyproof pass removes grammar errors and AI-isms without changing plot events.

ID: TDD-049  
Given a copyproofed scene, tighten pass 1 reduces wordiness while preserving meaning.

ID: TDD-049a  
Given a tighten pass 1 output, tighten pass 2 applies a final polish without reintroducing prohibited words.

ID: TDD-049b  
Given scene outputs, append-scene adds content to the chapter once per scene ID and preserves order.

ID: TDD-049c  
Given scene outputs for a chapter, compile-chapter concatenates scenes in order and produces `chapter.md`.

ID: TDD-049d  
Given chapter outputs, append-chapter adds content to the manuscript once per chapter ID and preserves order.

### 6) Worker Interface
ID: TDD-050  
Given a worker input payload, the worker returns `output.json` and `log.json`.

ID: TDD-051  
Worker logs include command, model, and duration.

ID: TDD-052  
Worker logs include timestamp, inputs used, and trace IDs.

### 7) Worker Orchestration (n8n-like)
ID: TDD-070  
Given a workflow definition with a cycle, validation fails and reports the cycle.

ID: TDD-071  
Given a workflow DAG, nodes only run after all dependencies succeed.

ID: TDD-072  
Given a node failure with retries configured, the node retries with backoff and logs each attempt.

ID: TDD-073  
Given a partial run, the system can resume from the last successful node using persisted outputs.

ID: TDD-074  
Each node run produces a log entry with inputs, outputs, status, timing, and retry count.

### 7) Smoke Tests
ID: TDD-060  
Run a minimal end-to-end book workflow: outline -> scene brief -> draft chapter -> improvement plan -> apply edits. Each step emits artifacts and logs.

ID: TDD-061  
Any failed step halts execution and reports the last successful artifact.

ID: TDD-062  
Run an end-to-end scene loop for two scenes and verify the second scene uses previous scene text.

ID: TDD-063  
Run an end-to-end chapter loop for two chapters and verify the first scene of chapter 2 uses previous chapter text.
