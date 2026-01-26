# Codebase Structure Diagram Prompt

> **Purpose**: Generate a text-based visual overview of an entire codebase structure as a markdown file.
> **Output**: `codebase-structure-diagram.md`

---

## Instructions for AI Assistant

You are tasked with generating a comprehensive codebase structure diagram that serves as a visual reference for understanding how the codebase is organized. The diagram should **reflect reality** - documenting what actually exists, not what should exist.

Execute this in **three phases**.

---

## Phase 1: Codebase Discovery

### Step 1.1: Identify the Root

Find the application root:
1. Look for entry points (`main.py`, `app.py`, `index.ts`, `main.go`, `App.java`, etc.)
2. Look for package manifests (`package.json`, `pyproject.toml`, `go.mod`, `Cargo.toml`, `pom.xml`)
3. Identify the primary source directory (`src/`, `app/`, `lib/`, or root-level code)

### Step 1.2: Detect Application Layers

Scan the codebase to identify which layers exist:

**Backend indicators:**
- Server frameworks (FastAPI, Express, Spring, Gin, etc.)
- API routes, controllers, handlers
- Database models, ORM files
- Server-side services

**Frontend indicators:**
- UI frameworks (React, Vue, Angular, Svelte)
- Components, views, pages folders
- Client-side JavaScript/TypeScript
- Static assets, stylesheets

**Possible structures:**
- Backend only
- Frontend only
- Full-stack (separate frontend/backend)
- Full-stack (integrated, e.g., Next.js, Django templates)
- Library/SDK (no frontend/backend split)

### Step 1.3: Identify Organizational Pattern

Determine how code is organized:

**Domain-driven:**
- `domains/`, `features/`, `modules/` folders
- Business capability groupings (auth, users, billing)

**Technical layers:**
- `controllers/`, `services/`, `models/`, `utils/`
- Horizontal slicing by technical concern

**Hybrid:**
- Mix of domain and technical organization

**Flat:**
- All files in root or single level

Note the pattern detected - it affects how you present the structure.

---

## Phase 2: Structure Mapping

### Step 2.1: Map Top-Level Structure

Create a high-level map of the codebase:

```
project-root/
├── [source directory]/     # Main application code
├── [tests]/                # Test files (if separate)
├── [config]/               # Configuration files
├── [docs]/                 # Documentation (if exists)
└── [other significant dirs]
```

### Step 2.2: Map Each Major Section

For each significant directory, create a detailed tree structure.

**Depth guidelines:**
- Show 3-4 levels deep for important directories
- Show 2 levels for less critical directories
- Use `...` or `└── ...` to indicate more files exist

**File inclusion guidelines (AI discretion):**

*Always show:*
- Entry points and main files
- Model/entity definitions
- Route/controller files
- Service files
- Configuration files
- Key business logic files

*Show selectively:*
- Utility files (show if few, summarize if many)
- Test files (show structure, not every test)
- Generated files (mention existence, don't enumerate)

*Abbreviate when:*
- More than 10 similar files in a folder
- Auto-generated or boilerplate files
- Third-party or vendor code

**Inline descriptions:**

Add brief descriptions after files/folders that aren't self-explanatory:

```
├── auth/                    # User authentication and sessions
│   ├── router.py            # OAuth and session endpoints
│   ├── models.py            # User, Session, Token models
│   └── services/
│       └── token_service.py # JWT generation and validation
```

Skip descriptions for obvious names:
```
├── utils/
│   ├── date.py
│   ├── string.py
│   └── validation.py
```

### Step 2.3: Identify Cross-Cutting Concerns

Look for and document:

**Shared/Common code:**
- `shared/`, `common/`, `lib/`, `utils/`
- Code used across multiple parts of the application

**Infrastructure/Core:**
- `core/`, `infrastructure/`, `config/`
- Database setup, logging, middleware, DI

**Note dependencies between sections** for the overview.

---

## Phase 3: Generate Diagram

### Step 3.1: Create the Document

Generate a markdown file with this structure:

```markdown
# Codebase Structure Diagram

**Last Updated**: [current date]
**Status**: Active Reference
**Purpose**: Visual reference guide for codebase structure

## Overview

[2-3 sentences describing:
- What this codebase is (infer from README or code)
- How it's organized (domain-driven, layered, etc.)
- Key architectural patterns observed]

**When to use this diagram:**
- Understanding where code lives
- Deciding where to add new code
- Onboarding to the codebase
- Code review reference

## [Section 1: e.g., "Backend Structure" or "Source Structure"]

### [Subsection: e.g., "Domains" or "Features"]

[Brief description of what this section contains]

```
[tree structure]
```

### [Subsection: e.g., "Shared Services"]

[Brief description]

```
[tree structure]
```

### [Subsection: e.g., "Core Infrastructure"]

[Brief description]

```
[tree structure]
```

## [Section 2: e.g., "Frontend Structure" - if applicable]

[Same pattern as above]

## Maintenance

**When to update this diagram:**
- New major section/domain added
- Significant structural reorganization
- Key files moved or renamed

**Update process:**
1. Make structural changes to codebase
2. Update diagram to reflect changes
3. Update "Last Updated" date

## Version History

- **[current date]**: Initial diagram created
```

### Step 3.2: Adapt to Detected Structure

**For domain-driven codebases:**
```markdown
## Backend Structure

### Domains

Business logic organized by domain:

```
app/domains/
├── authentication/     # User auth, OAuth, sessions
├── billing/            # Payments, subscriptions
└── ...
```

### Shared Services

Cross-domain services:

```
app/shared/
├── ai/                 # AI/ML services
└── ...
```

### Core Infrastructure

Technical infrastructure:

```
app/core/
├── database.py
└── ...
```
```

**For technically-layered codebases:**
```markdown
## Application Structure

### Controllers

HTTP request handlers:

```
src/controllers/
├── auth_controller.py
├── user_controller.py
└── ...
```

### Services

Business logic:

```
src/services/
├── auth_service.py
└── ...
```

### Models

Data structures:

```
src/models/
├── user.py
└── ...
```
```

**For frontend-only (e.g., React app):**
```markdown
## Application Structure

### Pages/Routes

```
src/pages/
├── Home/
├── Dashboard/
└── ...
```

### Components

```
src/components/
├── common/
├── forms/
└── ...
```

### State Management

```
src/store/
├── slices/
└── ...
```

### Services/API

```
src/services/
├── api.ts
└── ...
```
```

**For library/SDK:**
```markdown
## Library Structure

### Public API

Exported modules:

```
src/
├── index.ts           # Main entry point
├── client.ts          # Primary client class
└── ...
```

### Internal

Implementation details:

```
src/internal/
├── ...
```
```

### Step 3.3: Write the File

Write the generated diagram to:
- `docs/architecture/codebase-structure-diagram.md` (if `docs/` exists)
- `docs/codebase-structure-diagram.md` (if no architecture folder)
- `CODEBASE-STRUCTURE.md` at root (if no docs folder)

Ask user for preferred location if unclear.

---

## Output Considerations

### Tree Formatting

Use standard tree characters:
```
├── file.py          # Not last item in directory
└── last-file.py     # Last item in directory
│                    # Vertical connector for nested items
    └── nested.py    # Indentation (4 spaces per level)
```

### Section Descriptions

Keep descriptions brief and factual:

✅ Good:
```
### Domains

Business logic organized by domain (bounded context):
```

❌ Too verbose:
```
### Domains

This section contains all the business domains which are organized according to
domain-driven design principles where each domain represents a bounded context
that encapsulates related business logic and data models together.
```

### Handling Large Codebases

For codebases with many files:

1. **Prioritize important directories** - Show more detail for core business logic
2. **Summarize utilities** - `├── utils/  # 15 utility modules`
3. **Group similar files** - `├── *_controller.py  # 12 controller files`
4. **Use continuation markers** - `└── ...  # 8 more files`

### Handling Messy Codebases

If the codebase is disorganized:

1. **Document what exists** - Don't pretend it's cleaner than it is
2. **Note inconsistencies** - "Mixed organization patterns observed"
3. **Identify outliers** - Files in unexpected locations
4. **Stay neutral** - Describe, don't judge

---

## Example Output

```markdown
# Codebase Structure Diagram

**Last Updated**: 2025-01-26
**Status**: Active Reference
**Purpose**: Visual reference guide for codebase structure

## Overview

TaskFlow is a project management API built with FastAPI. The codebase uses domain-driven design with clear separation between business domains, shared services, and core infrastructure.

**When to use this diagram:**
- Understanding where code lives
- Deciding where to add new code
- Onboarding to the codebase
- Code review reference

## Backend Structure

### Domains

Business logic organized by domain:

```
app/domains/
├── projects/                # Project management
│   ├── router.py            # CRUD endpoints
│   ├── service.py           # Business logic
│   └── models.py            # Project, ProjectMember models
│
├── tasks/                   # Task management
│   ├── router.py
│   ├── models.py            # Task, TaskComment, TaskLabel
│   └── services/
│       ├── task_service.py
│       └── assignment_service.py
│
└── users/                   # User management
    ├── router.py
    ├── service.py
    └── models.py
```

### Shared Services

Cross-domain services used by multiple domains:

```
app/shared/
├── notifications/           # Email and push notifications
│   ├── email_service.py
│   └── push_service.py
│
└── search/                  # Full-text search
    └── search_service.py
```

### Core Infrastructure

Technical infrastructure:

```
app/core/
├── database.py              # SQLAlchemy setup
├── config.py                # Environment configuration
├── exceptions.py            # Custom exception classes
└── middleware/
    ├── auth.py              # JWT validation
    └── logging.py           # Request logging
```

## Maintenance

**When to update this diagram:**
- New domain added
- Shared service category added
- Core infrastructure component added
- Significant structural changes

**Update process:**
1. Make structural changes to codebase
2. Update diagram to reflect changes
3. Update "Last Updated" date

## Version History

- **2025-01-26**: Initial diagram created
```

---

*Begin by asking the user to confirm the codebase root path, or let them specify if auto-detection should proceed.*
