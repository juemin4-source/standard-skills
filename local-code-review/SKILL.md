---
name: local-code-review
description: "Pattern-based code review for LOCAL/WEAK models. Walks full decision tree, records all matches, then reports. Each finding requires exact line + code evidence."
---

# Local Code Review (Lite)

## Value Hierarchy

[P0] Data corruption / data loss
[P1] Crash / security hole / contract violation
[P2] Edge case / degraded output
[P3] Style / naming — only if P0-P2 are clean

Hard rule: no P3 if any P0-P2 exists. No finding without exact line evidence.

## Step 0: Preflight

diff non-empty, file is source, language known. Any fail → NO_DIFF / SKIPPED / UNKNOWN_LANGUAGE. Stop.

## Decision Tree

IMPORTANT: "Step 1" / "Step 2" below are DECISION TREE step numbers, not code line numbers.
When recording a finding, the Code Line field must contain the line number from the DIFF FILE, not 1, 2, 3, 4, or 5.

Walk ALL 5 steps. For each match: record the finding (pattern ID, line, evidence). After ALL steps done, output all recorded findings. Do NOT stop at first match.

Each finding requires: exact line number + exact code quote (2-5 lines). Without these → mark UNCERTAIN.

### Step 1: Security
1a. Input → SQL/shell/eval/file/HTML? → PAT-004 (INP). Record if evidence exists.
1b. Literal matches key/secret/token pattern? → PAT-011 (SEC). Record if evidence exists.
→ Continue to Step 2.

### Step 2: Memory / Resource
2a. Resource opened without matching close in finally/using? → PAT-003 (RSL). Record.
→ Continue to Step 3.

### Step 3: Data Flow
3a. Variable accessed as object without null guard? → PAT-002 (NLL). Record.
3b. Global var mutated in async context without lock? → PAT-007 (SMT). Record.
3c. Arithmetic on bounded type without range check? → PAT-009 (INT). Record.
→ Continue to Step 4.

### Step 4: Logic
4a. `<=` on zero-indexed array length? → PAT-001 (OBO). Record.
4b. `==` between types or `===` on floats? → PAT-005 (TYP) or PAT-008 (CMP). Record.
4c. `!` on compound breaking De Morgan? → PAT-010 (LOG). Record.
→ Continue to Step 5.

### Step 5: Async / Error
5a. Empty catch or silent error? → PAT-006 (ERR). Record.
5b. async without await or .catch? → PAT-012 (ASY). Record.
→ All steps done. Output all recorded findings.

If no findings recorded across all 5 steps → output NO_BUGS and list which steps were walked.

## Pattern Reference (load on demand)

| ID | Trigger | Flag Condition |
|----|---------|----------------|
| PAT-001 | `<=` on length, `i-1` without guard | Loop on zero-indexed array |
| PAT-002 | Property access without null check | No guard clause preceding |
| PAT-003 | open/create/lock without close/destroy | No finally/defer block |
| PAT-004 | External data → SQL/shell/eval/path | Visible data flow |
| PAT-005 | `==` between different types | Types differ |
| PAT-006 | Empty catch, ignored error return | Error path has no effect |
| PAT-007 | Global var mutated in async | No mutex/atomic |
| PAT-008 | Float `===`, NaN compare, object identity | Wrong comparison method |
| PAT-009 | Arithmetic on bounded type without guard | Value from external or unbounded |
| PAT-010 | Wrong `&&`/`||`, De Morgan violation | Compound condition with `!` |
| PAT-011 | Literal matching key/secret/token | High-entropy >20 chars |
| PAT-012 | async without await, promise without .catch | In async context |

Per-pattern detail: reference/patterns/pat-XXX.txt (load only matched ones).

## Output Template

--- REVIEW REPORT ---
FILE: <path>
LANGUAGE: <lang>
SEVERITY: P0 | P1 | P2 | P3 | NO_BUGS (use highest severity across all findings)
FINDING_COUNT: <N>

FINDING_1:
  Pattern: <PAT-XXX>
  Code Line: <line number from the diff, NOT from the decision tree>
  Evidence: <exact code, 2-5 lines>
  Confidence: CONFIRMED | UNCERTAIN

FINDING_2: ...
UNCERTAIN: ...
NOTES: ...
STEPS_WALKED: Step 1,2,3,4,5

## Failure Handling

Empty diff → NO_DIFF. Unknown lang → UNKNOWN_LANGUAGE.
No findings → NO_BUGS + list steps walked.
No exact line evidence → UNCERTAIN, not CONFIRMED.
Diff >300 lines → Steps 1-2 on all files, Steps 3-5 on first 200 lines.
No context → note "no spec provided."

## Anti-Patterns

1. Hallucination: need exact code Evidence. Without it → UNCERTAIN.
2. False confidence: CONFIRMED only when code EXACTLY matches trigger.
3. Style over substance: check Value Hierarchy before P3.
4. No new patterns outside PAT-001~012.
5. PAT-004 requires VISIBLE data flow in diff.



