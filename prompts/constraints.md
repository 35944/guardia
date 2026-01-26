# Constraints Analysis Prompt

> **Purpose**: Analyze a codebase to identify constraints - things that should NEVER happen.
> **Output**: `constraints.md`

---

## Instructions for AI Assistant

Analyze this codebase to identify constraints - things that should NEVER happen.

## Analysis Steps

### 1. Mine Past Incidents

- Search git history for "fix", "bug", "revert", "hotfix"
- Look at recent commits that fix issues
- Ask: "What went wrong that we never want to repeat?"

### 2. Analyze Code Review Patterns

- Look at any linting rules (.eslintrc, .pylintrc, ruff.toml)
- Check pre-commit hooks for what's blocked
- Search for "TODO", "FIXME", "HACK", "XXX" comments

### 3. Find Implicit Constraints

- Patterns that exist everywhere (these are likely required)
- Anti-patterns that are avoided everywhere
- Error handling patterns that are consistent

### 4. Surface Violations (IMPORTANT - these are weaknesses)

- Code that breaks the apparent patterns
- Inconsistent error handling
- Direct dependencies that should go through abstractions
- Security anti-patterns (hardcoded secrets, SQL concatenation, etc.)
- Files that are too large or too complex

## Output Format

Create a `constraints.md` with categories:

- **Architecture Constraints** (what structures are forbidden)
- **Code Quality Constraints** (what patterns are banned)
- **Data Constraints** (what data handling is prohibited)
- **Security Constraints** (what security practices are required)
- **Process Constraints** (what workflows are mandatory)

For each constraint:
- Name it
- Explain why it matters
- Show FORBIDDEN and ALLOWED examples from the actual codebase

Flag violations found as **"Current Violations to Fix"** at the bottom.
