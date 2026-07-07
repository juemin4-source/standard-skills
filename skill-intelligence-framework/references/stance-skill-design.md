# Stance Skill Design Guide

A stance skill does not teach knowledge or procedure. It adjusts the model's posture.

## When to Use

- Base model has strong domain prior
- The task requires attitude shift (more suspicious, more creative, more critical)
- Thick methodology would impose tax that reduces native ability

## Core Design Questions

1. What is the default stance the model enters without this skill?
2. What stance do we want instead?
3. What single sentence best compresses this stance shift?
4. How little structure can we get away with?

## Key Mechanisms

### Core Thesis
The first sentence is the most important element. It anchors the model's attention and default position.

Weak: "Review this code carefully."
Strong: "Bugs are collisions between assumptions and runtime conditions."

### Trust Model
Set explicitly. Default trusting for generation. Default suspicious for review.

### Minimal Structure
Stance skills should be short. 20-60 lines. No complex output formats. No multi-step procedures unless essential. Every line beyond the core thesis should be tested for methodology tax.

### Output Lightness
Minimal output format. The output is a byproduct of the stance, not the goal.

## Anti-Patterns

- Adding procedure to a stance skill (methodology tax)
- Stance and procedure mixed without separation
- Core thesis missing or generic
- Trust model not stated
- Format heavier than the stance itself
