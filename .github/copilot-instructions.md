# Copilot Instructions — Meta-Repo

## Project Context

This is the **meta-repo** — the central governance repository for a polyrepo ecosystem. It does not contain application code. It contains standards, templates, architecture decisions, data model definitions, infrastructure documentation, and coordination for automation.

## Language

- All files in this repository are written in **English**
- Use clear, concise, and structured Markdown
- Prefer tables and structured formats over free-form prose

## Key Conventions

- Follow the [ADR format](../architecture/README.md) for architecture decisions
- Use the templates in `standards/templates/` as the canonical structure for sub-repo documentation
- Catalog entries in `catalog/` follow the format defined in `catalog/README.md`
- Core entity definitions in `data-models/` are the source of truth for shared models

## Important Directories

- `standards/` — central rules, conventions, and templates
- `catalog/` — structured overview of all sub-repositories
- `architecture/decisions/` — architecture decision records (ADRs)
- `data-models/` — shared entity definitions and governance
- `infrastructure/` — hosts, services, storage documentation
- `monitoring/` — planned health and status system
- `automation/` — planned agent-based orchestration

## When Making Changes

- New standards should be added to `standards/`
- New architecture decisions should be added as numbered ADRs in `architecture/decisions/`
- New repositories should get a catalog entry in `catalog/`
- Infrastructure changes should be reflected in `infrastructure/`
- Always update the relevant README index when adding new files

