# Knowledge Skill Design Guide

A Knowledge skill provides structured domain information that other skills or agents can reference. It does not produce artifacts or find problems — it organizes and delivers expertise.

## When to Use

- The domain has stable knowledge that does not change per task (brand guidelines, design systems, coding standards, worldbuilding lore)
- Multiple skills or agents need consistent access to the same expertise
- The base model lacks specific domain knowledge that can be packaged as reference material
- Examples: design system tokens, art style guides, brand voice docs, API standards, architectural decision records

## Core Design Questions

1. What knowledge does this skill contain? What is its scope and boundary?
2. How is the knowledge structured? (flat list, hierarchy, graph, reference index)
3. How does an agent retrieve specific knowledge from it? (keyword, category, dependency walk)
4. How is the knowledge maintained? (versioned, dated, author attributed)
5. What is the context cost? (how much of this must be loaded vs referenced on demand)
6. What is the confidence level of each knowledge item? (settled fact, evolving guideline, opinion, deprecated)

## Key Mechanisms

### Knowledge Structure
Choose an organization that matches how the knowledge is used:

- Flat list: when items are independent and unordered. Good for glossaries, FAQs.
- Hierarchy: when items have parent/child relationships. Good for taxonomies, style guides.
- Reference index: when items are large and loaded on demand. Good for standards documents, specs.
- Decision tree: when the knowledge is conditional. Good for choosing between options.

### Retrieval Path
Define how an agent finds the right knowledge for a given context. Options:
- Keyword matching: agent searches by term. Simple but imprecise.
- Category routing: agent selects domain then sub-domain. More reliable.
- Dependency resolution: agent follows cross-references. Most complete but highest cost.

### Context Efficiency
Knowledge skills are especially vulnerable to context inflation. Strategies:
- Keep the SKILL.md itself short (just the retrieval method)
- Push detailed content to reference files loaded on demand
- Use progressive disclosure: surface the index first, load details only when needed
- Mark knowledge items by priority: MUST-know vs SHOULD-know vs NICE-to-know

### Maintenance Metadata
Each knowledge item should include:
- Date added or last reviewed
- Author or source
- Confidence (settled / evolving / deprecated)
- Dependencies (what other knowledge it references)

## Anti-Patterns

- SKILL.md is a giant encyclopedia (context cost explodes)
- No retrieval path (agent must read everything to find what it needs)
- No maintenance metadata (knowledge goes stale silently)
- Knowledge and procedure mixed in the same file (cannot update one without touching the other)
- Boundaries not stated (agent applies knowledge outside its valid domain)
- Knowledge treated as settled when it is evolving
