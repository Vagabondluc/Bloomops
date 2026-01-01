# TDD QA Guide

## How to Run QA (Checklist)
1. Validate BloomOps Markdown -> JSON/YAML generation.
2. Run schema validation (IDs, scene_plan, strict fields, doctrine_frozen).
3. Verify Layer 1 confirmation, freeze/unfreeze behavior.
4. Validate trace IDs across PRD/specs/TDD.
5. Run Layer 2 generation with assumption logging and critique pass.
6. Execute worker interface tests (I/O, logs, failures).
7. Execute orchestration tests (DAG, retries, ordering).
8. Run end-to-end book workflow tests.
9. Verify artifact paths, checksums, and manuscript integrity.

## Test ID Glossary
- TDD-001..009c: BloomOps schema and parsing
- TDD-005..008b: Layer 1 client behaviors
- TDD-010..013: Traceability
- TDD-020..025: Assumptions
- TDD-030..035: Critique and gating
- TDD-040..049e: Book workflow outputs
- TDD-050..057: Worker interface
- TDD-060..064: End-to-end smoke tests
- TDD-070..078: Orchestration engine
- TDD-080..087: Layer 3 agent
- TDD-090..097: Pipeline artifacts
