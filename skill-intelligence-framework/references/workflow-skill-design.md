# Workflow Skill Design Guide

A Workflow skill organizes multi-step processes. Its value is in reliability, reproducibility, and user confidence through the process.

## When to Use

- The task has multiple stages with dependencies between them
- State must be tracked across stages
- Failure at one stage should not lose work from earlier stages
- Examples: data processing pipelines, multi-stage generation, review cycles, content production

## Core Design Questions

1. What are the stages? Can they be named and ordered?
2. What are the dependencies between stages? Can stage 3 start before stage 2 finishes?
3. What state persists across stages? How is it stored and passed?
4. What happens if a stage fails? Can it be retried? Does the user need to restart?
5. What are the entry conditions? (what must be true before stage 1)
6. What are the exit criteria? (how do we know the workflow is done?)
7. Does it support partial re-run? (stage 3 failed, redo only stage 3)

## Key Mechanisms

### Stage Definition
Each stage has: name, input, output, entry condition, exit condition, failure handling.

### State Management
Explicitly define what data flows between stages. A shared file, a state object, or accumulated context.

### Failure Handling Per Stage
Define per-stage rather than one global handler:
- Retry: can this stage be re-run safely?
- Skip: can this stage be skipped without breaking downstream?
- Rollback: does a failure undo earlier stages?
- Notify: does the user need to know?

### Partial Re-run
Support re-running a specific stage without restarting the entire workflow. This is the most common user need after a failure.

## Anti-Patterns

- Stages defined but dependencies not specified (user doesn't know if they can skip steps)
- No failure handling per stage (one failure kills everything with no recovery path)
- State not persisted between stages (if interrupted, everything is lost)
- Entry conditions not stated (user starts the workflow with insufficient context)
- No partial re-run (every fix requires full restart)
- Workflow mistaken for expertise (process looks complete but has no judgment at any stage)
