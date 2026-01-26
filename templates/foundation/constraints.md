# {{PROJECT_NAME}} Constraints

These constraints are non-negotiable. They define what {{PROJECT_NAME}} will never do. AI agents expanding the product must operate within these boundaries.

## Architecture Constraints

### {{ARCHITECTURE_CONSTRAINT_1_NAME}}

{{ARCHITECTURE_CONSTRAINT_1_DESCRIPTION}}

```{{LANGUAGE}}
# FORBIDDEN
{{FORBIDDEN_PATTERN_1}}

# ALLOWED
{{ALLOWED_PATTERN_1}}
```

### {{ARCHITECTURE_CONSTRAINT_2_NAME}}

{{ARCHITECTURE_CONSTRAINT_2_DESCRIPTION}}

```{{LANGUAGE}}
# FORBIDDEN
{{FORBIDDEN_PATTERN_2}}

# ALLOWED
{{ALLOWED_PATTERN_2}}
```

## Code Quality Constraints

### {{CODE_CONSTRAINT_1_NAME}}

{{CODE_CONSTRAINT_1_DESCRIPTION}}

```{{LANGUAGE}}
# FORBIDDEN
{{FORBIDDEN_CODE_1}}

# ALLOWED
{{ALLOWED_CODE_1}}
```

### {{CODE_CONSTRAINT_2_NAME}}

{{CODE_CONSTRAINT_2_DESCRIPTION}}

## Data Constraints

### {{DATA_CONSTRAINT_1_NAME}}

{{DATA_CONSTRAINT_1_DESCRIPTION}}

### {{DATA_CONSTRAINT_2_NAME}}

{{DATA_CONSTRAINT_2_DESCRIPTION}}

## Security Constraints

### No Secrets in Code

API keys, passwords, tokens, and other secrets are never hardcoded. All secrets come from environment variables.

```{{LANGUAGE}}
# FORBIDDEN
api_key = "sk-abc123..."

# ALLOWED
api_key = {{ENV_VAR_SYNTAX}}
```

### {{SECURITY_CONSTRAINT_2_NAME}}

{{SECURITY_CONSTRAINT_2_DESCRIPTION}}

## Process Constraints

### {{PROCESS_CONSTRAINT_1_NAME}}

{{PROCESS_CONSTRAINT_1_DESCRIPTION}}

### {{PROCESS_CONSTRAINT_2_NAME}}

{{PROCESS_CONSTRAINT_2_DESCRIPTION}}

---

## Template Instructions

### How to Identify Constraints

Constraints answer: "What should this codebase NEVER do?"

**Sources to mine for constraints:**
1. Past incidents (what went wrong?)
2. Code review feedback (what gets rejected?)
3. Architecture decisions (what patterns are banned?)
4. Security requirements (what's prohibited?)
5. Team agreements (what's off-limits?)

### Common Constraint Categories

| Category | Example Constraints |
|----------|---------------------|
| **Architecture** | No circular dependencies, no god classes, no direct DB access from UI |
| **Code Quality** | No bare exceptions, no magic numbers, no commented-out code |
| **Data** | No PII in logs, no hard-coded connection strings, no mutable globals |
| **Security** | No secrets in code, no SQL concatenation, no eval() |
| **Process** | No commits without tests, no direct pushes to main |

### Tips

- Each constraint should have a clear FORBIDDEN/ALLOWED example
- Constraints should be enforceable (can you write a check for it?)
- Start with 5-10 constraints, add more as violations occur
- Link constraints to past incidents where possible
- Make the "why" clear - agents follow rules better when they understand the reason
