# {{PROJECT_NAME}} Invariants

These are architectural requirements the system must maintain at all times. They are not preferences. AI agents expanding the product must preserve these invariants.

## Layer Architecture

### {{LAYER_INVARIANT_NAME}}

{{LAYER_INVARIANT_DESCRIPTION}}

```
┌─────────────────┐
│   {{LAYER_1}}   │  ← {{LAYER_1_RESPONSIBILITY}}
└────────┬────────┘
         │ {{RELATIONSHIP_1_2}}
┌────────▼────────┐
│   {{LAYER_2}}   │  ← {{LAYER_2_RESPONSIBILITY}}
└────────┬────────┘
         │ {{RELATIONSHIP_2_3}}
┌────────▼────────┐
│   {{LAYER_3}}   │  ← {{LAYER_3_RESPONSIBILITY}}
└─────────────────┘
```

### Import/Dependency Rules

**Allowed:**
- {{ALLOWED_DEPENDENCY_1}}
- {{ALLOWED_DEPENDENCY_2}}
- {{ALLOWED_DEPENDENCY_3}}

**Forbidden:**
- {{FORBIDDEN_DEPENDENCY_1}}
- {{FORBIDDEN_DEPENDENCY_2}}

## Dependency Injection

### {{DI_INVARIANT_NAME}}

{{DI_INVARIANT_DESCRIPTION}}

```{{LANGUAGE}}
{{DI_EXAMPLE}}
```

## Error Handling

### {{ERROR_INVARIANT_NAME}}

{{ERROR_INVARIANT_DESCRIPTION}}

```{{LANGUAGE}}
{{ERROR_HANDLING_EXAMPLE}}
```

### Standardized Error Response Format

All API errors return this structure:

```json
{
  {{ERROR_RESPONSE_SCHEMA}}
}
```

## Code Size Limits

### {{SIZE_LIMIT_FILE}} Lines Per File

Files exceeding {{SIZE_LIMIT_FILE}} lines must be split by responsibility. {{SIZE_LIMIT_FILE_EXCEPTIONS}}

### {{SIZE_LIMIT_FUNCTION}} Lines Per Function

Functions exceeding {{SIZE_LIMIT_FUNCTION}} lines must be decomposed into smaller, focused functions.

### {{SIZE_LIMIT_NESTING}} Levels of Nesting Maximum

Deep nesting is avoided via guard clauses and early returns.

```{{LANGUAGE}}
# Preferred: guard clauses
{{GUARD_CLAUSE_EXAMPLE}}

# Avoided: deep nesting
{{DEEP_NESTING_EXAMPLE}}
```

## {{TECH_SPECIFIC_SECTION_1_NAME}}

### {{TECH_INVARIANT_1_NAME}}

{{TECH_INVARIANT_1_DESCRIPTION}}

```{{LANGUAGE}}
{{TECH_INVARIANT_1_EXAMPLE}}
```

## {{TECH_SPECIFIC_SECTION_2_NAME}}

### {{TECH_INVARIANT_2_NAME}}

{{TECH_INVARIANT_2_DESCRIPTION}}

## Testing

### {{TESTING_INVARIANT_NAME}}

{{TESTING_INVARIANT_DESCRIPTION}}

## Pre-Commit Enforcement

### All Commits Pass Quality Gates

Pre-commit hooks enforce:

{{#PRE_COMMIT_HOOKS}}
- {{HOOK_NAME}} ({{HOOK_PURPOSE}})
{{/PRE_COMMIT_HOOKS}}

Commits that fail these checks do not proceed.

---

## Template Instructions

### How to Identify Invariants

Invariants answer: "What must ALWAYS be true in this codebase?"

**Sources to mine for invariants:**
1. Architecture documentation (what patterns are mandated?)
2. Style guides (what's required, not just preferred?)
3. Framework conventions (what does the framework expect?)
4. Pre-commit hooks (what's already enforced?)
5. CI/CD checks (what blocks merges?)

### Difference Between Constraints and Invariants

| Constraints | Invariants |
|-------------|------------|
| What we never do | What we always do |
| Prohibitions | Requirements |
| "Never use X" | "Always use Y" |
| Negative rules | Positive rules |

### Common Invariant Categories

| Category | Example Invariants |
|----------|-------------------|
| **Layer Architecture** | Controllers call services, services call repositories |
| **Dependency Injection** | Dependencies injected, never instantiated |
| **Error Handling** | All errors through ErrorFactory, standardized format |
| **Size Limits** | Max 300 lines/file, 30 lines/function |
| **Testing** | All public methods have tests |
| **Typing** | All public APIs have type annotations |
| **Logging** | Structured JSON logging with correlation IDs |

### Tips

- Invariants should be measurable and verifiable
- Start with what your pre-commit hooks already enforce
- Document the "why" - helps agents make good judgment calls
- Include code examples for clarity
- Update when you add new enforcement mechanisms
