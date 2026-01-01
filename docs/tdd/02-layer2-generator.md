# TDD 02: Layer 2 Generator

## Coverage
- TDD-010, TDD-010a, TDD-011, TDD-012, TDD-013
- TDD-020, TDD-021, TDD-022, TDD-023, TDD-024, TDD-025
- TDD-030, TDD-031, TDD-032, TDD-033, TDD-034, TDD-035

## Traceability

ID: TDD-010  
Given a PRD requirement, it must include `trace_ids` that exist in BloomOps.

ID: TDD-010a  
Given an untraceable requirement, validation fails and reports the missing BloomOps/User Story IDs.

ID: TDD-011  
Given a spec item with `trace_ids`, all IDs must resolve to a BloomOps section or user story.

ID: TDD-012  
Given a requirement without `trace_ids` and no assumption entry, validation fails.

ID: TDD-013  
Given a requirement derived from an assumption, the requirement includes the assumption ID in metadata.

## Assumptions

ID: TDD-020  
Given missing required inputs, Layer 2 generates an assumption entry and alerts the user.

ID: TDD-021  
Assumption entries include reason, impact, and trace IDs.

ID: TDD-022  
Assumption notifications are emitted to CLI output and a generated file.

ID: TDD-023  
Assumption file includes a stable ID, timestamp, and trace IDs for each entry.

ID: TDD-024  
CLI output includes the assumption ID and file path.

ID: TDD-025  
Given unaccepted assumptions, downstream generation is blocked.

## Critique Pass and Gating

ID: TDD-030  
Given a non-testable requirement, the critique pass flags it and suggests a fix.

ID: TDD-031  
Given missing trace IDs, the critique pass reports the missing links.

ID: TDD-032  
Given `doctrine_frozen: false`, Layer 2 refuses to run and emits a clear error.

ID: TDD-033  
Given a critique pass, the output includes a fix list with exact target sections.

ID: TDD-034  
Given a critique pass, the model/provider differs from the generation step.

ID: TDD-035  
Given a `run_snapshot` mismatch, Layer 2 refuses to run.

## QA Checklist
Inputs:
- PRD/spec/TDD with valid trace IDs
- Variants with missing or invalid trace IDs, or assumption-derived requirements
- Missing required input for a generation step
- Requirements with non-testable statements and missing trace IDs
- JSON/YAML with `doctrine_frozen: false`
- JSON/YAML with mismatched `run_snapshot`
Steps:
1. Run trace validation across artifacts.
2. Run Layer 2 generation with missing data.
3. Run critique pass on artifacts.
4. Attempt Layer 2 generation with frozen false.
5. Attempt Layer 2 generation with unaccepted assumptions.
6. Attempt Layer 2 generation with snapshot mismatch.
Expected:
- Valid trace IDs pass.
- Missing/invalid trace IDs fail with clear errors.
- Assumption entry created with reason/impact/trace IDs and CLI notice.
- Critique outputs fix list and missing trace IDs.
- Generation is blocked with clear error.
