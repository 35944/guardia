# Development Process

This document defines the development process for AI agents expanding {{PROJECT_NAME}}. It operates within the system defined in `system.md` and respects the constraints and invariants.

## Process Overview

```
┌────────────────────────────────────────────────────────────────────────┐
│ 1. RESEARCH                                                             │
│    Input: Idea/Bug → Output: TDD → Gate: Go/No-Go                      │
├────────────────────────────────────────────────────────────────────────┤
│ 2. PLANNING                                                             │
│    Input: TDD → Output: Plan → Gate: Scope Check                       │
├────────────────────────────────────────────────────────────────────────┤
│ 3. REVIEW                                                               │
│    Input: Plan → Output: Executable Plan → Gate: Deep Audit            │
├────────────────────────────────────────────────────────────────────────┤
│ 4. EXECUTION                                                            │
│    Input: Plan → Output: Working Code → Gate: Phase QA                 │
├────────────────────────────────────────────────────────────────────────┤
│ 5. MERGE                                                                │
│    Input: Completed Build → Output: Merged Branch → Gate: Governance   │
└────────────────────────────────────────────────────────────────────────┘
```

## Phase 1: Research

**Goal**: Understand the problem space before proposing solutions.

### Inputs

- Feature idea (chat message, document, user feedback)
- Bug report with reproduction steps
- Enhancement request

### Process

1. **Frame the Problem**: Restate in system terms, note unknowns
2. **Confirm Scope**: Ask what NOT to change (prevent scope creep)
3. **Surface Constraints**: Check `constraints.md` and `invariants.md`
4. **Check Active Work**: Review {{TRACKING_LOCATION}} for conflicts
5. **Identify System Touchpoints**: {{TOUCHPOINT_CATEGORIES}}

### Required Reference Checkpoints

- Architecture docs: `{{ARCHITECTURE_DOCS_PATH}}`
- Codebase structure: `{{STRUCTURE_DOC_PATH}}`
- Existing plans: `{{COMPLETED_PLANS_PATH}}`
- Active work: `{{ACTIVE_WORK_PATH}}`

### Output: Technical Design Draft (TDD)

```markdown
# TDD: [Idea Slug]

## Idea Intake
- Source: [chat/file path]
- Problem Statement: [1-2 sentences]
- Non-Goals: [explicit exclusions]

## System Touchpoints
{{#TOUCHPOINT_SECTIONS}}
- {{TOUCHPOINT}}: [affected areas]
{{/TOUCHPOINT_SECTIONS}}

## Root Cause Analysis (for bugs)
- Input: [what triggers]
- Processing: [which function]
- Output: [what response]
- Root change point: [file:function:line-range]

## Architecture Compliance
- Constraints checked: [list from constraints.md]
- Invariants verified: [list from invariants.md]
- Gaps/Blockers: [list with ⚠️ Blocker or ℹ️ Needs review]

## Complexity Assessment
{{#COMPLEXITY_AREAS}}
- {{AREA}}: [Low/Medium/High] - [justification]
{{/COMPLEXITY_AREAS}}

## Risks & Unknowns
- [risk 1]
- [unknown requiring spike]

## Go/No-Go Gate
- Status: [✅ Ready / ❌ Blocked]
- Blockers: [list if any]
```

### Gate: Go/No-Go

- ✅ Pass if: All blockers resolved, scope clear, architecture compliant
- ❌ Fail if: Unresolved blockers, unclear scope, constraint violations

---

## Phase 2: Planning

**Goal**: Create bounded, executable implementation plan.

### Inputs

- Approved TDD with Go status

### Process

1. **Verify File Paths**: Use search to confirm all paths exist
2. **Check Structure**: Reference codebase structure documentation
3. **Write User Stories**: Use {{USER_STORY_FORMAT}} format
4. **List Affected Files**: With actual paths and line numbers
5. **Document Assumptions**: Tag with confidence levels
6. **Define Git Strategy**: Branch name, commit checkpoints

### Forbidden Language

- Marketing terms: "revolutionary", "seamless", "powerful", "robust"
- Unverified claims: "comprehensive", "full support", "advanced"
- Future tense for past: "Implemented January 2025" when planned

### Output: Implementation Plan

```markdown
# Plan: [Task ID] - [Title]

## Summary
[Clear goal statement in 1-2 sentences]

## User Stories
{{USER_STORY_TEMPLATE}}

## Functional Requirements
1. [Specific requirement]
2. [Specific requirement]

## Non-Goals
- [What this will NOT do]

## Affected Files
| File | Area | Change Type |
|------|------|-------------|
| `path/to/file.ext:45` | area | MODIFY |

## Implementation Assumptions

### {{LAYER_1}} Assumptions (MUST AUDIT)
- [Assumption 1] (UNCERTAIN)
- [Assumption 2] (ASSUMED)

### {{LAYER_2}} Assumptions (MUST AUDIT)
- [Assumption 1] (LIKELY)
- [Assumption 2] (CERTAIN)

Confidence Levels: CERTAIN (95%+), LIKELY (70%+), UNCERTAIN (50/50), ASSUMED (no verification)

## Architecture Compliance
- Areas affected: [list]
- Structure verified: [yes/no]
- Boundaries respected: [verified]

## Git Strategy
- Branch: `{{BRANCH_FORMAT}}`
- Commits: [checkpoint per phase]

## QA Strategy
- [ ] [Test scenario 1]
- [ ] [Test scenario 2]
```

### Gate: Scope Check

- ✅ Pass if: <{{MAX_FILES}} files, <{{MAX_SCENARIOS}} scenarios
- ⚠️ Warn if: Exceeds thresholds → suggest chunking
- ❌ Fail if: Missing assumptions section, unverified paths

---

## Phase 3: Review

**Goal**: Validate plan against actual codebase before execution.

### Inputs

- Plan with Implementation Assumptions section

### Process

1. **Validate Plan Format**: Assumptions section exists with >3 items
2. **Deep Audit**: Verify every assumption against codebase
3. **Structure Validation**: Check file placements
4. **Run Automated Checks**: {{ARCHITECTURE_CHECK_COMMAND}}
5. **Convert to Executable**: Create numbered task checklist
6. **Rate Completeness**: Score /10 with gaps identified

### Deep Audit Protocol

For each assumption:

```bash
{{AUDIT_COMMANDS}}
```

Document results:

```markdown
## Current State Audit Results

### Verified
- [ ] `Component.property` exists: ✅ line 45 / ❌ MISSING

### Gap Analysis
- Missing: [what needs ADD]
- Incomplete: [what needs MODIFY]
```

### Output: Executable Plan

```markdown
## Tasks

### Phase 1.0 - [Description]
- [ ] 1.1 `git commit -m "{{COMMIT_FORMAT}}"`
- [ ] 1.2 [Task with file:line reference]
- [ ] 1.3 [Task with file:line reference]
- [ ] 1.4 QA validation: [specific commands]
- [ ] 1.5 User confirmation checkpoint

### Phase 2.0 - [Description]
...
```

### Gate: Deep Audit

- ✅ Pass if: <50% assumptions wrong, all paths verified
- ❌ Fail if: >50% assumptions wrong → present options by complexity

---

## Phase 4: Execution

**Goal**: Execute tasks with production safety.

### Inputs

- Reviewed and approved executable plan

### Process

1. **Determine Worktree**: Check which worktree you're in
2. **Find Next Task**: First uncompleted `[ ]` item
3. **Execute Single Task**: One at a time
4. **Run QA**: Layer-specific validation
5. **Mark Complete**: Update `[x]`, get user confirmation
6. **Git Commit**: Add commit ID when phase complete
7. **PAUSE**: Await user confirmation before next phase

### QA Commands by Layer

```bash
{{QA_COMMANDS}}
```

### Stop Conditions

- Plan format incorrect → return to Review
- {{MIGRATION_TYPE}} change needed → STOP, request coordination
- Build/test fails → fix before continuing
- 3 failed fix attempts → pause, request help
- User rejects QA → address issues
- Mock/placeholder detected → remove before proceeding

### Gate: Phase QA

- ✅ Pass if: All tests pass, lint clean, architecture valid
- ❌ Fail if: Any check fails → fix and re-run

---

## Phase 5: Merge

**Goal**: Merge only when governance satisfied.

### Inputs

- Completed execution with all phases done
- Local acceptance gate passed

### Prerequisites

1. All phases marked complete
2. `{{ACCEPTANCE_SCRIPT}}` passes
3. Branch rebased on main
4. Tracking updated

### Governance Checks

All must pass:

{{#GOVERNANCE_CHECKS}}
1. **{{CHECK_NAME}}**: {{CHECK_DESCRIPTION}}
{{/GOVERNANCE_CHECKS}}

### Commands

```bash
{{GOVERNANCE_COMMANDS}}
```

### Override Protocol (exception only)

Required when business-critical:

1. Label: `override:governance`
2. Justification with explicit risks
3. {{APPROVAL_COUNT}} approvals (including {{REQUIRED_APPROVER}})
4. ADR/decision entry capturing override
5. Follow-up issue to remediate

### Gate: Governance

- ✅ Pass if: All checks pass OR valid override
- ❌ Fail if: Any check fails without override → fix and re-run

---

## Quick Reference: Phase Gates

| Phase | Gate Name | Pass Criteria | Fail Action |
|-------|-----------|---------------|-------------|
| Research | Go/No-Go | Blockers resolved, scope clear | Iterate on TDD |
| Planning | Scope Check | <{{MAX_FILES}} files, assumptions documented | Chunk or iterate |
| Review | Deep Audit | <50% wrong assumptions | Present options |
| Execution | Phase QA | Tests pass, lint clean | Fix and re-run |
| Merge | Governance | All checks pass | Fix or override |

## Anti-Patterns

### Skip Research

❌ "We already know what to build"
✅ Always frame problem, surface constraints, check conflicts

### Vague Planning

❌ "Details for implementation"
✅ Specific tasks with file:line references

### Assumptions During Review

❌ Generate assumptions when reviewing
✅ Reject plan, return to Planning to add assumptions

### Batch Execution

❌ Complete multiple phases, then report
✅ One phase at a time with user confirmation

### Governance Bypass

❌ "This is a small change, skip checks"
✅ Always run governance, override with full protocol if needed

---

## Template Instructions

### Key Placeholders to Customize

| Placeholder | Description | Example |
|-------------|-------------|---------|
| `{{TRACKING_LOCATION}}` | Where active work is tracked | "Jira board", "GitHub Projects" |
| `{{TOUCHPOINT_CATEGORIES}}` | System areas | "UI, API, Database, External" |
| `{{USER_STORY_FORMAT}}` | Story format | "Gherkin", "As a..." |
| `{{MAX_FILES}}` | Max files per plan | 15 |
| `{{MAX_SCENARIOS}}` | Max test scenarios | 10 |
| `{{BRANCH_FORMAT}}` | Branch naming | "feature/JIRA-123-desc" |
| `{{QA_COMMANDS}}` | Test/lint commands | Your test runner commands |
| `{{GOVERNANCE_CHECKS}}` | Merge requirements | Your CI checks |
| `{{APPROVAL_COUNT}}` | Override approvals | 2 |

### Tips

- Adjust phase complexity to match team maturity
- Start with lighter gates, tighten as needed
- The 50% assumption threshold is a starting point - adjust based on experience
- Document your QA commands exactly as they should be run
