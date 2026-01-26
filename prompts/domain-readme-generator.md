# Domain README Generator Prompt

> **Purpose**: Generate README.md files for each domain in a domain-driven folder structure, serving as an index for AI assistants to quickly navigate the codebase.
> **Output**: One `README.md` per domain folder

---

## Instructions for AI Assistant

You are tasked with generating README files for each domain in a domain-driven codebase. These READMEs serve as an **index of reality** - they document what actually exists in the code, helping AI assistants quickly understand and navigate each domain.

Execute this in **three phases**.

---

## Phase 1: Structure Analysis

### Step 1.1: Locate the Domains

Find the domains folder structure:

1. Search for a `domains/` folder (common locations: `src/domains/`, `app/domains/`, `lib/domains/`)
2. If not found, search for domain-like folder patterns (feature folders with services, models, routers/controllers)
3. List all domain folders found

### Step 1.2: Identify the Tech Stack

Determine the technology to adapt analysis patterns:

1. Check for `package.json` (Node.js/TypeScript)
2. Check for `requirements.txt`, `pyproject.toml`, `setup.py` (Python)
3. Check for `go.mod` (Go)
4. Check for `Cargo.toml` (Rust)
5. Check for `pom.xml`, `build.gradle` (Java/Kotlin)

Note the framework if detectable (FastAPI, Express, NestJS, Spring, etc.)

### Step 1.3: Map the Structure

For each domain, list:
- All files and subdirectories
- File sizes (to detect potential debt)
- File types (models, services, routers/controllers, types, utils, tests)

Report:
```
Domains Found: X

1. [domain-name]/
   - files: N
   - subdirs: [list]
   - detected patterns: [models, services, routes, etc.]

2. [domain-name]/
   ...
```

---

## Phase 2: Domain Analysis

For each domain, analyze and extract:

### 2.1: Purpose

Infer purpose from:
- Folder name
- File names and class/function names
- Comments at top of main files
- README if one already exists (to update, not replace blindly)

Write 1-2 sentences describing what this domain does.

### 2.2: Entities (Models/Types)

Search for:
- **Python**: Classes inheriting from ORM base (SQLAlchemy, Django, Pydantic), files named `models.py`, `entities.py`, `schemas.py`
- **TypeScript/JS**: Interfaces, types, classes in `models/`, `entities/`, `types/` folders or files
- **Go**: Structs in `models.go`, `types.go`, or `entity.go`
- **Java/Kotlin**: Classes annotated with `@Entity`, `@Table`, or in `model/`, `entity/` packages

For each entity found, extract:
- Name
- Brief description (from docstring/comment or infer from fields)
- Key fields (primary key, foreign keys, important business fields)

If no entities found, note: "No own models. Operates on: [what it uses, if detectable]"

Format as table:
```markdown
| Model | Description | Key Fields |
|-------|-------------|------------|
| User  | Core user account | id, email, created_at |
```

### 2.3: Public API

Search for:
- **Python FastAPI**: `@router.get`, `@router.post`, etc. decorators
- **Python Django**: `urlpatterns` in `urls.py`
- **Express/NestJS**: `@Get`, `@Post` decorators or `router.get()`, `router.post()` calls
- **Go**: Handler functions registered to routes
- **Spring**: `@GetMapping`, `@PostMapping`, etc.

For each endpoint found, extract:
- HTTP method
- Path/endpoint
- Brief description (from docstring or function name)

If no API endpoints, note: "No public API. Internal domain only."

Format as table:
```markdown
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET    | `/users` | List all users |
| POST   | `/users` | Create new user |
```

### 2.4: Services

Search for:
- Files named `service.py`, `services.py`, `*_service.py`, `*Service.ts`, etc.
- Classes with "Service" suffix
- Folders named `services/`

For each service found, extract:
- Name
- Responsibility (from docstring, class comment, or infer from methods)

If no services, note: "No dedicated service layer." and explain where logic lives (e.g., "Logic lives in router/controller").

Format as table:
```markdown
| Service | Responsibility |
|---------|----------------|
| UserService | User CRUD, authentication, profile management |
```

### 2.5: Dependencies

Analyze imports to categorize:

- **Shared**: Imports from `shared/`, `common/`, `lib/` (cross-domain utilities)
- **Core**: Imports from `core/`, `infrastructure/`, `config/` (technical infrastructure)
- **Cross-domain**: Direct imports from other domain folders (potential violations)
- **External**: Third-party libraries critical to this domain (Redis, S3, Stripe, etc.)

Format as bullet list:
```markdown
- **Shared**: `shared/auth`, `shared/events`
- **Core**: `core.database`, `core.exceptions`
- **Cross-domain**: `users.models.User` (note: potential violation)
- **External**: Redis (for caching)
```

### 2.6: Domain Rules

Extract implicit rules from:
- Constants and configuration (limits, allowed values)
- Validation logic (required fields, formats, ranges)
- Business logic patterns (state machines, workflows)
- Comments mentioning "must", "always", "never", "required"

Format as bullet list:
```markdown
- Sessions expire after 24 hours
- Email must be unique per tenant
- Passwords require minimum 8 characters
```

If no clear rules detected, note: "No explicit domain rules detected."

### 2.7: File Map

Create a tree structure with inline descriptions:

```markdown
## File Map

```
domain-name/
  models.py          # User, Session ORM models
  router.py          # CRUD endpoints with auth
  service.py         # UserService (business logic)
  services/
    email_service.py # Email notification handling
  utils.py           # Domain-specific helpers
```
```

### 2.8: Known Debt

Automatically detect:
- **File size**: Files exceeding 300 lines (configurable threshold)
- **Function size**: Functions exceeding 50 lines
- **Cross-domain imports**: Direct imports from other domains
- **Missing tests**: No corresponding test files
- **TODO/FIXME/HACK comments**: Count and summarize
- **Type coverage**: Missing type annotations on public functions (if typed language)

Format as bullet list:
```markdown
- `service.py` exceeds 300 lines (425 lines)
- Direct import from `orders` domain in `router.py:15`
- No test coverage found
- 3 TODO comments (authentication refactor, caching, error handling)
```

If no significant debt detected, note: "None significant."

---

## Phase 3: Generate READMEs

### Step 3.1: Generate All READMEs

For each domain, create a README.md with this exact structure:

```markdown
# Domain: [Name]

## Purpose

[1-2 sentences describing what this domain does]

## Entities

[Table of models/types, or note if none]

## Public API

[Table of endpoints, or note if none]

## Services

[Table of services, or note if none]

## Dependencies

[Categorized bullet list]

## Domain Rules

[Bullet list of rules, or note if none detected]

## File Map

```
[tree structure with descriptions]
```

## Known Debt

[Bullet list of detected issues, or "None significant."]
```

### Step 3.2: Write Files

Write each README.md to its respective domain folder:
- `domains/authentication/README.md`
- `domains/users/README.md`
- etc.

### Step 3.3: Summary Report

After generating all READMEs, provide a summary:

```markdown
## Domain README Generation Complete

### Generated
| Domain | Files Analyzed | Entities | Endpoints | Services | Debt Items |
|--------|----------------|----------|-----------|----------|------------|
| auth   | 5              | 3        | 4         | 1        | 2          |
| users  | 8              | 2        | 6         | 2        | 0          |
| ...    | ...            | ...      | ...       | ...      | ...        |

### Cross-Domain Dependencies Detected
- `orders` → `users.models.User` (router.py:15)
- `billing` → `orders.models.Order` (service.py:42)

### High Debt Domains (3+ issues)
- `analytics`: 5 issues (oversized files, missing tests)

### Domains Without Tests
- authentication
- metadata
```

---

## Customization

Before running, you may specify:

- **Line limit threshold**: Default 300, adjust for your codebase standards
- **Domains to skip**: Exclude specific domains from generation
- **Existing README handling**:
  - `overwrite`: Replace existing READMEs entirely
  - `preserve-purpose`: Keep existing Purpose section, regenerate rest
  - `skip`: Don't touch domains with existing READMEs
- **Debt detection strictness**:
  - `strict`: Flag all potential issues
  - `moderate`: Flag clear violations only
  - `minimal`: Only file size and cross-domain imports

---

## Language-Specific Patterns

### Python (FastAPI/Django)

```python
# Models: Look for
class User(Base):  # SQLAlchemy
class User(models.Model):  # Django

# Routes: Look for
@router.get("/users")
@api_view(['GET'])  # Django REST

# Services: Look for
class UserService:
```

### TypeScript/JavaScript (Express/NestJS)

```typescript
// Models: Look for
interface User { }
type User = { }
@Entity() class User { }  // TypeORM

// Routes: Look for
router.get('/users', ...)
@Get('users')  // NestJS

// Services: Look for
@Injectable() class UserService { }
class UserService { }
```

### Go

```go
// Models: Look for
type User struct { }

// Routes: Look for
r.HandleFunc("/users", handler)
e.GET("/users", handler)  // Echo

// Services: Look for
type UserService struct { }
```

---

## Edge Cases

### Domain with Only Types/Interfaces
```markdown
## Entities

| Type | Description | Key Fields |
|------|-------------|------------|
| UserDTO | Data transfer object | id, email, name |

## Services

No services. This domain provides shared type definitions only.
```

### Domain with Only Utilities
```markdown
## Purpose

Provides utility functions for date formatting and validation used across the application.

## Entities

No models. Utility functions only.

## Public API

No API. Internal utilities only.
```

### Domain Acting on Other Domains' Data
```markdown
## Entities

No own models. Operates on JSONB metadata fields in:
- `folders.Folder.folder_metadata`
- `documents.Document.document_metadata`
```

---

*Begin by asking the user to provide the path to their domains folder, or let them confirm auto-detection.*
