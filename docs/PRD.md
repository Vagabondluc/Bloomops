# BloomOps PRD

## Summary
BloomOps is a three-layer system that turns human intent into executable, testable outputs. Layer 1 captures intent via Bloom taxonomy scaffolds and user story documents. Layer 2 interprets those documents to generate a PRD, specs, and TDD, plus automated critiques and smoke tests. Layer 3 is a CLI-run AI agent with access to "worker" scripts (Python/CLI) to execute tasks using the artifacts from Layer 2. The system is designed to maximize time between user interventions while keeping intent traceable and auditable.

## Goals
- Provide a Bloom taxonomy wheel scaffold for interpreting user intent.
- Support dual documentation: Markdown (source of truth) and JSON/YAML (machine-parsed).
- Map real authoring workflows to BloomOps (v0.1 uses a full book-writing workflow from `book/Jason's Prompts.md`).
- Generate PRD, specs, and TDD from BloomOps docs with traceability.
- Run automated critiques and smoke tests against generated TDD and outputs.
- Provide a CLI agent layer that orchestrates workers and LLM calls in a predictable, logged way.

## Non-Goals (v0.1 defaults; confirm)
- No autonomous intent changes; BloomOps docs are read-only for execution.
- No real-time UI; CLI only.
- No continuous background agents; runs are explicit.
- No code execution outside the workspace by default.

## Users
- Primary: Solo creators and small teams who build structured content (books, TTRPG campaigns, design docs).
- Secondary: Prompt engineers and tool builders who want a spec-first AI pipeline.

## Key Workflows
1. Author writes BloomOps Markdown docs with intent and constraints.
2. System generates JSON/YAML representation from Markdown.
3. Layer 2 generates PRD, specs, and TDD, with assumption logs when needed.
4. Layer 2 runs critique prompts and smoke tests to verify artifacts.
5. Layer 3 agent uses workers to execute tasks and generate outputs (book drafts, docs).
6. User passes PRD/specs/TDD to BMAD and open-code workflows.

## Requirements
- BloomOps Markdown is authoritative; JSON/YAML is derived.
- `doctrine_frozen` in JSON/YAML must be set to true before Layer 2 generation.
- `run_snapshot.source_hash` must match the current BloomOps Markdown before Layer 2 generation.
- Each generated artifact traces back to BloomOps section IDs.
- Ambiguity behavior: proceed with assumption logs and user notification.
- Jason book prompts must be mapped to BloomOps stages and used to construct a full book workflow.
- Worker interface must be explicit: inputs, outputs, and logs.
- Workers must support an n8n-like orchestration layer (node-based workflows, step dependencies, retries).
- Book workflow must support per-chapter loops with multi-pass editing (critique, edit, copyproof, tighten).
- Layer 1 includes an AI LLM client UI to guide BloomOps outline and scene iteration with the user.
- All automation steps are logged with timestamps, inputs, and output summaries.

## Success Metrics
- A complete book workflow can run end-to-end using the Layer 1 prompts.
- All PRD/spec/TDD items have traceability to BloomOps IDs.
- TDD includes smoke tests that can be executed by workers.
- Assumption logs are generated when ambiguity exists and are visible to the user.

## Risks
- Misinterpretation drift from BloomOps to PRD/specs.
- Self-confirming critique loops if the same model validates its own output.
- Overhead of maintaining Markdown + JSON/YAML sync.

## Open Questions
- Confirm v0.1 non-goals.
- Confirm minimum Bloom verb set for v0.1.
- Identify which worker scripts already exist.
