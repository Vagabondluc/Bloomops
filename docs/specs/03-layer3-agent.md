# Spec 03: Layer 3 CLI Agent

## Purpose
Define the CLI-run agent that orchestrates workers and LLM calls to execute tasks from PRD/specs/TDD.

## Capabilities
- Read PRD/specs/TDD and plan tasks.
- Run worker scripts via CLI.
- Call LLMs via workers.
- Emit logs and artifacts.

## Restrictions
- No direct edits to BloomOps Markdown.
- No network access unless explicitly allowed by user.
- No implicit requirement changes.

## Execution Flow
1. Load PRD/specs/TDD.
2. Build a task plan with references to trace IDs.
3. Run workers step-by-step.
4. Run smoke tests.
5. Summarize results and unresolved issues.

## Logging
Each run must emit:
- timestamp
- inputs used
- command executed
- outputs generated
- pass/fail for smoke tests

## LLM Provider
- Workers may use Ollama as the LLM provider.
