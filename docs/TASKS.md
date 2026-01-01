# Task List (v0.1) Based on TDD

## Phase 0: Foundations
### 0.1 BloomOps Schema and Parser
1. Define strict JSON/YAML schema, including `scene_plan` and `doctrine_frozen`. (TDD-001, TDD-004, TDD-009, TDD-009a)
2. Implement Markdown parser and source hash generation. (TDD-001, TDD-001a)
3. Add validation for IDs, ordering, and required fields. (TDD-002, TDD-003, TDD-004a, TDD-004b)

## Phase 1: Layer 1 LLM Client (BloomOps Authoring)
### 1.1 Session and Confirmation
1. Implement user confirmation gate before writing Markdown. (TDD-005)
2. Log confirmation and freeze actions to interaction log. (TDD-008a)
3. Auto-unfreeze on Markdown edits. (TDD-008b)

### 1.2 Outline and Scene Planning
1. Capture outline guidance and update Markdown + JSON/YAML. (TDD-006)
2. Capture `scene_plan` guidance and update Markdown + JSON/YAML. (TDD-007)

## Phase 2: Layer 2 Generator
### 2.1 Gating and Traceability
1. Enforce `doctrine_frozen` before any generation. (TDD-008, TDD-032)
2. Implement trace ID validation across PRD/specs/TDD. (TDD-010, TDD-011, TDD-010a, TDD-012, TDD-013)

### 2.2 Assumptions and Critique
1. Generate assumption log file and CLI notifications. (TDD-020, TDD-021, TDD-022, TDD-023, TDD-024)
2. Implement critique pass with fix list output. (TDD-030, TDD-031, TDD-033)

## Phase 3: Worker Interface
### 3.1 Payloads and Logs
1. Implement standard worker input/output files. (TDD-050)
2. Enforce log fields (command, model, duration, timestamps, trace IDs). (TDD-051, TDD-052)
3. Record provider and model identifiers (Ollama supported). (TDD-053)
4. Return structured failure responses on missing inputs. (TDD-056)

### 3.2 Book Actions
1. Implement `derive-scene-list` using BloomOps `scene_plan`. (TDD-054)
2. Implement idempotent append for scenes and chapters. (TDD-055)

## Phase 4: Orchestration Engine (n8n-like)
### 4.1 Workflow Validation
1. Validate DAG and detect cycles. (TDD-070, TDD-076)
2. Enforce dependency ordering and scene order. (TDD-071, TDD-075)

### 4.2 Execution and Recovery
1. Implement retries with backoff and logging. (TDD-072, TDD-074)
2. Persist outputs and resume from last success. (TDD-073)
3. Support parallel branches and deterministic merges. (TDD-077)

## Phase 5: Book Workflow Implementation
### 5.1 Prewriting Outputs
1. Callsheet generation matches required format and section order. (TDD-041, TDD-041a)
2. Outline generation uses required headings and summary length. (TDD-042, TDD-042a)
3. Style sheet generation includes required sections and snippets. (TDD-043)

### 5.2 Scene Pipeline
1. Scene brief includes required fields and verbatim plot summary. (TDD-044, TDD-044a)
2. Scene draft respects constraints and continuity. (TDD-045, TDD-045a, TDD-045b)
3. Improvement plan and apply pass preserve structure. (TDD-046, TDD-047)
4. Copyproof pass preserves plot and headings. (TDD-048, TDD-048a)
5. Tighten passes preserve meaning and constraints. (TDD-049, TDD-049a)
6. Append scene and compile chapter maintain order and boundaries. (TDD-049b, TDD-049c, TDD-049e)
7. Append chapter maintains manuscript order. (TDD-049d)

### 5.3 Artifact Checks
1. Verify global artifacts exist. (TDD-090)
2. Verify per-scene artifacts exist. (TDD-091)
3. Verify chapter compilation and manuscript append. (TDD-092, TDD-093)
4. Verify checksums, summaries, and scene checks. (TDD-094, TDD-095, TDD-096)

## Phase 6: Layer 3 Agent
### 6.1 Planning and Execution
1. Generate task plans with trace IDs. (TDD-080)
2. Log each worker step and output. (TDD-081, TDD-083)
3. Honor retry policies and record attempts. (TDD-086)

### 6.2 Safeguards
1. Block BloomOps edits without approval. (TDD-084)
2. Halt on `doctrine_frozen: false`. (TDD-085)
3. Exit non-zero and summarize on worker failure. (TDD-082, TDD-087)

## Phase 7: End-to-End Verification
1. Run minimal pipeline smoke test. (TDD-060, TDD-061)
2. Run two-scene continuity test. (TDD-062)
3. Run two-chapter continuity test. (TDD-063)
4. Run one-chapter two-scene manuscript test. (TDD-064)
