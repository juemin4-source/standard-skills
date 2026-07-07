# Verification Skill Design Guide

A Verification skill tests whether something is correct. It is not Diagnostic (which finds problems) — it checks specific claims against evidence.

## When to Use

- Benchmark results need to be judged against golden data
- A generated artifact needs to be checked for correctness
- A claim needs to be supported or refuted by evidence
- A skill's output needs to be measured against a standard
- Examples: benchmark judge, golden comment matching, output validation, acceptance testing

## Core Design Questions

1. What is the object of verification? (a skill output, a generated artifact, a claim, a behavior)
2. What is the standard being verified against? (golden data, spec, contract, expected behavior)
3. What counts as a match? (exact, semantic, partial, probabilistic)
4. How is disagreement resolved? (tiebreaker, confidence threshold, human review)
5. Is the verification reproducible? (same input + same golden → same result)
6. What are the verification metrics? (recall, precision, F1, accuracy, pass/fail)

## Key Mechanisms

### Golden Data
The reference standard must be explicit, versioned, and representative. A verification skill is only as good as its golden data.

### Matching Criteria
Define what constitutes a match. Different tasks need different strictness:
- Exact match: string or structural identity
- Semantic match: same meaning, different wording
- Partial match: overlapping but not identical
- Probabilistic match: confidence score with threshold

### Judge Design
The judge (the entity that compares output against golden) must be:
- Consistent: same input → same judgment
- Calibrated: knows when to be strict vs lenient
- Transparent: can explain why something matched or did not
- Aware of its own bias: knows what it tends to miss or over-count

### Metric Calculation
Define metrics before running the verification, not after. Standard set:
- True Positive, False Positive, True Negative, False Negative
- Recall = TP / (TP + FN)
- Precision = TP / (TP + FP)
- F1 = 2 * (Precision * Recall) / (Precision + Recall)
- Accuracy = (TP + TN) / Total

### Error Analysis
After verification, classify errors:
- False positives: what did the skill find that wasn't there?
- False negatives: what did the skill miss?
- Are errors clustered in specific problem categories?
- Are errors due to skill mechanism, golden quality, or judge bias?

## Anti-Patterns

- Golden data not versioned (cannot reproduce results)
- Matching criteria not defined (judge makes arbitrary calls)
- Judge not calibrated (too strict → low recall; too lenient → low precision)
- Metrics computed before all data is labeled (cherry-picked results)
- Error analysis not done (knows the score, doesn't know what went wrong)
- Verification mistaken for diagnosis (knows something failed, doesn't know why)
- Single run treated as definitive (no confidence interval, no error bars)
