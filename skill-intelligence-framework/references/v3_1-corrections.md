# Skill Intelligence Framework v3.1 Corrections

Based on 2026-07-07 benchmark experiments.

## Methodology Tax

Every layer of structure in a skill imposes an attention tax on the model. If the base model is already strong in the domain, this tax may exceed the structural benefit.

Skill structure is not free. Each step, probe, format rule, and output template consumes context and attention that could be used for task execution.

For domains where the base model has strong native ability (code review, common writing, standard UI), prefer thin skills that adjust stance rather than teach procedure.

## Stance Skill (New Type)

A Stance Skill does not teach knowledge or procedure. It changes the model attitude, suspicion level, exploration tendency, and interaction posture.

Characteristics: minimal structure, strong tone, core thesis, no complex output format. Effectiveness depends on base model quality.

Example: grilling is a Stance Skill, not a Diagnostic Skill.

## Skill Thickness Fit

Thin Skill (minimal structure, high stance): base model strong, task needs recall, format kills discovery.
Thick Skill (structured, multi-phase): base model weak, task needs embedded knowledge, stable output required.

## Hunter vs Consolidator Separation

Hunter: maximum recall, minimal structure, stance-heavy, candidate list output.
Consolidator: maximum precision, moderate structure, criteria-heavy, structured report.

A benchmark measuring recall should use a Hunter. Production review should chain Hunter -> Consolidator.

## Base Model Prior Assessment

Code review: strong prior -> thin skill. UI design: moderate -> medium. High-art critique: weak -> thick judgment model. Domain tools: weak -> thick reference. Writing: strong -> thin stance.

## Stance Skill Mechanism (expanded)

A Stance Skill does not add information. It changes five things:

1. Default position: do not trust the surface
2. Search mode: cast wide before categorizing
3. Judgment intensity: flag suspicious findings rather than suppress them for politeness
4. Objective function: find real risk, not produce pretty output
5. Output attitude: direct, specific, evidence-grounded

It works because strong base models already possess domain knowledge. They are constrained by: politeness, conservatism, fear of false positives, premature summarization, template-following, and user-pleasing defaults.

A Stance Skill removes these constraints. It does not teach; it activates.

## The "Less Is More" Principle

Top-level skill design knows when NOT to add structure.

Many skill authors write everything they know. But expert skill authors know:
- What to write in (compressed judgment)
- What would crush the model (excessive procedure)
- What should be stance (attitude adjustment)
- What should be reference (loadable on demand)
- What should be left to the model (native ability space)

Skill is "you" (explicit). It must leave room for "wu" (implicit native ability). A good skill does not fill the entire context — it leaves space for the model to bring its own competence.

## Applying to High-Art Domains

Not all high-art tasks need thick skills.

Tasks where base model is moderately capable (stance skill sufficient):
- Visual description and analysis
- Style critique
- Design suggestion
- Prompt writing
- Creative ideation

Tasks where base model is weak (thick skill needed):
- Character turnaround modeling readiness
- Costume structural breakdown
- ComfyUI workflow pipeline
- Topology logic
- Game asset production standards
- UE material/shader details

Judge per task type, not per domain label.
