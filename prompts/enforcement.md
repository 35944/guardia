# Enforcement System Prompt

> **Purpose**: Design the enforcement system that automatically validates constraints and invariants.
> **Output**: `enforcement.md`

---

## Instructions for AI Assistant

Design the enforcement system for this codebase.

## Analysis Steps

### 1. Inventory Existing Enforcement

- Pre-commit hooks (list each, what it checks)
- CI checks (list each, what it validates)
- Linting rules (errors vs warnings)
- Type checking (strict vs lenient)

### 2. Map Enforcement Layers

- What's caught at edit time? (IDE)
- What's caught at commit time? (pre-commit)
- What's caught at push/PR time? (CI)
- What's caught at merge time? (required checks)

### 3. Identify Enforcement Gaps

- Constraints that aren't enforced
- Invariants that aren't checked
- Rules that are warnings but should be errors
- Checks that are slow and get skipped

### 4. Surface What Slips Through (IMPORTANT - these are weaknesses)

- What violations make it to production?
- What gets caught only in code review?
- What requires manual verification?
- What's documented but not automated?

## Output Format

Create an `enforcement.md` with:

- **Enforcement layers diagram**
- **Layer 0: Design time** (before code)
- **Layer 1: Edit time** (during code)
- **Layer 2: Commit time** (pre-commit)
- **Layer 3: Phase time** (during execution)
- **Layer 4: Merge time** (CI/review)
- **Override protocol**
- **Violation cost summary**

Include actual commands and config snippets from this codebase.

Flag gaps as **"Enforcement to Add"** at the bottom.
