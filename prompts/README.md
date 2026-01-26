# Guardia Prompts

This folder contains prompts for AI assistants to analyze and transform codebases. Each prompt is designed to be run independently or as part of a comprehensive analysis.

## Governance Document Prompts

These prompts generate the foundational governance documents for AI agent collaboration.

| Prompt | Output | Purpose |
|--------|--------|---------|
| [product-purpose.md](./product-purpose.md) | `product-purpose.md` | Define what the product does, who it's for, and why it exists |
| [constraints.md](./constraints.md) | `constraints.md` | Identify things that should NEVER happen |
| [invariants.md](./invariants.md) | `invariants.md` | Identify things that must ALWAYS be true |
| [system.md](./system.md) | `system.md` | Design the AI agent operating system |
| [process.md](./process.md) | `process.md` | Define the development workflow |
| [enforcement.md](./enforcement.md) | `enforcement.md` | Design automated validation |
| [learning-loop.md](./learning-loop.md) | `learning-loop.md` | Design continuous improvement |
| [combined-analysis.md](./combined-analysis.md) | All documents + `GAPS.md` | Run complete analysis in one pass |

### Recommended Order

**For new codebases**, run in this order:
1. `product-purpose.md` - Establish what you're building
2. `constraints.md` - Define the guardrails
3. `invariants.md` - Define the requirements
4. `process.md` - Define how work flows
5. `enforcement.md` - Automate the rules
6. `system.md` - Design agent coordination
7. `learning-loop.md` - Set up improvement cycles

**For quick setup**, use `combined-analysis.md` to generate everything at once.

---

## Codebase Transformation Prompts

These prompts help restructure, document, or visualize codebases.

| Prompt | Purpose |
|--------|---------|
| [domain-driven-restructure.md](./domain-driven-restructure.md) | Transform a technically-layered codebase into a domain-driven product structure |
| [domain-readme-generator.md](./domain-readme-generator.md) | Generate README.md index files for each domain folder |
| [codebase-structure-diagram.md](./codebase-structure-diagram.md) | Generate a text-based visual overview of the entire codebase structure |

### Recommended Sequence

For a full transformation from technical layers to documented domain structure:

1. `domain-driven-restructure.md` - Reorganize code into domain folders
2. `codebase-structure-diagram.md` - Generate visual overview of the new structure
3. `domain-readme-generator.md` - Generate READMEs as navigation index per domain

All three prompts also work standalone on any existing codebase structure.

---

## Usage

### Prerequisites

Before running any prompt:

1. Have the AI agent explore your codebase structure
2. Share key files: README, package.json/requirements.txt, main config files
3. Share any existing documentation or architecture decisions

### Running a Prompt

1. Open a conversation with an AI assistant (Claude Code, Cursor, etc.)
2. Point the assistant to your codebase
3. Copy the prompt content and paste it into the conversation
4. Follow the checkpoints and provide approvals when asked

### Tips for Best Results

1. **Share context** - Give the AI access to your actual codebase, not just descriptions
2. **Be honest about problems** - The goal is to surface weaknesses, not hide them
3. **Iterate** - Run prompts multiple times, refining based on results
4. **Verify claims** - Check that examples cited actually exist in your code
5. **Start small** - Begin with Product Purpose and Constraints, add others over time

---

## Contributing

To add a new prompt:

1. Create a new `.md` file in this folder
2. Follow the existing format:
   - Header with purpose and output
   - Analysis steps with clear instructions
   - Output format specification
   - Checkpoint gates where appropriate
3. Add the prompt to this README's index table
