---
name: local-code-gen
description: "Template-driven code generation for LOCAL/WEAK models. Skeleton + fill blanks. Templates in reference/templates/, loaded on demand."
---

# Local Code Generation (Lite)

## Portable Mechanism: Constrained Generation

Forcing a weak generator to fill blanks in a fixed skeleton rather than generate freely is not specific to code. It applies to any context where the generator has more enthusiasm than accuracy.

**The pattern:** Provide the structure. Let the generator only fill the values. Never let the generator modify the structure. If the generator cannot determine a value, it marks TODO and moves on — it does not guess.

**Apply this to:**
- **Form filling:** user picks from options, not free text. Fewer errors.
- **Template-based content:** headline + body + CTA. Fill each, don't rewrite the layout.
- **Any low-confidence generation:** when you know the output is unreliable, constrain the output space.

**Core assumption:** This model cannot write correct code from scratch.

## Value Hierarchy

T1: Correctness — imports present, names defined, signatures correct, no syntax errors
T2: Safety — DB queries parameterized, file ops use context managers, API calls handle errors
T3: Completeness — all `___FILL___` replaced
T4: Convention — Django snake_case, Python PEP8, JS camelCase

Hard rule: Never output `___FILL___`. Never modify skeleton structure. Only fill blanks.

## Phase 0: Requirement Check

Three checks, all must pass:
0a. Framework specified? (Django / Python / JS)
0b. Component maps to exactly one template?
0c. Key identifiers provided?

If any fails → output `PHASE0_FAIL` with reason. Fail closed: better to reject than guess.

## Phase 1: Template Selection

Q1: Framework?
  Django → Q2 | Python → Q4 | JS → Q5

Q2 (Django):
  Model → django-model | View (read) → django-view | View (create/edit) → django-create-update | URL → django-url

Q3 (Python):
  Function → python-function | Class → python-class | CLI → python-cli | Data pipeline → python-data-pipeline

Q4 (JS):
  Async function → js-async-function | API call → js-api-call

Output: SELECTED_TEMPLATE: <id>

## Phase 2: Skeleton

Load the template from reference/templates/<id>.txt. Output with blanks as `___FILL___`. Do not fill yet.

If file not found, output `TEMPLATE_NOT_FOUND` and the template ID.

## Phase 3: Fill Blanks

One blank at a time. Each: read name → read constraint → derive value → replace ALL occurrences.
- Max 30 chars per blank
- If unresolvable: fill with `TODO` and note it
- No nested logic, no code expressions in blanks

## Phase 4: Self-Review

Check generated code against these patterns:
4a. Imports: all stdlib or framework standard?
4b. Null safety: every param checked before access?
4c. Resource release: every open() has matching close() in finally/with?
4d. Input validation: blank contains raw input in SQL/shell?
4e. Error handling: every try has meaningful catch?
4f. Async handling: every async called with await?

Any fail → fix blanks, re-run Phase 4. If fix requires skeleton change, note in NOTES and output with warning.

## Output Template

--- GENERATION REPORT ---
TEMPLATE: <id>
LANGUAGE: <Django | Python | JS>
PHASE0_CHECK: PASS | FAIL
SELF_REVIEW: PASS | <failed checks>
--- GENERATED CODE ---
<code, no ___FILL___ markers>
--- BLANK LOG ---
<blank> -> <value> (source: <request|default|TODO>)
--- NOTES ---
<limitations, warnings, manual steps required>

## Failure Handling

Framework not specified → PHASE0_FAIL: specify framework
No template match → PHASE0_FAIL: available templates + list
Key names missing → PHASE0_FAIL: ask user for [names]
Template file missing → TEMPLATE_NOT_FOUND
Self-review fail → return to Phase 3, note failing check
Blank unresolvable → fill TODO, note in NOTES
All blanks filled but code looks wrong → note in NOTES, do not modify skeleton
Request to write full app → PHASE0_FAIL: too large, break into components




