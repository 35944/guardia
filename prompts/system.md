# System (AI Agent Operating System) Prompt

> **Purpose**: Design an AI Agent Operating System that defines how agents work together on this codebase.
> **Output**: `system.md`

---

## Instructions for AI Assistant

Design an AI Agent Operating System for this codebase.

## Analysis Steps

### 1. Map Existing Workflows

- How do features currently get built? (tickets → code → review → merge)
- What gates exist? (code review, CI, staging, etc.)
- What approvals are required?

### 2. Identify Trust Boundaries

- What can be automated safely? (formatting, linting)
- What needs human review? (logic, security)
- What needs explicit approval? (schema changes, deployments)

### 3. Assess Parallelization Potential

- Can multiple features be worked on simultaneously?
- What creates conflicts? (shared files, schema changes)
- How is work currently coordinated?

### 4. Surface Bottlenecks (IMPORTANT - these are weaknesses)

- Where do things get stuck waiting?
- What manual steps could be automated?
- What causes merge conflicts frequently?
- What lacks clear ownership?

## Output Format

Create a `system.md` with:

- **System overview diagram**
- **Foundational documents list**
- **Agent types** (what each does, constraints)
- **Parallel coordination** (branches, isolation)
- **State machine** (lifecycle of a change)
- **Trust boundaries** (high/medium/low trust items)
- **Error recovery procedures**

Flag bottlenecks as **"Process Improvements to Consider"** at the bottom.
