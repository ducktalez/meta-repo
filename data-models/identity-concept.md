# Central Identity Concept

> This document outlines the vision and phased approach for a central identity model across all projects, similar to an ERP master data concept.

## Vision

Multiple projects in our ecosystem manage users, roles, and access control independently. The long-term goal is to establish a **central identity foundation** that:

- Provides a single source of truth for user identity
- Enables single sign-on (SSO) across projects
- Standardizes role and permission management
- Reduces duplicated authentication and authorization logic
- Supports multi-tenancy through shared organization structures

## Current State

Today, each project manages its own:

- User registration and authentication
- Password storage and reset flows
- Role definitions and permission checks
- Session or token management

This leads to fragmented user experiences and duplicated effort.

## Target Architecture

```
┌──────────────────────────────────────────────┐
│            Central Identity Service          │
│                                              │
│  ┌──────────┐  ┌──────────┐  ┌───────────┐  │
│  │  Users   │  │  Roles   │  │   Orgs    │  │
│  │          │  │  Perms   │  │   Teams   │  │
│  └──────────┘  └──────────┘  └───────────┘  │
│                                              │
│  Auth endpoints: login, register, verify,    │
│  token refresh, password reset               │
│                                              │
│  Standards: JWT tokens, OAuth2 flows         │
└──────────────┬───────────────────────────────┘
               │
    ┌──────────┼──────────┐
    │          │          │
    ▼          ▼          ▼
┌────────┐ ┌────────┐ ┌────────┐
│Project │ │Project │ │Project │
│   A    │ │   B    │ │   C    │
│        │ │        │ │        │
│ Local  │ │ Local  │ │ Local  │
│ domain │ │ domain │ │ domain │
│ models │ │ models │ │ models │
└────────┘ └────────┘ └────────┘
```

## Phased Approach

### Phase 1: Model Alignment (Current)

- Define shared core entities in the meta-repo (→ [core-entities.md](core-entities.md))
- Sub-repos align their user/role models to the shared definitions
- No shared infrastructure yet — each project runs independently
- Deviations are documented

**Outcome:** Consistent data models, easy future migration.

### Phase 2: Shared Authentication Library

- Extract common auth logic into a shared library or package
- Standardize JWT token format and validation
- Standardize password hashing (bcrypt / argon2)
- Projects import the shared library instead of implementing their own

**Outcome:** Reduced duplication, consistent auth behavior.

### Phase 3: Central Identity Service

- Deploy a dedicated identity/auth microservice
- All projects authenticate against this service
- User management (registration, profile, password reset) centralized
- Projects receive identity via JWT and manage local authorization

**Outcome:** Single sign-on, centralized user management.

### Phase 4: Federated Authorization (Optional)

- Central service also manages cross-project roles and permissions
- Projects query the identity service for authorization decisions
- Organization and team management fully centralized

**Outcome:** Unified access control across the ecosystem.

## Authentication Standards

Regardless of the current phase, all projects should follow these conventions:

| Aspect              | Standard                                  |
|---------------------|-------------------------------------------|
| Token format        | JWT (JSON Web Tokens)                     |
| Token signing       | RS256 or HS256 (RS256 preferred)          |
| Token lifetime      | Access: 15–60 min, Refresh: 7–30 days    |
| Password hashing    | bcrypt or argon2                          |
| Transport           | HTTPS only                                |
| Storage (client)    | HttpOnly cookies or secure storage        |

## Open Questions

- Which projects are candidates for early adoption?
- Should we use an existing identity provider (e.g., Keycloak, Auth0) or build our own?
- How to handle migration of existing user data?
- What is the minimal viable scope for Phase 2?

## Related Documents

- [Core Entities](core-entities.md) — shared entity definitions
- [Shared vs. Local](shared-vs-local.md) — extension principle
- [ADR 003: Central Identity Model](../architecture/decisions/003-central-identity-model.md) — decision record

