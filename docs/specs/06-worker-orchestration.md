# Spec 06: Worker Orchestration (n8n-like)

## Purpose
Define the worker workflow engine that mirrors n8n-style automation: node-based steps, explicit dependencies, and repeatable runs.

## Core Concepts
- Node: a single worker execution unit.
- Workflow: directed acyclic graph (DAG) of nodes.
- Run: a specific execution instance with inputs, outputs, and logs.
- Chapter loop: a template that expands into per-chapter DAG segments (no cycles in the final DAG).
- Scene loop: a template that expands into per-scene DAG segments within each chapter.

## Node Definition
Each node must declare:
- `node_id`
- `worker_name`
- `inputs` (resolved from constants or prior node outputs)
- `outputs` (keys produced by the worker)
- `retries` (count, backoff strategy)
- `timeout_ms`

## Workflow Definition
A workflow includes:
- list of nodes
- dependency edges
- entry nodes
- run metadata (trace IDs, user, timestamp)
- optional loop definition that expands into per-chapter nodes
- optional nested loop definition that expands into per-scene nodes

## Workflow Schema (YAML Example)
```yaml
workflow_id: "book-v0.1"
run:
  user: "author"
  trace_ids: ["US-001"]
nodes:
  - node_id: "callsheet"
    worker_name: "generate-callsheet"
    inputs:
      braindump: "{{inputs.braindump}}"
      genre_tropes: "{{inputs.genre_tropes}}"
    outputs: ["callsheet_path"]
edges:
  - from: "callsheet"
    to: "characters"
loops:
  chapters:
    source: "outline.chapters"
    scene_loop:
      source: "bloomops.scene_plan"
```

## Execution Rules
- Validate the DAG before execution (no cycles).
- A node runs only when all dependencies succeed.
- Failed nodes can be retried per policy.
- Partial runs must persist outputs for resumption.
- All node outputs are stored in a run artifact directory.
- Loop expansion must materialize a static DAG using the outline chapter list.
- Nested loop expansion must materialize per-scene DAG segments from the derived scene list.
- Scene ordering must follow `scene_plan` order for each chapter.

## Logging
Each node run records:
- status: success/failure
- inputs resolved
- output paths
- timings
- retry attempts
