# TDD 03: Layer 3 Agent

## Coverage
- TDD-080, TDD-081, TDD-082, TDD-083, TDD-084, TDD-085, TDD-086, TDD-087

## Agent Behavior

ID: TDD-080  
Given PRD/specs/TDD inputs, the agent produces a task plan with trace IDs.

ID: TDD-081  
Given worker execution, the agent logs each step with inputs, outputs, and status.

ID: TDD-082  
Given a smoke test failure, the agent reports the last successful artifact.

ID: TDD-083  
Given a worker uses an LLM, the agent records provider and model in the run log.

ID: TDD-084  
Given a request to modify BloomOps Markdown, the agent refuses without user approval.

ID: TDD-085  
Given a run with `doctrine_frozen: false`, the agent halts before Layer 2 generation.

ID: TDD-086  
Given a retry policy, the agent honors it and logs each attempt.

ID: TDD-087  
Given a worker failure, the agent records a failure summary and exits non-zero.

## QA Checklist
Inputs:
- PRD/specs/TDD with trace IDs
- Worker failure scenario
Steps:
1. Generate task plan and execute workers.
2. Trigger a worker failure.
Expected:
- Plan includes trace IDs.
- Logs include provider/model and outputs.
- Failure summary emitted; non-zero exit.
