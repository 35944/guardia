# Architecture Enforcement

This document defines how the system makes it expensive for AI agents to violate constraints and invariants. Violations are caught early, blocked automatically, and require explicit remediation.

## Enforcement Philosophy

**Make violations expensive by:**

1. **Early detection**: Catch violations before code is written
2. **Automated blocking**: Prevent commits/merges that violate rules
3. **Explicit remediation**: Require documented fixes, not silent workarounds
4. **Learning capture**: Turn violations into system improvements

## Enforcement Layers

```
┌─────────────────────────────────────────────────────────────────────┐
│ LAYER 0: DESIGN TIME (before code)                                   │
│ - TDD architecture compliance audit                                  │
│ - Plan assumption verification                                       │
│ - Structure check                                                    │
├─────────────────────────────────────────────────────────────────────┤
│ LAYER 1: EDIT TIME (during code)                                     │
│ - IDE/editor linting                                                 │
│ - Real-time type checking                                            │
├─────────────────────────────────────────────────────────────────────┤
│ LAYER 2: COMMIT TIME (before commit)                                 │
│ - Pre-commit hooks (formatting, linting, types)                      │
│ - Import/dependency validation                                       │
├─────────────────────────────────────────────────────────────────────┤
│ LAYER 3: PHASE TIME (after each phase)                               │
│ - Phase QA validation                                                │
│ - Architecture checker                                               │
│ - Test suite                                                         │
├─────────────────────────────────────────────────────────────────────┤
│ LAYER 4: MERGE TIME (before merge)                                   │
│ - Full governance check                                              │
│ - CI quality gates                                                   │
│ - Manual review                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

## Layer 0: Design Time Enforcement

### TDD Architecture Compliance Audit

**When**: During Research phase, before planning

**Checks**:

- [ ] Constraints from `constraints.md` not violated
- [ ] Invariants from `invariants.md` preserved
- [ ] {{BOUNDARY_TYPE}} boundaries respected
- [ ] File placement follows structure documentation

**Enforcement**:

```markdown
## Architecture Compliance Audit

### Constraints Checked
- [ ] {{CONSTRAINT_1}}: ✅ Compliant
- [ ] {{CONSTRAINT_2}}: ✅ Compliant
- [ ] {{CONSTRAINT_3}}: ✅ Compliant

### Invariants Preserved
- [ ] {{INVARIANT_1}}: ✅ Maintained
- [ ] {{INVARIANT_2}}: ✅ Required in plan

### Blockers
- ⚠️ Blocker: [describe]
- ℹ️ Needs review: [describe]
```

**Cost of Violation**: TDD rejected, cannot proceed to planning.

### Plan Assumption Verification

**When**: During Planning phase

**Checks**:

- [ ] Implementation Assumptions section exists
- [ ] Each assumption tagged with confidence level
- [ ] File paths verified via search
- [ ] Placement correct per structure documentation

**Enforcement**: Review agent rejects plans missing assumptions.

**Cost of Violation**: Plan returned for iteration, time lost.

---

## Layer 1: Edit Time Enforcement

### IDE/Editor Integration

**Tools**: {{EDIT_TIME_TOOLS}}

**Checks**:

- Syntax errors (immediate)
- Type errors (immediate)
- Linting violations (immediate)
- Import errors (immediate)

**Cost of Violation**: Red squiggles, cannot ignore easily.

---

## Layer 2: Commit Time Enforcement

### Pre-Commit Hooks

**Configuration**: `{{PRE_COMMIT_CONFIG}}`

**{{LANGUAGE_1}} Hooks**:

```{{CONFIG_FORMAT}}
{{LANGUAGE_1_HOOKS}}
```

**{{LANGUAGE_2}} Hooks**:

```{{CONFIG_FORMAT}}
{{LANGUAGE_2_HOOKS}}
```

**Checks Enforced**:

| Check | Tool | Blocking |
|-------|------|----------|
{{#COMMIT_CHECKS}}
| {{CHECK_NAME}} | {{TOOL}} | {{BLOCKING}} |
{{/COMMIT_CHECKS}}

**Cost of Violation**: Commit blocked, must fix to proceed.

### {{BOUNDARY_TYPE}} Boundary Enforcement

**Configuration**: `{{BOUNDARY_CONFIG}}`

**Rules**:

```{{CONFIG_FORMAT}}
{{BOUNDARY_RULES}}
```

**Cost of Violation**: Commit blocked with clear error message showing violating import/dependency.

---

## Layer 3: Phase Time Enforcement

### Phase QA Validation

**When**: After each execution phase, before user confirmation

**Commands**:

```bash
{{PHASE_QA_COMMANDS}}
```

**Cost of Violation**: Phase marked incomplete, cannot proceed to next phase.

### Architecture Checker

**Script**: `{{ARCHITECTURE_SCRIPT}}`

**Checks**:

{{#ARCHITECTURE_CHECKS}}
- {{CHECK_NAME}}
{{/ARCHITECTURE_CHECKS}}

**Cost of Violation**: Architecture report with violations, must fix before proceeding.

---

## Layer 4: Merge Time Enforcement

### Governance Check Script

**Script**: `{{GOVERNANCE_SCRIPT}}`

**Checks**:

{{#GOVERNANCE_CHECK_LIST}}
1. {{CHECK}}
{{/GOVERNANCE_CHECK_LIST}}

```bash
{{GOVERNANCE_SCRIPT_CONTENT}}
```

**Cost of Violation**: Merge blocked, must fix or follow override protocol.

### Override Protocol (Making Bypass Expensive)

**Required for any governance bypass**:

1. **Label**: `override:governance` on PR/MR
2. **Documentation**:
   - Justification (why bypass needed)
   - Explicit risks (what could go wrong)
   - Mitigation (how risks are managed)
3. **Approvals**: {{APPROVAL_COUNT}} maintainers including {{REQUIRED_APPROVER}}
4. **Decision Record**: Create/update ADR documenting the override
5. **Follow-up**: Issue created to remediate within {{REMEDIATION_TIMELINE}}
6. **Learning Loop**: Entry added to `violations-log.md`

**Cost of Bypass**: Significant documentation burden, multiple approvals, mandatory follow-up.

---

## {{TECH_SPECIFIC_SECTION}} Enforcement

### {{TECH_SPECIFIC_RULE_NAME}}

**Location**: `{{TECH_SPECIFIC_CONFIG_PATH}}`

**Structure**:

```{{CONFIG_FORMAT}}
{{TECH_SPECIFIC_CONFIG}}
```

**Enforcement**: {{TECH_SPECIFIC_ENFORCEMENT_DESCRIPTION}}

### Adding New Rules

When a pattern emerges that should be enforced:

1. Create/update `{{TECH_SPECIFIC_CONFIG_PATH}}`
2. Register in {{REGISTRATION_LOCATION}}
3. Checker automatically picks up new rules
4. Document in learning loop

---

## Violation Cost Summary

| Layer | Violation Type | Cost |
|-------|---------------|------|
| Design | Constraint violation in TDD | TDD rejected, iterate |
| Design | Missing assumptions in plan | Plan returned, iterate |
| Edit | Syntax/type error | Cannot save valid code |
| Commit | Format/lint failure | Commit blocked |
| Commit | {{BOUNDARY_TYPE}} boundary violation | Commit blocked |
| Phase | Test failure | Phase incomplete, cannot proceed |
| Phase | Architecture violation | Must fix before next phase |
| Merge | Governance failure | Merge blocked |
| Merge | Override without protocol | Merge blocked, escalation |

---

## Escalation Path

When enforcement blocks progress:

1. **Self-fix**: Agent attempts to fix violation (max 3 tries)
2. **Debug**: Investigate root cause
3. **Consult**: Check learning loop for similar past violations
4. **Escalate**: Request human review with full context
5. **Override**: If business-critical, follow override protocol

---

## Monitoring Enforcement Effectiveness

Track metrics:

- Violations caught at each layer
- Time to fix violations
- Override frequency
- Learning loop entries created

Goal: Catch more violations earlier (shift left), reduce override frequency over time.

---

## Template Instructions

### Key Customizations

| Placeholder | Description | Example |
|-------------|-------------|---------|
| `{{EDIT_TIME_TOOLS}}` | IDE linting tools | "ESLint, Ruff, mypy" |
| `{{PRE_COMMIT_CONFIG}}` | Pre-commit config file | ".pre-commit-config.yaml" |
| `{{BOUNDARY_TYPE}}` | Dependency boundary type | "Import", "Module", "Package" |
| `{{BOUNDARY_CONFIG}}` | Boundary config file | "importlinter.ini" |
| `{{PHASE_QA_COMMANDS}}` | Commands run after each phase | Your test/lint commands |
| `{{ARCHITECTURE_SCRIPT}}` | Architecture check script | "scripts/check-architecture.js" |
| `{{GOVERNANCE_SCRIPT}}` | Pre-merge check script | "scripts/check-governance.sh" |
| `{{APPROVAL_COUNT}}` | Override approvals needed | 2 |
| `{{REMEDIATION_TIMELINE}}` | Time to fix override | "1 sprint" |

### Building Your Enforcement Layer

**Start with what you have:**
1. List all existing pre-commit hooks
2. List all CI checks
3. List all linting rules
4. List all test requirements

**Identify gaps:**
1. What violations slip through?
2. What gets caught late (at merge) that could be caught early (at commit)?
3. What's documented but not enforced?

**Prioritize:**
1. Add enforcement for most common violations first
2. Make the feedback loop fast (seconds, not minutes)
3. Ensure error messages are clear and actionable
