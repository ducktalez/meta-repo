# Shared Core vs. Local Extensions

> This document describes the principle of maintaining a shared core data model while allowing project-specific extensions.

## Principle

The meta-repo defines a **shared core** of entities and conventions that all projects should align with. Individual projects are free to **extend** this core with domain-specific models and attributes, but the shared foundation must remain consistent.

```
┌─────────────────────────────────────────────┐
│              Shared Core (meta-repo)        │
│  User, Role, Permission, Organization, Team │
│  Audit fields, naming conventions, ID       │
│  strategy, soft delete pattern              │
├─────────────────────────────────────────────┤
│         Project-Specific Extensions         │
│  Domain entities, custom attributes,        │
│  specialized relationships                  │
└─────────────────────────────────────────────┘
```

## What belongs in the shared core?

Entities and patterns that are common across multiple projects:

| Category              | Examples                                      |
|-----------------------|-----------------------------------------------|
| Identity              | User, authentication, password management     |
| Authorization         | Role, Permission, RBAC structure              |
| Organization          | Organization, Team, Membership                |
| Ownership & Audit     | `created_by`, `updated_by`, `created_at`, ... |
| Technical conventions | ID strategy, naming, soft delete, timestamps  |

## What stays local?

Entities and logic that are specific to a single project's domain:

| Category              | Examples                                      |
|-----------------------|-----------------------------------------------|
| Business entities     | Product, Invoice, Booking, Article, etc.      |
| Domain-specific logic | Pricing rules, scoring algorithms, workflows  |
| Experimental models   | Prototypes, POC-only structures               |
| Integration-specific  | Third-party API mappings, sync tables         |

## Rules

1. **Do not diverge from the core without documentation.** If a project changes a core entity (e.g., renames `email` to `mail`), it must be documented as a deviation.

2. **Extend, don't replace.** Add columns or related tables rather than modifying core columns.

3. **Propose upstream improvements.** If a local extension proves valuable across projects, propose adding it to the shared core via a pull request to the meta-repo.

4. **Keep the core minimal.** Only add to the shared core what is genuinely shared. Resist the urge to centralize everything.

5. **Version awareness.** When the shared core evolves, sub-repos should evaluate and adopt changes. The meta-repo catalog tracks each repo's alignment status.

## Example: Extending the User Entity

The shared core defines `users` with standard fields. A project that needs a `bio` and `avatar_url` simply adds them:

```
users (core)            users (project-specific)
─────────────           ─────────────────────────
id                      id
email                   email
username                username
first_name              first_name
last_name               last_name
is_active               is_active
...                     ...
                        bio          ← extension
                        avatar_url   ← extension
```

The core columns remain unchanged. The extension is documented in the project's Architecture.md.

## Phased Adoption

Not all projects need to adopt the full shared core immediately. The recommended path:

1. **Awareness** — project documents its current model vs. the shared core
2. **Alignment** — project adopts naming conventions and audit fields
3. **Adoption** — project migrates to the shared core entity structure
4. **Integration** — project connects to shared identity services (future)

