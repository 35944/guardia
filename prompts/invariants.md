# Invariants Analysis Prompt

> **Purpose**: Analyze a codebase to identify invariants - things that must ALWAYS be true.
> **Output**: `invariants.md`

---

## Instructions for AI Assistant

Analyze this codebase to identify invariants - things that must ALWAYS be true.

## Analysis Steps

### 1. Map the Architecture

- Identify layers (controllers, services, repositories, models)
- Trace the dependency direction
- Find the patterns that are consistent across the codebase

### 2. Document Enforced Rules

- List all pre-commit hooks and what they check
- List all CI checks and what they validate
- List all linting rules that are errors (not warnings)

### 3. Find Implicit Invariants

- How are errors handled? (Is there a standard pattern?)
- How is configuration managed? (Env vars? Config files?)
- How are dependencies injected? (Constructor? Framework?)
- How is logging done? (Structured? Levels?)

### 4. Surface Inconsistencies (IMPORTANT - these are weaknesses)

- Places where the architecture is violated
- Error handling that doesn't match the pattern
- Missing type annotations on public APIs
- Tests that are missing or skipped
- Documentation that's out of sync with code

## Output Format

Create an `invariants.md` with sections:

- **Layer Architecture** (with ASCII diagram)
- **Dependency Rules** (allowed/forbidden)
- **Error Handling** (standard pattern with example)
- **Code Size Limits** (if enforced)
- **Tech-specific invariants** (framework conventions, etc.)
- **Pre-commit enforcement** (what's already automated)

For each invariant:
- Name it
- Explain the requirement
- Show an example from the codebase

Flag inconsistencies found as **"Invariants Not Yet Enforced"** at the bottom.
