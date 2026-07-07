# Director Skill Design Guide

A Director skill applies high-level judgment, taste, strategy, and tradeoffs. It does not primarily produce artifacts or find problems — it decides what matters.

## When to Use

- The task requires value judgment, not just detection or generation
- Someone needs to decide what to keep, what to cut, what direction to take
- The base model tends to be overly accommodating or lacks a point of view
- Examples: art direction, product strategy, portfolio review, design critique

## Core Design Questions

1. What is the core thesis? What one belief anchors all judgments?
2. What value hierarchy does it enforce? (what matters > what matters less > what doesn't matter)
3. What does it reject? (false goals, pseudo-criteria, common mistakes)
4. How does it handle tradeoffs? (when X and Y conflict, which wins?)
5. What is its taste position? (does it have one, or is it neutral?)
6. Does it know its boundaries? (what it is NOT qualified to judge)

## Key Mechanisms

### Core Thesis
A single sentence that compresses the skill's worldview. This is the most important element. Everything else derives from it.

Weak: "Help improve the quality of character designs."
Strong: "A good character design is recognizable at 80px, has a clear identity silhouette, and can be modeled without guessing hidden structures."

### Value Hierarchy
Explicitly rank what matters. Without this, the skill will treat everything as equally important.

Example: "structural integrity > identity clarity > material logic > polish > ornament > style preference"

### False-Goal Rejection
State what the skill should NOT optimize for. This is as important as stating what it should optimize for.

Example: "Do not optimize for visual polish at the expense of structural clarity. Do not mistake detail density for quality. Do not reward ornament that obscures function."

### Tradeoff Rules
When two good things conflict, which wins? Give concrete rules.

Example: "If beauty conflicts with identity, preserve identity. If detail conflicts with readability, reduce detail. If novelty conflicts with consistency, prefer consistency unless the brief explicitly asks for novelty."

## Anti-Patterns

- No core thesis (generic excellence language instead)
- No value hierarchy (everything is "important")
- No false-goal rejection (optimizes for wrong things)
- Afraid to take a position (tries to please everyone)
- Confuses taste with rules (has opinions but no criteria)
- No boundary awareness (judges things outside its expertise)
