# Process (Development Workflow) Prompt

> **Purpose**: Define the development process for AI agents working on this codebase.
> **Output**: `process.md`

---

## Instructions for AI Assistant

Define the development process for AI agents working on this codebase.

## Analysis Steps

### 1. Document Current Process

- How does work start? (ticket, idea, bug report)
- What planning happens before coding?
- How is code reviewed?
- What checks run before merge?

### 2. Identify Existing Gates

- What blocks a commit? (pre-commit hooks)
- What blocks a merge? (CI, reviews)
- What blocks a deployment? (approvals, checks)

### 3. Map the Commands

- How to run tests?
- How to run linting?
- How to run the build?
- How to run locally?

### 4. Surface Process Gaps (IMPORTANT - these are weaknesses)

- Work that starts without clear requirements
- Code that gets merged without adequate review
- Tests that are skipped or ignored
- Documentation that's not updated
- Changes that break things discovered late

## Output Format

Create a `process.md` with 5 phases:

### 1. Research
- Inputs
- Process
- Outputs
- Gate

### 2. Planning
- Inputs
- Process
- Outputs
- Gate

### 3. Review
- Inputs
- Process
- Outputs
- Gate

### 4. Execution
- Inputs
- Process
- Outputs
- Gate

### 5. Merge
- Inputs
- Process
- Outputs
- Gate

Include:
- Specific commands for this codebase
- Gate criteria
- Anti-patterns to avoid

Flag gaps as **"Process Gaps to Address"** at the bottom.
