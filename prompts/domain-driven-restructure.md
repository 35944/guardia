# Domain-Driven Codebase Restructuring Prompt

> **Purpose**: Transform a technically-layered codebase into a domain-driven product structure.
> **Target**: AI Assistant (Claude Code, Cursor, etc.)
> **Mode**: Analyze → Propose → Execute with gated approval at each phase

---

## Instructions for AI Assistant

You are tasked with restructuring a codebase from a **technical layer organization** (e.g., `/components`, `/services`, `/models`, `/utils`) to a **domain-driven product structure** (e.g., `/domains/authentication`, `/domains/billing`, `/domains/inventory`).

Execute this in **four phases**, waiting for explicit user approval before proceeding to the next phase.

---

## Phase 1: Discovery & Domain Identification

### Step 1.1: Understand the Current Structure

Analyze the codebase to understand its current organization:

1. **Map the folder structure** - List all top-level and second-level directories
2. **Identify technical layers** - Find patterns like:
   - `/components`, `/pages`, `/views` (UI layer)
   - `/services`, `/api`, `/controllers` (Service layer)
   - `/models`, `/entities`, `/types`, `/schemas` (Data layer)
   - `/utils`, `/helpers`, `/lib` (Utilities)
   - `/hooks`, `/store`, `/state` (State management)
3. **Count and categorize files** - How many files exist in each layer?
4. **Identify entry points** - Routes, pages, or main features that indicate product domains

### Step 1.2: Gather Domain Knowledge (Priority Order)

Build domain understanding using this hierarchy (higher priority overrides lower, but all sources inform the complete picture):

**Priority 1: User-Defined Domains**
Ask the user:
```
What are the core product domains/features in this application?

Examples of domains:
- Authentication (login, signup, password reset)
- User Management (profiles, settings, permissions)
- Billing (subscriptions, payments, invoices)
- Dashboard (analytics, reporting, widgets)

Please list your domains, or type "skip" to infer from documentation/code.
```

**Priority 2: Documentation-Inferred Domains**
If user skips or to supplement user input, scan:
- `README.md`, `CONTRIBUTING.md`
- `/docs` folder
- API documentation
- Route definitions
- Any product specification files

**Priority 3: Code-Inferred Domains**
Analyze code patterns:
- Group related files by naming patterns (e.g., `UserService`, `UserModel`, `UserCard` → User domain)
- Identify clusters from imports (files that heavily import each other likely belong together)
- Extract domains from route/page structure
- Look for existing domain hints in folder names

### Step 1.3: Reconcile & Report Mismatches

Create a reconciliation report:

```markdown
## Domain Discovery Report

### Identified Domains
| Domain | Source | Confidence | Key Files |
|--------|--------|------------|-----------|
| [name] | user/docs/code | high/medium/low | [files] |

### Mismatches & Conflicts
- ⚠️ User defined "Payments" but code suggests "Billing" - recommend: [suggestion]
- ⚠️ Documentation mentions "Analytics" but no corresponding code found
- ⚠️ Code contains "notifications" cluster not mentioned by user

### Shared/Cross-Cutting Concerns Identified
- Logging utilities
- API client
- Common UI components (Button, Modal, etc.)
- Authentication middleware
- Error handling
```

**CHECKPOINT 1**: Present this report and ask:
```
Please review the Domain Discovery Report above.

1. Are the identified domains correct? (Add/remove/rename any)
2. How should the mismatches be resolved?
3. Is the shared/cross-cutting list accurate?

Reply with your adjustments, or "approved" to proceed to Phase 2.
```

---

## Phase 2: Structure Proposal

### Step 2.1: Design the Target Structure

Based on approved domains, propose a new folder structure:

```
/src (or existing root)
├── /domains
│   ├── /[domain-name]
│   │   ├── /components      # UI components specific to this domain
│   │   ├── /hooks           # React hooks (if applicable)
│   │   ├── /services        # API calls, business logic
│   │   ├── /types           # TypeScript types/interfaces
│   │   ├── /utils           # Domain-specific utilities
│   │   ├── /store           # State management (if applicable)
│   │   ├── /tests           # Domain tests
│   │   └── index.ts         # Public API - what this domain exports
│   │
│   ├── /authentication
│   ├── /user-management
│   ├── /billing
│   └── /...
│
├── /shared
│   ├── /components          # Reusable UI (Button, Modal, etc.)
│   ├── /hooks               # Generic hooks (useDebounce, etc.)
│   ├── /services            # Shared services (API client, logger)
│   ├── /types               # Global types
│   ├── /utils               # Generic utilities
│   ├── /constants           # App-wide constants
│   └── /styles              # Global styles, themes
│
├── /app                     # App shell, routing, providers
│   ├── /routes              # Route definitions
│   ├── /layouts             # Layout components
│   └── /providers           # Context providers
│
└── /config                  # Configuration files
```

### Step 2.2: Create the Migration Mapping

Generate a detailed mapping document:

```markdown
## Migration Mapping

### Domain: Authentication
| Current Path | New Path | Action |
|-------------|----------|--------|
| /components/LoginForm.tsx | /domains/authentication/components/LoginForm.tsx | move |
| /services/authService.ts | /domains/authentication/services/authService.ts | move |
| /hooks/useAuth.ts | /domains/authentication/hooks/useAuth.ts | move |
| /types/auth.ts | /domains/authentication/types/index.ts | move & merge |

### Domain: [Next Domain]
...

### Shared
| Current Path | New Path | Reason for Shared |
|-------------|----------|-------------------|
| /components/Button.tsx | /shared/components/Button.tsx | Used by 5+ domains |
| /utils/formatDate.ts | /shared/utils/formatDate.ts | Generic utility |

### Files Requiring Manual Review
| File | Issue |
|------|-------|
| /services/mixedService.ts | Contains logic for both Auth and User domains - needs splitting |
```

### Step 2.3: Visualize the Change

Create a before/after comparison:

```
BEFORE (Technical Layers)          AFTER (Domain-Driven)
========================          =====================
/src                              /src
├── /components                   ├── /domains
│   ├── LoginForm.tsx            │   ├── /authentication
│   ├── UserProfile.tsx          │   │   ├── /components
│   ├── BillingCard.tsx          │   │   │   └── LoginForm.tsx
│   └── Button.tsx               │   │   └── ...
├── /services                     │   ├── /user-management
│   ├── authService.ts           │   │   ├── /components
│   ├── userService.ts           │   │   │   └── UserProfile.tsx
│   └── billingService.ts        │   │   └── ...
├── /hooks                        │   └── /billing
│   ├── useAuth.ts               │       └── ...
│   └── useUser.ts               ├── /shared
└── /utils                        │   ├── /components
    └── formatDate.ts            │   │   └── Button.tsx
                                  │   └── /utils
                                  │       └── formatDate.ts
                                  └── /app
```

**CHECKPOINT 2**: Present the structure proposal and ask:
```
Please review the proposed structure and migration mapping.

1. Does the folder structure work for your project?
2. Are files correctly categorized into domains vs shared?
3. Any files that need different placement?

Reply with adjustments, or "approved" to proceed to Phase 3.
```

---

## Phase 3: Migration Strategy Selection

### Step 3.1: Present Migration Options

```
How would you like to execute this migration?

**Option A: Clean Cutover**
- All files moved at once
- All imports updated in a single operation
- Pros: Clean result, no temporary complexity
- Cons: Large changeset, harder to review
- Best for: Smaller codebases, strong test coverage

**Option B: Gradual Migration with Aliases**
- Create new structure alongside old
- Add path aliases for backward compatibility
- Migrate domain-by-domain
- Remove aliases once complete
- Pros: Incremental, easier to review, lower risk
- Cons: Temporary complexity, longer process
- Best for: Large codebases, limited test coverage

**Option C: Gradual Migration with Re-exports**
- Move files to new locations
- Leave re-export stubs in old locations
- Remove stubs domain-by-domain after verification
- Pros: No import changes needed initially
- Cons: Temporary duplication, cleanup required

Please choose A, B, or C.
```

### Step 3.2: Confirm Rollback Strategy

```
Before proceeding, confirm your rollback strategy:

Recommended: Ensure you have one of the following:
- [ ] Git: All changes committed, can `git reset --hard`
- [ ] Branch: Working on a feature branch
- [ ] Backup: Manual backup of source directory

Type "rollback confirmed" to proceed, or describe your rollback plan.
```

**CHECKPOINT 3**: Wait for migration strategy selection and rollback confirmation.

---

## Phase 4: Execution

### Step 4.1: Pre-flight Checks

Before making changes:
1. Verify the codebase builds/compiles successfully
2. Run existing tests (if available) to establish baseline
3. Create a git commit or backup point

Report status:
```
Pre-flight Check Results:
- Build status: ✅ passing / ❌ failing (fix before proceeding)
- Test status: ✅ X tests passing / ⚠️ no tests / ❌ Y tests failing
- Git status: ✅ clean / ⚠️ uncommitted changes

[If issues] Resolve the above before proceeding.
[If clean] Ready to execute. Proceed? (yes/no)
```

### Step 4.2: Execute Migration

Based on selected strategy, execute:

**For Clean Cutover (Option A):**
1. Create new folder structure
2. Move all files according to mapping
3. Update all import statements
4. Remove empty old directories
5. Verify build passes
6. Run tests

**For Gradual Migration (Options B/C):**
1. Create new folder structure
2. Set up aliases or re-exports
3. Migrate first domain (lowest dependency count)
4. Verify build and tests
5. Report status, ask to continue to next domain
6. Repeat for each domain
7. Final cleanup of aliases/stubs

### Step 4.3: Post-Migration Verification

After execution:
```
Migration Complete!

## Summary
- Files moved: X
- Imports updated: Y
- New domains created: Z

## Verification
- Build status: ✅/❌
- Tests status: ✅/❌
- Import errors: [list any]

## New Structure
[Display final folder tree]

## Next Steps
1. Review the changes: `git diff --stat`
2. Run your full test suite
3. Manual smoke test of key features
4. Commit when satisfied: `git commit -m "refactor: reorganize to domain-driven structure"`

## If Issues Arise
- Rollback: `git reset --hard HEAD~1` (or restore from backup)
- Report specific errors for targeted fixes
```

---

## Handling Edge Cases

### Circular Dependencies
If detected during analysis:
```
⚠️ Circular dependency detected:
- /domains/auth imports from /domains/user
- /domains/user imports from /domains/auth

Recommended resolution:
1. Extract shared types to /shared/types
2. Create a /domains/identity domain combining both
3. Use dependency injection pattern

Which approach do you prefer?
```

### Ambiguous File Placement
When a file could belong to multiple domains:
```
File: UserPaymentHistory.tsx
Could belong to: User Management OR Billing

Indicators:
- Name suggests: User (primary), Billing (secondary)
- Imports from: 60% billing services, 40% user services
- Used by: Billing pages only

Recommendation: Place in /domains/billing with clear naming
Your preference?
```

### Large Files Needing Splitting
```
File: monolithicService.ts (500+ lines)
Contains logic for: Authentication, User Management, Billing

Recommendation: Split into domain-specific services
- Extract auth logic → /domains/authentication/services/authService.ts
- Extract user logic → /domains/user-management/services/userService.ts
- Extract billing logic → /domains/billing/services/billingService.ts

Proceed with split? (yes/no/manual)
```

---

## Shared vs Domain Decision Framework

A file belongs in `/shared` when:
- Used by **3+ domains** with no primary owner
- Is a **generic utility** (date formatting, string manipulation)
- Is a **UI primitive** (Button, Input, Modal)
- Is **infrastructure** (API client, logger, error handler)
- Has **no domain-specific business logic**

A file belongs in a **domain** when:
- Contains **business logic specific** to that domain
- Is **primarily used** by that domain (even if occasionally used elsewhere)
- Would need to **change when that domain's requirements change**
- Is **named after** domain concepts

When in doubt: **Start in the domain, promote to shared later if needed.**

---

## Naming Conventions

### Domain Folders
- Use **kebab-case**: `user-management`, `order-processing`
- Use **product language**, not technical terms
- Be **specific**: `authentication` not `auth`, `user-profile` not `users`

### File Names
- Preserve existing project conventions
- Suggest improvements only if inconsistent

### Index Files (Public API)
Each domain should export its public API:
```typescript
// domains/authentication/index.ts
export { LoginForm } from './components/LoginForm';
export { useAuth } from './hooks/useAuth';
export { authService } from './services/authService';
export type { User, AuthState } from './types';
```

---

## Customization Points

Before starting, you may specify:
- **Framework-specific patterns** (Next.js app router, Remix routes, etc.)
- **Monorepo considerations** (packages vs apps)
- **Existing conventions** to preserve
- **Domains to exclude** from restructuring
- **Custom shared categories** beyond the defaults

---

*End of prompt. Begin by asking the user to point you to the codebase root directory.*
