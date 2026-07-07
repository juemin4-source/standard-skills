---
name: skill-intelligence-framework
description: "Root skill. Routes any Skill design or evaluation task to the correct archetype guide. Does not contain design logic itself."
---

# Skill Intelligence Framework

## Core Principle

A skill should not be judged by what domain it targets, but by what capability it provides to the agent.

Do not classify skills by topic (code, art, writing). Classify by what they change in the agent's behavior.

## Archetype Router

Before designing or evaluating a skill, determine its primary archetype.

Ask five questions:
1. What does this skill ultimately produce? (a list, an artifact, a decision, a state, a process, a tool call, knowledge, or understanding)
2. What capability does it primarily change in the agent? (seeing, making, being, judging, doing, connecting, knowing, learning)
3. What is its success metric? (recall, stability, activation, correctness, reliability, fidelity, clarity, insight)
4. What failure mode would be most damaging? (miss, format error, no effect, wrong decision, broken step, tool crash, stale info, shallow understanding)
5. How strong is the base model in this domain? (determines thickness)

Then route to the appropriate design guide.

## Archetype Reference

| Archetype | The skill makes the agent... | Success metric | Failure mode |
|---|---|---|---|
| Diagnostic | ...see problems | Recall, precision | Missed issues |
| Delivery | ...produce artifacts | Stability, usability | Bad output |
| Stance | ...maintain posture | Activation, stance shift | No effect |
| Director | ...make tradeoffs | Judgment correctness | Wrong call |
| Workflow | ...organize steps | Reliability, reproducibility | Broken process |
| Pipeline | ...call tools | Correct invocation, safety | Tool crash |
| Knowledge | ...use domain info | Retrieval accuracy, fidelity | Stale/wrong info |
| Research | ...understand new domains | Insight, pattern quality | Shallow understanding |

## Multi-archetype Skills

A skill may combine archetypes. Record primary and secondary explicitly.

Example: cascade-review = Diagnostic (primary) + Stance (secondary) + Delivery (tertiary)

## Usage

To design a skill: Route → Read guide → Apply principles → Draft → Verify
To evaluate a skill: Route → Read guide → Score → Diagnose → Recommend

See references/archetype-router.md for the routing decision tree.
See references/*-design.md for per-archetype design guides.
