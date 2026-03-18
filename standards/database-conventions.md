# Database Conventions

> This document defines the database design standards that all sub-repositories should follow.
> Deviations must be documented using the [deviation template](deviation-template.md).

## Database Engine

- **Default:** PostgreSQL
- Other engines are allowed with documented justification

## Naming Conventions

### Tables

- Use `snake_case`
- Use **plural** names for tables: `users`, `roles`, `organizations`
- Junction/association tables: combine both table names, e.g., `user_roles`, `team_members`

### Columns

- Use `snake_case`
- Primary key: `id`
- Foreign keys: `{referenced_table_singular}_id` — e.g., `user_id`, `organization_id`
- Boolean columns: use `is_` or `has_` prefix — e.g., `is_active`, `has_verified_email`
- Timestamp columns: use `_at` suffix — e.g., `created_at`, `updated_at`, `deleted_at`

### Indexes

- Name format: `ix_{table}_{column}` for single-column indexes
- Name format: `ix_{table}_{col1}_{col2}` for composite indexes
- Unique constraints: `uq_{table}_{column}`

### Constraints

- Primary key: `pk_{table}`
- Foreign key: `fk_{table}_{column}_{referenced_table}`
- Check constraint: `ck_{table}_{description}`

## ID Strategy

- **Default:** UUID v4 as primary key
- Stored as `UUID` type in PostgreSQL (not as string)
- Generated server-side (application layer), not database-side
- Rationale: globally unique, safe for distributed systems, no sequential exposure

## Standard Audit Fields

Every table should include these audit fields unless there is a strong reason not to:

| Column       | Type        | Description                       |
|-------------|-------------|-----------------------------------|
| `id`        | UUID        | Primary key                       |
| `created_at`| TIMESTAMP   | Row creation time (UTC)           |
| `updated_at`| TIMESTAMP   | Last modification time (UTC)      |
| `created_by`| UUID / NULL | Reference to user who created     |
| `updated_by`| UUID / NULL | Reference to user who last updated|

## Soft Delete

- **Default:** Use soft delete for important entities
- Add `deleted_at` (TIMESTAMP, nullable) and optionally `deleted_by` (UUID, nullable)
- `deleted_at IS NULL` means the record is active
- Application queries should filter soft-deleted records by default
- Hard delete only for data that must be permanently removed (e.g., GDPR compliance)

## Versioning / History

- For entities requiring audit trails, consider a separate history/audit table
- Pattern: `{table}_history` with the same columns plus `version`, `changed_at`, `changed_by`
- Not required for all tables — use where business requirements demand it

## Migration Strategy

- Use **Alembic** for Python/SQLAlchemy projects
- Migrations must be:
  - Versioned and sequential
  - Reversible where possible (include `downgrade`)
  - Reviewed before deployment
- Never modify a migration that has been applied to production
- Migration naming: auto-generated with descriptive message

## Relationships & Foreign Keys

- Always define explicit foreign key constraints
- Use `ON DELETE` behavior intentionally:
  - `CASCADE` — only when child records have no meaning without parent
  - `SET NULL` — when child records should survive parent deletion
  - `RESTRICT` — default, prevents accidental deletion of referenced records

## Enums & Status Fields

- Use database-level enums or string-based status fields (not magic integers)
- Define allowed values in application code, not only in the database
- Example: `status VARCHAR NOT NULL DEFAULT 'active' CHECK (status IN ('active', 'inactive', 'suspended'))`

## Multi-Tenancy Considerations

- If a project requires multi-tenancy, prefer row-level isolation with an `organization_id` column
- Shared tables (e.g., `users`) may reference multiple organizations via junction tables
- Schema-per-tenant only if there is a strong isolation requirement

## Reference to Core Entities

Shared core entities (User, Role, Organization, etc.) are defined in the meta-repo:
→ [data-models/core-entities.md](../data-models/core-entities.md)

All sub-repositories using these entities should align with the core definitions and document any extensions or deviations.

