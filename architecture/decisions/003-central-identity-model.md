# 3. Central Identity Model

**Date:** 2026-03-18
**Status:** Proposed

## Context

Multiple projects manage their own user, role, and permission models independently. This leads to:

- Duplicated user management logic across projects
- Inconsistent role and permission models
- No single source of truth for identity across the ecosystem
- Difficulty implementing cross-project features (SSO, shared teams, unified dashboards)

Similar to how an ERP system provides a central master data model, our ecosystem would benefit from a shared identity foundation.

## Decision

We will define and adopt a **central identity model** that serves as the shared foundation for user, role, and organization management across all projects.

The central model covers:

- **Users** — core identity attributes shared across projects
- **Roles & Permissions** — standardized RBAC model
- **Organizations & Teams** — multi-tenancy and group structures
- **Ownership & Audit** — who created/modified what, when

This does not mean all projects must share a single database. The model defines:

1. **Standard entity definitions** that projects should align with
2. **Extension points** where projects can add domain-specific attributes
3. **Integration patterns** for projects that need to share identity data

Implementation may evolve from:
- Aligned but independent database tables (phase 1)
- Shared authentication service (phase 2)
- Centralized identity service (phase 3)

See [data-models/identity-concept.md](../../data-models/identity-concept.md) for the detailed concept.

## Consequences

**Easier:**
- Consistent user experience across projects
- Cross-project features (shared teams, unified auth)
- Onboarding new projects with proven identity patterns
- Future SSO and centralized access management

**Harder:**
- Coordinating schema changes across multiple projects
- Handling projects with genuinely different identity requirements
- Migration of existing projects to the shared model
- Defining the boundary between shared and project-specific identity attributes


