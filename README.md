# Guardia

**Governance system for AI agents working on your codebase.**

Guardia helps you create a system of constraints, invariants, processes, and learning loops that enable AI agents to work on your codebase safely and effectively—while improving the codebase over time.

## The Problem

When AI agents work on code, they can:
- Violate architectural patterns they don't know about
- Create inconsistent code across the codebase
- Make the same mistakes repeatedly
- Work in ways that conflict with other agents

## The Solution

Guardia provides templates and prompts to create:

1. **Foundation** - What the project is and its boundaries
2. **Process** - How work flows from idea to merged code
3. **Enforcement** - How rules are automatically enforced
4. **Learning** - How mistakes become system improvements

## Quick Start

### Option 1: Use the Prompts (Recommended)

1. Copy this folder to your project
2. Open `prompts/README.md` for the full index of available prompts
3. Run each prompt with your AI agent of choice (Claude Code, Cursor, etc.)
4. The prompts will analyze your codebase and generate customized documents

**For governance setup**: Start with `prompts/combined-analysis.md` to generate all governance documents at once, or run individual prompts in order.

**For codebase transformation**: Use the transformation prompts to restructure and document your codebase.

### Option 2: Use the Templates Directly

1. Copy the `templates/` folder to your project's `docs/principles/` (or similar)
2. Fill in the placeholders (marked with `{{PLACEHOLDER}}`)
3. Remove the "Template Instructions" sections when done

## Folder Structure

```
guardia/
├── README.md                 # This file
├── prompts/                  # AI prompts for codebase analysis
│   ├── README.md             # Prompt index and usage guide
│   │
│   │   # Governance prompts
│   ├── product-purpose.md    # Analyze and define product purpose
│   ├── constraints.md        # Identify things that should never happen
│   ├── invariants.md         # Identify things that must always be true
│   ├── system.md             # Design AI agent operating system
│   ├── process.md            # Define development workflow
│   ├── enforcement.md        # Design automated enforcement
│   ├── learning-loop.md      # Design continuous improvement
│   ├── combined-analysis.md  # Generate all governance docs at once
│   │
│   │   # Codebase transformation prompts
│   ├── domain-driven-restructure.md  # Technical → domain-driven structure
│   ├── codebase-structure-diagram.md # Generate visual codebase overview
│   └── domain-readme-generator.md    # Generate READMEs per domain
│
├── templates/
│   ├── foundation/
│   │   ├── product-purpose.md   # Why the project exists
│   │   ├── constraints.md       # What you never do
│   │   └── invariants.md        # What must always be true
│   ├── process/
│   │   ├── system.md            # AI agent operating system
│   │   └── process.md           # Development workflow
│   ├── enforcement/
│   │   └── enforcement.md       # How rules are enforced
│   └── learning/
│       ├── learning-loop.md     # How to learn from mistakes
│       └── violations-log.md    # Where to log violations
└── examples/
    └── (example implementations)
```

## The Four Layers

### 1. Foundation

**Documents**: `product-purpose.md`, `constraints.md`, `invariants.md`

Foundation documents answer:
- **Product Purpose**: Why does this project exist? What problem does it solve?
- **Constraints**: What should we NEVER do? (Non-negotiable prohibitions)
- **Invariants**: What must ALWAYS be true? (Architectural requirements)

### 2. Process

**Documents**: `system.md`, `process.md`

Process documents answer:
- **System**: How do AI agents operate? How do they coordinate?
- **Process**: What are the phases of work? What are the gates?

### 3. Enforcement

**Document**: `enforcement.md`

Enforcement answers:
- How are rules automatically enforced?
- What blocks commits, merges, deployments?
- What's the cost of violation at each layer?

### 4. Learning

**Documents**: `learning-loop.md`, `violations-log.md`

Learning answers:
- How do we capture mistakes?
- How do we analyze root causes?
- How do we prevent recurrence?
- How do we measure improvement?

## Codebase Transformation

Beyond governance, Guardia includes prompts for transforming and documenting codebases:

| Prompt | Purpose |
|--------|---------|
| `domain-driven-restructure.md` | Transform technically-layered code into domain-driven structure |
| `codebase-structure-diagram.md` | Generate a visual overview of the entire codebase |
| `domain-readme-generator.md` | Generate README index files for each domain folder |

**Recommended sequence** for full transformation:
1. Restructure code into domains
2. Generate codebase structure diagram
3. Generate per-domain READMEs

These prompts work standalone on any codebase structure.

## Implementation Guide

### Phase 1: Foundation

1. Run the Product Purpose prompt → Create `product-purpose.md`
2. Run the Constraints prompt → Create `constraints.md`
3. Run the Invariants prompt → Create `invariants.md`

**Outcome**: AI agents understand what the project is and its boundaries.

### Phase 2: Process

1. Run the System prompt → Create `system.md`
2. Run the Process prompt → Create `process.md`

**Outcome**: AI agents know how to work and what gates to pass.

### Phase 3: Enforcement

1. Run the Enforcement prompt → Create `enforcement.md`
2. Implement missing enforcement (pre-commit hooks, CI checks)
3. Update enforcement.md with actual commands

**Outcome**: Rules are automatically enforced, not just documented.

### Phase 4: Learning (Ongoing)

1. Run the Learning Loop prompt → Create `learning-loop.md`
2. Create `violations-log.md` from template
3. Start logging violations as they occur
4. Do root cause analysis weekly
5. Run system violations trends monthly

**Outcome**: The system improves over time.

## Using with AI Agents

### Claude Code / Cursor / Similar

Add to your project's `CLAUDE.md` or equivalent:

```markdown
## AI Agent Operating System

Before starting work, read the foundational documents in `docs/principles/`:

| Document | Purpose |
|----------|---------|
| `product-purpose.md` | Why this project exists |
| `constraints.md` | What we never do |
| `invariants.md` | What must always be true |
| `system.md` | How AI agents operate |
| `process.md` | Development workflow |
| `enforcement.md` | How rules are enforced |
| `learning-loop.md` | How mistakes improve the system |
| `violations-log.md` | History of violations |
```

### Multiple Agents in Parallel

If running multiple agents:

1. Use separate git worktrees for each agent
2. Use separate databases/state for each agent
3. Track active work in a shared location
4. Coordinate schema/migration changes explicitly

See `system.md` for detailed coordination protocols.

## Customization Checklist

After generating documents, verify:

- [ ] All `{{PLACEHOLDER}}` values replaced
- [ ] Examples use actual code from your codebase
- [ ] Commands are correct for your tech stack
- [ ] File paths match your project structure
- [ ] "Template Instructions" sections removed
- [ ] Documents cross-reference each other correctly

## Measuring Success

Track these metrics:

| Metric | Target | Description |
|--------|--------|-------------|
| Violations per task | <2 | Fewer mistakes over time |
| Recurrence rate | 0% | Same mistake never happens twice |
| Shift left | >80% | Violations caught early (commit, not merge) |
| Time to prevention | <1 day | Fast turnaround on fixes |

## FAQ

### How is this different from just writing documentation?

Documentation tells agents what to do. Guardia creates a **system** that:
- Enforces rules automatically (not just documents them)
- Learns from mistakes (not just records them)
- Improves over time (not just gets stale)

### Do I need all the documents?

Start with Foundation (product-purpose, constraints, invariants). Add others as needed.

Minimum viable system:
1. `constraints.md` - What never to do
2. `invariants.md` - What must always be true
3. `violations-log.md` - Where to log mistakes

### How do I handle violations?

1. Log it in `violations-log.md`
2. Do root cause analysis (5 whys)
3. Implement prevention (new rule, new check, new enforcement)
4. Verify the prevention works
5. Update the system documents

### Can this work with any tech stack?

Yes. The templates use placeholders for tech-specific details. The prompts analyze your actual codebase and generate appropriate content.

## Contributing

Improvements welcome! Areas to help:
- Examples for specific tech stacks
- Additional prompts for specific scenarios
- Integration guides for specific AI agents
- Translations

## License

MIT - Use freely, attribution appreciated.

---

*Guardia: Because AI agents work better with guardrails.*
