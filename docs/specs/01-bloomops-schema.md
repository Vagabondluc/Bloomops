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
user_stories:
  - id: "US-001"
    role: "author"
    goal: "draft a book"
    benefit: "produce a full manuscript"
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

