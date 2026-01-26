# Combined Analysis Prompt (Full System)

> **Purpose**: Comprehensive analysis to create a complete AI agent governance system in one pass.
> **Output**: All 8 governance documents plus a GAPS.md summary

---

## Instructions for AI Assistant

Analyze this codebase comprehensively to create a complete AI agent governance system.

## Analysis Process

Run all 7 individual analyses:

1. **Product Purpose** - What does this product do and for whom?
2. **Constraints** - What should NEVER happen?
3. **Invariants** - What must ALWAYS be true?
4. **System** - How do agents coordinate?
5. **Process** - What is the development workflow?
6. **Enforcement** - How are rules automated?
7. **Learning Loop** - How does the system improve?

## Synthesis Steps

### 1. Cross-Reference Findings

After completing individual analyses, verify alignment:

- Do constraints align with what's enforced?
- Do invariants match actual patterns?
- Does the process match how work actually flows?
- Is enforcement covering the constraints and invariants?

### 2. Prioritize Improvements

Rank all discovered weaknesses:

- What's the biggest gap between documented and actual?
- What causes the most recurring problems?
- What would have the highest impact if fixed?

### 3. Create Implementation Plan

Categorize improvements by effort:

- **Quick wins** (can fix this week)
- **Medium effort** (can fix this month)
- **Large effort** (needs dedicated project)

## Output

Create all 9 documents:

1. `product-purpose.md` - Mission, capabilities, users
2. `constraints.md` - What must never happen
3. `invariants.md` - What must always be true
4. `system.md` - Agent operating system
5. `process.md` - Development workflow
6. `enforcement.md` - Automated validation
7. `learning-loop.md` - Continuous improvement
8. `violations-log.md` - Empty template for tracking
9. `GAPS.md` - Summary of all weaknesses and prioritized improvements

## GAPS.md Format

```markdown
# Governance Gaps Analysis

## Critical (Fix This Week)
- [ ] Gap description - Source: [which analysis found it]

## Important (Fix This Month)
- [ ] Gap description - Source: [which analysis found it]

## Improvement (Backlog)
- [ ] Gap description - Source: [which analysis found it]

## Cross-Cutting Issues
Issues that appeared in multiple analyses:
- Issue X appeared in: Constraints, Enforcement, Learning Loop
```
