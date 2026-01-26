# Learning Loop: Compound Engineering

This document defines how the system learns from mistakes. When AI agents make errors, the system captures the root cause and updates itself to prevent recurrence. This creates compound improvements over time.

## Learning Loop Overview

```
┌─────────────┐     detect      ┌─────────────┐     analyze     ┌─────────────┐
│  VIOLATION  │ ──────────────► │   CAPTURE   │ ──────────────► │  ROOT CAUSE │
└─────────────┘                 └─────────────┘                 └─────────────┘
                                                                       │
                                                                       │
┌─────────────┐     verify      ┌─────────────┐     update      │
│   IMPROVE   │ ◄────────────── │   PREVENT   │ ◄──────────────┘
└─────────────┘                 └─────────────┘
```

## The Learning Process

### Step 1: Detect Violation

**Trigger**: Any of:

- Pre-commit hook failure
- Phase QA failure
- Architecture check failure
- Governance check failure
- Human review rejection
- Production incident

### Step 2: Capture Context

**Log Entry**: Create entry in `violations-log.md`

```markdown
## [YYYY-MM-DD] Violation: [Short Description]

### Context
- Task: [Task ID] - [Task Name]
- Phase: [Research/Planning/Review/Execute/Merge]
- Agent: [Agent ID]
- Files: [affected files]

### Violation Details
- Type: [constraint/invariant/process/governance]
- Rule violated: [specific rule from constraints.md/invariants.md]
- Detection layer: [design/edit/commit/phase/merge]

### Evidence
[Paste actual error message, failed check output, etc.]
```

### Step 3: Root Cause Analysis

**Questions to Answer**:

1. **What failed?** (Symptom)
   - What check/gate blocked progress?
   - What was the exact error?

2. **Why did it fail?** (Proximate cause)
   - What code/change caused the failure?
   - When was the violation introduced?

3. **Why was it possible?** (Root cause)
   - What gap in the system allowed this violation?
   - Why wasn't it caught earlier?
   - What knowledge was missing?

4. **How can we prevent recurrence?** (Systemic fix)
   - What rule/check should be added?
   - What documentation should be updated?
   - What gate should be strengthened?

**Document Analysis**:

```markdown
### Root Cause Analysis

#### Symptom
[What failed]

#### Proximate Cause
[What code caused it]

#### Root Cause
[Why the system allowed it]

#### Prevention Strategy
[How to prevent recurrence]
```

### Step 4: Prevent Recurrence

**Update Options** (choose one or more):

| Update Type | When to Use | Location |
|-------------|-------------|----------|
| Constraint | New "never do" rule discovered | `constraints.md` |
| Invariant | New "always true" requirement | `invariants.md` |
| Process | Workflow gap identified | `process.md` |
| Enforcement | New check needed | `enforcement.md`, hooks, scripts |
| {{TECH_RULE_TYPE}} | Tech-specific pattern | `{{TECH_RULE_LOCATION}}` |
| Decision Record | Architectural decision needed | `{{DECISION_DOCS_PATH}}` |
| Agent Guide | Command/pattern for agents | `{{AGENT_GUIDE}}` |

**Document the Update**:

```markdown
### Prevention Applied

#### Update Type
[constraint/invariant/process/enforcement/tech-rule/decision]

#### Change Made
[Describe the change]

#### Location
[File path]

#### Verification
[How to verify the fix works]
```

### Step 5: Verify Improvement

**Test the Prevention**:

1. Reproduce the original violation scenario
2. Verify the new check catches it
3. Verify the error message is clear
4. Update the violation log with verification result

```markdown
### Verification

#### Reproduction Test
- [ ] Original scenario reproduced
- [ ] New check catches violation
- [ ] Error message is clear

#### Status
[✅ Prevention verified / ❌ Needs iteration]
```

---

## Compound Patterns

### Pattern 1: Escalating Detection

**Goal**: Catch violations earlier over time.

```
Merge → Phase → Commit → Edit → Design
```

When a violation is caught at merge time, ask: "How could we have caught this at design time?"

**Example**:

- Violation: {{BOUNDARY_TYPE}} boundary violation caught at merge
- Prevention: Add to plan template: "Verify no {{BOUNDARY_TYPE}} violations in affected files"
- Result: Next time caught during planning, not merge

### Pattern 2: Failure Class Abstraction

**Goal**: One fix prevents a class of failures, not just one instance.

**Example**:

- Violation: Agent created file in wrong location
- Narrow fix: Add check for that specific file
- Abstract fix: Add structure verification to plan template
- Result: All future file placements verified, not just this one

### Pattern 3: Documentation as Code

**Goal**: Turn documentation into executable checks.

**Example**:

- Violation: Invariant violated (documented but not enforced)
- Documentation: Rule exists in invariants.md
- Code: Add automated check for the rule
- Result: Documentation now enforced automatically

---

## Learning Loop Metrics

Track these metrics to measure learning effectiveness:

### Leading Indicators

- Time from violation to prevention deployed
- Violations per task (should decrease)
- Violations caught earlier (shift left)

### Lagging Indicators

- Recurrence rate (same violation type)
- Override frequency
- Production incidents

### Targets

| Metric | Target | Current |
|--------|--------|---------|
| Violations per task | <{{TARGET_VIOLATIONS}} | -- |
| Recurrence rate | 0% | -- |
| Shift left (% caught before merge) | >{{TARGET_SHIFT_LEFT}}% | -- |
| Time to prevention | <{{TARGET_PREVENTION_TIME}} | -- |

---

## Integration Points

### With Process

After every violation:

1. Log in violations-log.md
2. Complete root cause analysis
3. Update relevant process document
4. Verify prevention works

### With Enforcement

Every prevention should result in:

1. New check (if possible to automate)
2. New hook (if early detection possible)
3. Updated enforcement.md (if new layer/check)

### With Agents

Before starting work, agents should:

1. Read recent violations log entries
2. Be aware of new prevention rules
3. Avoid patterns that caused past violations

---

## Continuous Improvement Cadence

### Daily

- Log any new violations immediately
- Quick root cause (5 min)
- Immediate prevention if obvious

### Weekly

- Review violations log
- Complete root cause for any unresolved
- Deploy preventions

### Monthly

- Analyze violation trends
- Identify systemic gaps
- Major system updates if needed

### Quarterly

- Review metrics
- Adjust targets
- Update agent briefing materials

---

## Anti-Patterns

### Symptom Fix

❌ Fix the specific code that caused violation
✅ Fix the system gap that allowed the violation

### One-Off Check

❌ Add check for this specific file/pattern
✅ Add check for the class of violations

### Documentation Only

❌ Add note to documentation, hope agents read it
✅ Turn documentation into automated enforcement

### Blame Agent

❌ "Agent should have known better"
✅ "System should have caught this earlier"

---

## Template Instructions

### Key Customizations

| Placeholder | Description | Example |
|-------------|-------------|---------|
| `{{TECH_RULE_TYPE}}` | Tech-specific rule category | "Domain Rule", "Module Rule" |
| `{{TECH_RULE_LOCATION}}` | Where tech rules live | "app/domains/{domain}/architecture.json" |
| `{{DECISION_DOCS_PATH}}` | Decision records location | "docs/decisions/" |
| `{{AGENT_GUIDE}}` | Main agent guidance file | "CLAUDE.md", "AGENTS.md" |
| `{{TARGET_VIOLATIONS}}` | Target violations per task | 2 |
| `{{TARGET_SHIFT_LEFT}}` | Target % caught early | 80 |
| `{{TARGET_PREVENTION_TIME}}` | Target time to fix | "1 day" |

### Getting Started

1. Create `violations-log.md` from template
2. Start logging violations as they occur
3. Do root cause analysis for each
4. Implement at least one prevention per week
5. Track metrics monthly
6. Review and adjust quarterly
