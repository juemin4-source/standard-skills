# Delivery Skill Design Guide

A delivery skill's job is to produce a stable, usable artifact from an input.

## Core Design Questions

1. What is the input? Is it validated before processing?
2. What is the output format? Is it templated or free-form?
3. What is the truth source during iteration? (SSOT pattern)
4. Does it support multi-round editing? How?
5. What happens with bad input? (fail fast, degrade, or fix?)

## Key Mechanisms

### Input Contract
Define what valid input looks like. Reject or flag input that does not meet minimum quality. Empty/incomplete input should not produce plausible-looking garbage output.

### Output Template
Most delivery skills benefit from a defined output structure. Template-driven gives stability. Rule-driven gives flexibility. Hybrid gives both.

### Single Source of Truth (SSOT)
For multi-round editing, define what the canonical artifact is. Baoyu pattern: prompt files are SSOT, generated output is derived. Never edit derived artifacts directly.

### Iteration Support
- Selective regeneration: ability to redo one part without touching others
- Backup conventions: timestamp or numbered backups before changes
- Comparison: ability to compare before/after across iterations

### Failure Handling
- Bad input: reject with clear reason, not silent garbage output
- Tool failure: fallback path if external tool unavailable
- Partial failure: state what succeeded and what did not

## Anti-Patterns

- No input validation (most common failure)
- SSOT not defined (user edits output, next iteration confused)
- Iteration without comparison (no way to tell if change helped)
- Format over content (template produces valid structure but empty substance)
- Single monolithic generation without selective edit (every change = full regenerate)
