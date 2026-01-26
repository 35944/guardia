# AI Agent Operating System

This document defines the system in which AI agents operate when expanding {{PROJECT_NAME}}. Multiple agents can work in parallel within this system.

## System Overview

```
┌─────────────────────────────────────────────────────────────────────┐
│                         GOVERNANCE LAYER                             │
│  Constraints (never do) + Invariants (always true) + Purpose         │
└─────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────┐
│                         PROCESS LAYER                                │
│  Research → Planning → Implementation → Merge (with gates)           │
└─────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────┐
│                       ENFORCEMENT LAYER                              │
│  Pre-commit hooks + CI gates + Architecture checks + Linters         │
└─────────────────────────────────────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────┐
│                        LEARNING LAYER                                │
│  Violation logs → Root cause → Rule updates → Knowledge base         │
└─────────────────────────────────────────────────────────────────────┘
```

## Foundational Documents

Every AI agent must internalize these documents before starting work:

| Document | Purpose | Location |
|----------|---------|----------|
| Product Purpose | Why {{PROJECT_NAME}} exists, what problem it solves | `{{DOCS_PATH}}/product-purpose.md` |
| Constraints | What {{PROJECT_NAME}} will never do (non-negotiable) | `{{DOCS_PATH}}/constraints.md` |
| Invariants | What must always be true (architectural requirements) | `{{DOCS_PATH}}/invariants.md` |
| Development Process | Research → Planning → Implementation | `{{DOCS_PATH}}/process.md` |
| {{AGENT_GUIDE}} | Commands, architecture overview, coding standards | `{{AGENT_GUIDE_PATH}}` |

## Agent Types and Responsibilities

### 1. Research Agent

**Purpose**: Understand the problem space before proposing solutions.

**Inputs**: Feature idea, bug report, user feedback

**Outputs**: Technical Design Draft (TDD) with:
- Problem statement and non-goals
- System touchpoints ({{TOUCHPOINT_CATEGORIES}})
- Root cause analysis (for bugs)
- Architecture compliance audit
- Complexity assessment
- Go/No-Go gate for planning

**Constraints**:
- Must reference architecture docs before proposing solutions
- Must cite file paths with line numbers
- Must tag assumptions with confidence levels (CERTAIN/LIKELY/UNCERTAIN/ASSUMED)
- Must not promise implementation

### 2. Planning Agent

**Purpose**: Create bounded, executable implementation plans.

**Inputs**: Approved TDD

**Outputs**: Implementation Plan with:
- User stories ({{USER_STORY_FORMAT}})
- Affected files (verified via search)
- Implementation assumptions (explicit, tagged)
- Architecture compliance check
- Git strategy (branch name, commit checkpoints)
- QA strategy (checklist)

**Constraints**:
- Must verify all file paths exist before listing
- Must include Implementation Assumptions section
- Must check codebase structure for file placement
- Must not use marketing language
- Must not add scope beyond requirements

### 3. Review Agent

**Purpose**: Validate plans against actual codebase before execution.

**Inputs**: Plan from Planning Agent

**Outputs**: Reviewed Plan with:
- Verified/Missing/Different status for each assumption
- Executable task checklist ({{MAX_TASKS_PER_PHASE}} tasks per phase max)
- Current state audit results
- Completeness score (/10)

**Constraints**:
- Must complete deep audit before approving any plan
- Must verify every assumption with actual code references
- Must reject plans with >50% wrong assumptions
- Must not generate assumptions during review

### 4. Execution Agent

**Purpose**: Execute approved task checklists with production safety.

**Inputs**: Reviewed and approved plan

**Outputs**:
- Completed tasks with commit IDs
- QA validation results per phase
- Architecture check results

**Constraints**:
- Must execute one task at a time
- Must pause after each phase for user confirmation
- Must run QA validation after each phase
- Must not proceed if build/tests fail
- Must not use mocks/placeholders in production code

### 5. Merge Agent

**Purpose**: Ensure governance compliance before merge.

**Inputs**: Completed execution with all phases done

**Outputs**:
- Governance evidence package
- Merge or block decision

**Constraints**:
- Must block merge if any governance check fails
- Must document manual override with full protocol
- Must update tracking after merge

## Parallel Agent Coordination

### Worktree Isolation

Each agent operates in its own git worktree:

```
{{REPO_PATH}}              # Main worker
{{REPO_PATH}}-agentA       # Agent A
{{REPO_PATH}}-agentB       # Agent B (if needed)
```

### Branch Naming Convention

```
feature/{{TASK_ID_FORMAT}}   # Feature work
bugfix/{{TASK_ID_FORMAT}}    # Bug fix
hotfix/{{TASK_ID_FORMAT}}    # Hotfix
```

### {{DATABASE_OR_STATE}} Isolation

Each worktree uses separate {{DATABASE_OR_STATE}}:

```
{{ISOLATION_EXAMPLE}}
```

### Conflict Prevention

1. Check {{TRACKING_LOCATION}} before starting
2. Claim files to prevent overlap
3. {{MIGRATION_TYPE}} changes require explicit coordination
4. Merge order: Agent A first, then main worker rebases

## State Machine: Agent Lifecycle

```
┌─────────┐     TDD         ┌─────────┐     Plan       ┌─────────┐
│  IDEA   │ ──────────────► │   TDD   │ ─────────────► │  PLAN   │
└─────────┘   Research      └─────────┘   Planning     └─────────┘
                              Agent                       Agent
                                │                           │
                                │ Gate ❌                    │ Gate ❌
                                ▼                           ▼
                            [Iterate]                   [Iterate]
                                                            │
                                                            │ Gate ✅
                                                            ▼
┌─────────┐     Merge       ┌─────────┐    Execute     ┌─────────┐
│ MERGED  │ ◄────────────── │EXECUTED │ ◄───────────── │REVIEWED │
└─────────┘   Merge Agent   └─────────┘   Execution    └─────────┘
                              Agent                     Review Agent
```

## Trust Boundaries

### High Trust (automated)

{{#HIGH_TRUST_ITEMS}}
- {{ITEM}} ({{TOOL}})
{{/HIGH_TRUST_ITEMS}}

### Medium Trust (human spot-check)

- Code review for logic correctness
- QA validation for user experience
- Assumption verification during review

### Low Trust (human approval required)

{{#LOW_TRUST_ITEMS}}
- {{ITEM}}
{{/LOW_TRUST_ITEMS}}

## Error Recovery

### Execution Failure

1. Stop at failing task
2. Log error with context
3. Attempt fix (max 3 tries)
4. If still failing: pause, request human help

### Governance Failure

1. Log all violations
2. Per violation: choose fix or override
3. Implement fixes with atomic commits
4. Re-run governance checks
5. Repeat until all pass

---

## Template Instructions

### Customization Checklist

- [ ] Replace `{{PROJECT_NAME}}` with your project name
- [ ] Set `{{DOCS_PATH}}` to your principles documentation path
- [ ] Define `{{TOUCHPOINT_CATEGORIES}}` (e.g., "UI, API, data, external")
- [ ] Set `{{USER_STORY_FORMAT}}` (e.g., "Gherkin", "As a... I want... So that...")
- [ ] Set `{{MAX_TASKS_PER_PHASE}}` (recommended: 3-5)
- [ ] Define `{{TASK_ID_FORMAT}}` (e.g., "B[N]-[description]", "JIRA-123")
- [ ] Set `{{DATABASE_OR_STATE}}` and `{{ISOLATION_EXAMPLE}}` for your stack
- [ ] Set `{{TRACKING_LOCATION}}` (e.g., "project board", "tracking doc")
- [ ] List `{{HIGH_TRUST_ITEMS}}` and `{{LOW_TRUST_ITEMS}}` for your context

### Tips

- Start simple: Use 1 agent type initially, add more as team grows
- Trust boundaries evolve: Move items from low→medium→high as confidence builds
- Tracking is key: Agents need a single source of truth for coordination
