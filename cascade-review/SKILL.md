---
name: cascade-review
description: "Deep code review using 4 parallel entry-point cascades. Data/State/Coupling/Pattern audits, each cascading until exhausted. For strong models (Claude). Probes are attention guides, not boundaries."
---

# Cascade Review

## When to Use

Use when: diff needs deep review for hidden bugs, assumptions, cross-module risks. Critical paths, shared interface changes, state management changes.

## When NOT to Use

Do not use for: style checks, formatting, trivial one-line changes, non-production code (tests, docs, configs), or when the reviewer is a weak model (use local-code-review instead).


## Portable Mechanism: Parallel Cascade Audit

This four-entry model does not depend on code review. It applies to any artifact where hidden failures matter.

**The pattern:** Launch N independent perspectives on the same target. Each perspective cascades (one finding → next question) until exhausted. Stop only when all perspectives are exhausted. Do not stop because you have enough findings — stop because you have no more questions.

**Apply this to:**
- **Architecture review:** Data (data flow between services) | State (state consistency across events) | Coupling (which services depend on which) | Pattern (known architecture anti-patterns)
- **Design critique:** Silhouette | Identity | World Logic | Production Readiness
- **PRD review:** User Need | Feasibility | Consistency | Edge Cases

The mechanism does not depend on code, diffs, or git. It depends only on the existence of a target with multiple dimensions worth examining independently.
## Core Thesis

Bugs are collisions between assumptions and runtime conditions. The safest code has the fewest unstated beliefs.

## Trust Model

Default suspicious. Style never outranks correctness.

## Entry Points

Every file gets examined through all four. Run open hunt first — which entry points fire? Then cascade each to exhaustion. Return to any entry that still has signal.

### Data Audit
Trace each value from source to use. What shape does the caller promise vs what the callee expects? Where can they diverge?
Exhausted when: every data path is traced and no unresolved assumption remains.

### State Audit
Identify every state mutation. After each error path, is state still correct? Which mutations are unrecoverable? Which error handlers continue silently?
Exhausted when: every mutation is checked for recovery and every error handler for silent continuation.

### Coupling Audit
For every touched module, who else depends on this contract? If a new constraint is introduced, which callers silently violate it?
Exhausted when: every modified modules callers are considered and no undocumented dependency remains.

### Pattern Audit
Match known failure archetypes: off-by-one, TOCTOU, empty-collection, resource-leak-on-early-return, catch-and-continue, unvalidated-offset, type-punning, shared-mutable-state-without-lock.
Exhausted when: no archetype matches remain.

## Cascade Mechanics

Each finding leads to the next question. Do not switch entry points while one still has signal. Switch only when the current cascade returns empty for three consecutive questions.

## Stop Condition

Stop only when every entry point reports exhaustion. Not when you have enough findings. Not when every file is mentioned once.

## Output

Flat list ranked by severity. Each finding: severity [P0-P3], confidence [CONFIRMED/PLAUSIBLE/SUSPICIOUS], file:line, symptom, root assumption.

If no bugs found, produce a negative finding: which entry points fired, what was examined.

## Failure Handling

Empty diff → stop. Large diff (>500 lines) → flag sampling risk. Missing context → proceed with [NO_CONTEXT] tag.




