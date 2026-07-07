# Research Skill Design Guide

A Research skill explores an unfamiliar domain and produces structured understanding. It differs from Diagnostic (which finds problems) and Knowledge (which contains expertise) — it generates understanding where none existed before.

## When to Use

- The agent needs to understand a new domain before acting on it
- The task requires gathering, comparing, and synthesizing information from multiple sources
- The output is an understanding or insight, not a fixed artifact
- Examples: skill ecosystem survey, design trend analysis, competitor research, technology landscape mapping

## Core Design Questions

1. What is the research question? What are we trying to understand?
2. What are the information sources? (existing skills, documentation, expert interviews, benchmarks)
3. How many samples are enough? (stopping condition for data gathering)
4. How is raw information structured into understanding? (categorization, pattern extraction, hypothesis formation)
5. What is the output? (report, map, framework, recommendation, uncertainty assessment)
6. How is uncertainty communicated? (what is known, what is likely, what is unknown, what is assumed)

## Key Mechanisms

### Research Question Definition
A good research skill starts by making the question explicit. Without a clear question, information gathering has no stopping condition.

### Source Selection
Define what counts as a valid source and how to prioritize:
- Primary vs secondary sources
- Authoritative vs community sources
- Recent vs historical sources
- First-hand vs derived sources

### Sample Sufficiency
Define a stopping condition for data gathering:
- Minimum sample count (e.g., study at least 5 examples)
- Saturation (last N samples yielded no new patterns)
- Coverage (all known categories are represented)
- Timebox (gather for N minutes, then synthesize)

### Pattern Extraction
Define how raw observations become structured findings:
- What counts as a pattern? (repeated observation across independent sources)
- How to distinguish signal from noise?
- What to do with outliers? (flag but do not discard)

### Uncertainty Communication
Research findings always have uncertainty. The skill should communicate:
- What is well-supported by evidence
- What is suggestive but not confirmed
- What is assumed (and why)
- What was not investigated (and why not)
- What would need to change to increase confidence

## Anti-Patterns

- No research question (gathering without purpose)
- No stopping condition (gathers forever or stops arbitrarily)
- Source bias (only reads sources that confirm prior beliefs)
- Certainty inflation (presents suggestive findings as definitive)
- Pattern hallucination (sees patterns where none exist)
- No uncertainty communication (reader cannot tell what is reliable)
- Research and diagnosis confused (tries to fix problems before understanding them)
- Output too long (research findings are raw notes, not structured understanding)
