# TDD 06: Worker Orchestration

## Coverage
- TDD-070, TDD-071, TDD-072, TDD-073, TDD-074, TDD-075, TDD-076, TDD-077, TDD-078

## Orchestration

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

ID: TDD-075  
Given a scene loop, execution order follows `scene_plan` for each chapter.

ID: TDD-076  
Given a nested loop definition, expansion produces a static DAG with no cycles.

ID: TDD-077  
Given parallel branches, the orchestrator runs them concurrently and merges outputs deterministically.

ID: TDD-078  
Given a workflow definition, validation enforces the workflow schema and required node fields.

## QA Checklist
Inputs:
- DAG with cycle, DAG with retries, nested loops, parallel branches
Steps:
1. Validate workflows.
2. Run with retries and parallel branches.
Expected:
- Cycles rejected; DAG execution obeys dependencies.
- Retries logged; merges deterministic.
- Scene order matches `scene_plan`.
