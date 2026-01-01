# TDD 01: BloomOps Schema and Layer 1 Client

## Coverage
- TDD-001, TDD-001a, TDD-002, TDD-003, TDD-004, TDD-004a, TDD-004b, TDD-009, TDD-009a, TDD-009b, TDD-009c
- TDD-005, TDD-006, TDD-007, TDD-008, TDD-008a, TDD-008b

## BloomOps Schema and Parsing

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

ID: TDD-004a  
Given duplicate `scene_plan` IDs, validation fails with the duplicate list.

ID: TDD-004b  
Given out-of-order `scene_plan` entries for a chapter, validation fails and reports the ordering issue.

ID: TDD-009  
Given BloomOps JSON/YAML with unknown fields, schema validation fails (strict fields enforced).

ID: TDD-009a  
Given `doctrine_frozen` missing, validation fails.

ID: TDD-009b  
Given `run_snapshot` missing or `source_hash` mismatch, validation fails.

ID: TDD-009c  
Given invalid `scene_constraints` (missing or non-numeric values), validation fails.

## Layer 1 LLM Client

ID: TDD-005  
Given a user session, the client generates BloomOps Markdown only after explicit user confirmation.

ID: TDD-006  
Given outline guidance, the client records changes to BloomOps and updates JSON/YAML.

ID: TDD-007  
Given scene planning guidance, the client stores scene guidance under the BloomOps doc and updates JSON/YAML.

ID: TDD-008  
Given a request to run Layer 2 with `doctrine_frozen: false`, generation is blocked with a clear error.

ID: TDD-008a  
Given a user sets `doctrine_frozen: true`, the client records the action in an interaction log.

ID: TDD-008b  
Given a user edits BloomOps Markdown after freezing, the client forces `doctrine_frozen: false`.

## QA Checklist
Inputs:
- BloomOps Markdown with valid sections and `scene_plan`
- Variants with duplicate IDs, missing inputs/outputs, malformed `scene_plan`, unknown fields, missing `doctrine_frozen`, missing `run_snapshot`, invalid `scene_constraints`
- User session with outline and scene guidance
Steps:
1. Run Markdown parser and JSON/YAML generation.
2. Run schema validation across all variants.
3. Attempt Markdown write without confirmation.
4. Confirm and generate Markdown + JSON/YAML.
5. Set `doctrine_frozen: true`, then edit Markdown.
Expected:
- Valid inputs succeed with correct `source_hash`.
- Invalid inputs fail with specific errors for each issue.
- No write without confirmation.
- JSON/YAML updates on guidance.
- Freeze is logged; edits auto-unfreeze.
