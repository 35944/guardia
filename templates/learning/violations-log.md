# Violations Log

This log captures all violations and their resolutions for learning and prevention. When AI agents make mistakes, they are logged here, analyzed for root cause, and used to improve the system.

## Statistics

- Total violations: 0
- By type: constraints 0, invariants 0, process 0, governance 0
- By phase: research 0, planning 0, review 0, execute 0, merge 0
- Prevention rules added: 0

---

## How to Log a Violation

When a violation is detected, add an entry using this template:

```markdown
## [YYYY-MM-DD] Violation: [Short Description]

### Context

- Task: [Task ID] - [Task Name]
- Phase: [Research/Planning/Review/Execute/Merge]
- Agent: [Agent ID or "Main"]
- Files: [affected files]

### Violation Details

- Type: [constraint/invariant/process/governance]
- Rule violated: [specific rule from constraints.md/invariants.md/process.md]
- Detection layer: [design/edit/commit/phase/merge]

### Evidence

[Paste actual error message, failed check output, etc.]

### Root Cause Analysis

#### Symptom

[What failed]

#### Proximate Cause

[What code/action caused it]

#### Root Cause

[Why the system allowed it]

#### Prevention Strategy

[How to prevent recurrence]

### Prevention Applied

- Update type: [constraint/invariant/process/enforcement/tech-rule/decision/none-yet]
- Location: [file path or "pending"]
- Change: [description of change]

### Verification

- [ ] Original scenario reproduced
- [ ] New check catches violation
- [ ] Error message is clear

### Status

[✅ Resolved / ⏳ Pending / 🔄 In Progress]
```

---

## Log Entries

(No violations logged yet)

---

## Pending Preventions

(No pending preventions)

---

## Patterns Observed

(No patterns observed yet - patterns will be documented as violations accumulate)

---

## Template Instructions

### When to Log

Log a violation when:

- A pre-commit hook blocks a commit
- A test fails during phase QA
- An architecture check finds violations
- A governance check blocks a merge
- A human reviewer rejects code
- A bug reaches production that should have been caught

### How to Analyze

For each violation, ask:

1. **What** failed? (The symptom)
2. **Why** did it fail? (The immediate cause)
3. **Why** was that possible? (The root cause)
4. **How** do we prevent it? (The systemic fix)

### Updating Statistics

After adding each entry:

1. Increment "Total violations"
2. Increment the appropriate "By type" counter
3. Increment the appropriate "By phase" counter
4. When prevention is applied, increment "Prevention rules added"

### Identifying Patterns

After 5+ violations, look for:

- Same type recurring (constraint vs invariant vs process)
- Same phase recurring (caught late vs early)
- Same area of codebase
- Same agent or workflow

Patterns indicate systemic issues needing bigger fixes.
