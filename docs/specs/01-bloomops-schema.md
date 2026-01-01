# Spec 01: BloomOps Schema and Dual Docs

## Purpose
Define the BloomOps documentation format, including the Markdown source of truth and the derived JSON/YAML representation used by Layer 2.

## Normative Rules
- Markdown is authoritative and human-edited.
- JSON/YAML is generated and must be updated whenever Markdown changes.
- Each section must have a stable ID for traceability.
- No automation step may modify the Markdown without explicit user approval.

## Markdown Structure (v0.1)
Each BloomOps doc must include:
- Title
- Intent summary
- User stories
- Bloom verb sections with inputs, outputs, constraints, and prompts
- Assumptions and open questions

### Template
```md
# BloomOps: <project name>

## Intent Summary
<short intent statement>

## User Stories
- US-001: As a <role>, I want <goal>, so that <benefit>.

## Scene Planning
- CH01-SC01: <Chapter 1 - Scene 1 title or short description>
- CH01-SC02: <Chapter 1 - Scene 2 title or short description>
- CH02-SC01: <Chapter 2 - Scene 1 title or short description>

## Bloom Sections
### BO-REMEMBER-001: Remember
Inputs:
- ...
Outputs:
- ...
Constraints:
- ...
Prompts:
- ...

### BO-UNDERSTAND-001: Understand
...

## Assumptions
- AS-001: ...

## Open Questions
- Q-001: ...
```

## JSON/YAML Representation
Derived fields:
- `source_hash`: SHA256 of Markdown
- `sections`: array of Bloom sections with IDs, inputs, outputs, constraints, prompts
- `user_stories`: list of user story objects
- `assumptions` and `open_questions`

### Minimal Schema (conceptual)
```yaml
project:
  name: "BloomOps"
  source_hash: "<sha256>"
  doctrine_frozen: false
user_stories:
  - id: "US-001"
    role: "author"
    goal: "draft a book"
    benefit: "produce a full manuscript"
scene_plan:
  - id: "CH01-SC01"
    label: "Chapter 1 - Opening scene"
  - id: "CH01-SC02"
    label: "Chapter 1 - First conflict"
sections:
  - id: "BO-CREATE-001"
    verb: "create"
    inputs: []
    outputs: []
    constraints: []
    prompts: []
assumptions: []
open_questions: []
```

## Validation Rules
- All section IDs are unique.
- Each Bloom section includes inputs and outputs.
- `source_hash` must match the Markdown file content.
- Any automation output must include `trace_ids` referencing Bloom section IDs.
- Scene plan IDs must be human-readable and stable (format `CH##-SC##`).
- `doctrine_frozen` must be true before Layer 2 generation.

## Layer 1 LLM Client (BloomOps Authoring)

### Purpose
Provide a user-facing LLM client that helps author BloomOps docs, including outline creation and scene iteration guidance.

### Delivery
- v0.1 may be a Gradio UI, CLI, or simple web client.
- UI must be optional; BloomOps docs remain editable in Markdown.

### Core Flows
1. Capture project intent and create the initial BloomOps Markdown.
2. Assist with series outline generation and refinement.
3. Assist with chapter outline and scene list iteration.
4. Record assumptions and open questions for unresolved items.

### Data Outputs
- BloomOps Markdown (authoritative)
- BloomOps JSON/YAML (derived)
- Interaction log (optional but recommended)

### Constraints
- Must not change BloomOps docs without user confirmation.
- Must record which Bloom sections were updated by the user.

### Suggested UI Sections
- Intent Summary
- User Stories
- Outline Builder
- Scene Planning
- Assumptions / Open Questions
