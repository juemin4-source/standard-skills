# Pipeline Skill Design Guide

A Pipeline skill coordinates external tools, files, scripts, APIs, and execution environments. It differs from Workflow in that its primary complexity is tool orchestration, not process organization.

## When to Use

- The skill must call external tools (CLI, API,本地模型, ComfyUI, Blender, Figma)
- Multiple tools must be chained (output of tool A → input of tool B)
- Environment context matters (which tools are installed, what version, what permissions)
- Examples: ComfyUI workflow runner, image generation pipeline, benchmark runner, document export pipeline

## Core Design Questions

1. What tools does the skill depend on? Are they explicitly listed?
2. What are the tool parameters? Are they validated before execution?
3. What is the environment contract? (OS, dependencies, versions, paths)
4. What is the security boundary? (what can the tool access, what is off-limits?)
5. What happens if a tool fails? (retry, fallback, stop, or degrade?)
6. Is the pipeline reproducible? (same input → same output, given same tools)
7. Does the pipeline handle partial output? (tool produced something before crashing)

## Key Mechanisms

### Tool Manifest
Explicit list of all tools, their expected versions, and how to verify they are available. Fail early if a tool is missing rather than failing midway.

### Parameter Validation
Validate tool parameters before execution. Bad parameters are the most common pipeline failure mode.

### Environment Contract
Document what the pipeline assumes about its environment: OS, installed packages, network access, file system paths, environment variables.

### Security Boundaries
Define what the pipeline can and cannot access. File system, network, credentials. Do not assume the agent has access to everything.

### Failure Handling Per Tool
- Retry with backoff for transient failures
- Fallback to alternative tool if available
- Partial output handling if the tool produced something before failing
- Clear error messages that distinguish tool failure from parameter error from environment mismatch

## Anti-Patterns

- Tools not explicitly listed (assumes they exist, fails mysteriously)
- Parameters not validated (tool fails with cryptic error)
- No environment contract (works on author's machine, fails everywhere else)
- No security boundaries (pipeline can access anything, creates risk)
- No partial output handling (tool produced 80% but crashed → entire pipeline restarts)
- Tool version not pinned (works today, breaks after update)
- Pipeline assumed to be workflow (over-engineered process for what is essentially a tool chain)
