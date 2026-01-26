# Learning Loop Prompt

> **Purpose**: Design the learning loop for continuous improvement based on violations and incidents.
> **Output**: `learning-loop.md` and `violations-log.md` (template)

---

## Instructions for AI Assistant

Design the learning loop for continuous improvement.

## Analysis Steps

### 1. Find Past Learnings

- Post-mortems or incident reports
- "Lessons learned" in documentation
- Rules that were added after problems
- Tests that were added after bugs

### 2. Identify Recurring Issues

- Same types of bugs appearing repeatedly
- Same review feedback given repeatedly
- Same types of merge conflicts
- Same misunderstandings about architecture

### 3. Assess Current Learning

- Is there a place to log issues?
- Is there a process to analyze root causes?
- Is there a way to turn learnings into rules?
- Is there follow-up to verify fixes work?

### 4. Surface Learning Gaps (IMPORTANT - these are weaknesses)

- Problems that recur without prevention
- Knowledge that's tribal (not documented)
- Fixes that address symptoms not causes
- Rules that exist but no one knows why

## Output Format

Create a `learning-loop.md` with:

- **Learning loop diagram**
- **5-step process**:
  1. Detect
  2. Capture
  3. Analyze
  4. Prevent
  5. Verify
- **Compound patterns** (escalating detection, abstraction, doc as code)
- **Metrics to track**
- **Integration points**
- **Cadence** (daily, weekly, monthly)
- **Anti-patterns**

Create `violations-log.md` as an empty template with columns:
- Date
- Violation type
- Description
- Root cause
- Prevention action
- Status

Flag gaps as **"Learning System Improvements"** at the bottom.
