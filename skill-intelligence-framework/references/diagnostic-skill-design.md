# Diagnostic Skill Design Guide

A diagnostic skill discovers hidden problems in a target.

## Core Design Questions

1. What search operator(s) will expand the search space?
2. What lens(es) define the abstract perspectives?
3. What consolidation mechanism filters candidates?
4. What is the stop condition? (exhaustion, not completion)
5. What is the trust model?

## Three Mechanisms (from v3.1 experiments)

### Expansion Operator
Opens search space and generates candidates. Choose based on domain prior and omission cost.

Operators: Open Hunt, Question Cascade, Parallel Audit, Dependency Walk, Adversarial Challenge, Residual Sweep.

### Lens Set
Abstract perspectives that determine which problem families are visible.

When a problem category has near-zero recall, diagnose as Lens Failure. Add the missing lens; do not patch specific cases.

### Consolidation Operator
Filters, validates, and ranks candidates.

Standard gate: Candidate → Evidence → Failure Path → Impact → Status (Confirmed/Suspicious/Drop)

## Failure Diagnosis

- Search Failure: low findings, low recall → improve expansion
- Lens Failure: category at zero recall → add lens
- Consolidation Failure: high findings, low precision → add evidence gate
- Delivery Suppression: strong structure, low recall → separate hunter/consolidator

## Anti-Patterns

- Probe closure (probes as exhaustive boundaries)
- Stop by completion, not exhaustion
- Using one mechanism for both expansion and consolidation
- Format during discovery phase
