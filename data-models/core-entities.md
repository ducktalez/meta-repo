# Core Entities

> This document defines the shared core entities that sub-repositories should align with.
> Project-specific extensions are allowed but the core structure should remain consistent.
> See [shared-vs-local.md](shared-vs-local.md) for the extension principle.

## User

The central identity entity. Every project managing users should align with this structure.

| Column             | Type         | Required | Description                          |
|--------------------|-------------|----------|--------------------------------------|
| `id`               | UUID        | Yes      | Primary key                          |
| `email`            | VARCHAR     | Yes      | Unique email address                 |
| `username`         | VARCHAR     | No       | Optional display/login name          |
| `first_name`       | VARCHAR     | No       | First name                           |
| `last_name`        | VARCHAR     | No       | Last name                            |
| `is_active`        | BOOLEAN     | Yes      | Whether the account is active        |
| `is_verified`      | BOOLEAN     | Yes      | Whether email is verified            |
| `password_hash`    | VARCHAR     | Yes      | Hashed password (never plaintext)    |
| `last_login_at`    | TIMESTAMP   | No       | Last successful login                |
| `created_at`       | TIMESTAMP   | Yes      | Account creation time (UTC)          |
| `updated_at`       | TIMESTAMP   | Yes      | Last modification time (UTC)         |
| `deleted_at`       | TIMESTAMP   | No       | Soft delete timestamp                |

**Notes:**
- `email` is the primary unique identifier for authentication
- Password hashing algorithm should be consistent (recommend `bcrypt` or `argon2`)
- Projects may add columns but should not rename or redefine the core columns

## Role

Defines a named set of permissions. Supports RBAC (Role-Based Access Control).

| Column        | Type      | Required | Description                    |
|---------------|----------|----------|--------------------------------|
| `id`          | UUID     | Yes      | Primary key                    |
| `name`        | VARCHAR  | Yes      | Unique role name (e.g., `admin`, `editor`) |
| `description` | TEXT     | No       | Human-readable description     |
| `is_system`   | BOOLEAN  | Yes      | Whether this is a built-in role|
| `created_at`  | TIMESTAMP| Yes      | Creation time (UTC)            |
| `updated_at`  | TIMESTAMP| Yes      | Last modification time (UTC)   |

## Permission

Granular permission that can be assigned to roles.

| Column        | Type      | Required | Description                       |
|---------------|----------|----------|-----------------------------------|
| `id`          | UUID     | Yes      | Primary key                       |
| `codename`    | VARCHAR  | Yes      | Machine-readable key (e.g., `user.create`, `project.delete`) |
| `description` | TEXT     | No       | Human-readable description        |
| `created_at`  | TIMESTAMP| Yes      | Creation time (UTC)               |

## User–Role Assignment (`user_roles`)

| Column     | Type      | Required | Description          |
|------------|----------|----------|----------------------|
| `user_id`  | UUID     | Yes      | FK → `users.id`      |
| `role_id`  | UUID     | Yes      | FK → `roles.id`      |
| `granted_at`| TIMESTAMP| Yes     | When the role was assigned |
| `granted_by`| UUID    | No       | FK → `users.id` (who assigned it) |

**Primary Key:** (`user_id`, `role_id`)

## Role–Permission Assignment (`role_permissions`)

| Column          | Type      | Required | Description             |
|-----------------|----------|----------|-------------------------|
| `role_id`       | UUID     | Yes      | FK → `roles.id`         |
| `permission_id` | UUID     | Yes      | FK → `permissions.id`   |

**Primary Key:** (`role_id`, `permission_id`)

## Organization

Represents a company, team, or tenant.

| Column        | Type      | Required | Description                      |
|---------------|----------|----------|----------------------------------|
| `id`          | UUID     | Yes      | Primary key                      |
| `name`        | VARCHAR  | Yes      | Organization name                |
| `slug`        | VARCHAR  | Yes      | URL-friendly unique identifier   |
| `is_active`   | BOOLEAN  | Yes      | Whether the organization is active|
| `created_at`  | TIMESTAMP| Yes      | Creation time (UTC)              |
| `updated_at`  | TIMESTAMP| Yes      | Last modification time (UTC)     |
| `deleted_at`  | TIMESTAMP| No       | Soft delete timestamp            |

## Team

A group within an organization.

| Column            | Type      | Required | Description                    |
|-------------------|----------|----------|--------------------------------|
| `id`              | UUID     | Yes      | Primary key                    |
| `organization_id` | UUID     | Yes      | FK → `organizations.id`       |
| `name`            | VARCHAR  | Yes      | Team name                      |
| `description`     | TEXT     | No       | Team description               |
| `created_at`      | TIMESTAMP| Yes      | Creation time (UTC)            |
| `updated_at`      | TIMESTAMP| Yes      | Last modification time (UTC)   |

## Team Membership (`team_members`)

| Column     | Type      | Required | Description                    |
|------------|----------|----------|--------------------------------|
| `team_id`  | UUID     | Yes      | FK → `teams.id`                |
| `user_id`  | UUID     | Yes      | FK → `users.id`                |
| `role`     | VARCHAR  | Yes      | Role within team (`member`, `lead`, `admin`) |
| `joined_at`| TIMESTAMP| Yes      | When the user joined the team  |

**Primary Key:** (`team_id`, `user_id`)

## Organization Membership (`organization_members`)

| Column            | Type      | Required | Description                    |
|-------------------|----------|----------|--------------------------------|
| `organization_id` | UUID     | Yes      | FK → `organizations.id`       |
| `user_id`         | UUID     | Yes      | FK → `users.id`                |
| `role`            | VARCHAR  | Yes      | Role in org (`owner`, `admin`, `member`) |
| `joined_at`       | TIMESTAMP| Yes      | When the user joined           |

**Primary Key:** (`organization_id`, `user_id`)

## Entity Relationship Overview

```
User ──< UserRole >── Role ──< RolePermission >── Permission
 │
 ├──< OrganizationMember >── Organization
 │                                │
 └──< TeamMember >── Team ────────┘
```

## Extension Guidelines

- Projects **should not** rename or remove core columns
- Projects **may** add columns to core tables for project-specific needs
- Project-specific extensions should be documented in the project's Architecture.md
- If an extension proves useful across multiple projects, it should be proposed as a core entity change

