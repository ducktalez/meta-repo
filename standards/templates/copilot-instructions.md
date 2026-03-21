# [Project Name] – Copilot Instructions

## What is this?

<!-- One or two sentences: what does this project do, what is its core abstraction? -->

[Project Name] does ...

## Development Phase Policy

<!-- State the current phase and what Copilot should and should NOT build right now. -->

The project is in early development. Only implement what is **technically necessary right now**.
- **Security, caching, styling, monitoring**: deferred. Mark placeholders with `# TODO: post-dev`.
- **No speculative features or database columns.** If it's not needed for the current task, don't build it.
- Priority: **Backend API → Tests → Seed data → Frontend (minimal).**
- See `.github/instructions/backend.instructions.md` and `frontend.instructions.md` for layer-specific rules.

## Coding Conventions

- All code, comments, docstrings, and documentation in **English**.
- Every new endpoint **must** have tests in `backend/tests/` (`test_{resource}.py`).
- Shared test fixtures live in `conftest.py`.
- New models → `models.py`, schemas → `schemas.py`, routes → `routers/{resource}.py` (register in `main.py`).
- Keep it simple — working and lean over complex and perfect.

## API Conventions

- All endpoints prefixed with `/api` (or `/api/v1/`).
- Error format: `{ "detail": "...", "code": "MACHINE_READABLE_CODE" }`.
- Enum values are **uppercase strings** in JSON.

<!-- Add project-specific API rules here. -->

## Known Pitfalls

<!-- List concrete gotchas that would trip up Copilot or a new developer. -->

- **Tests must run from `backend/`**: `cd backend && python -m pytest tests/ -v`.
- After `db.commit()` + `db.close()`, do **not** access ORM attributes on detached objects → `DetachedInstanceError`.

<!-- Add project-specific pitfalls here. -->

## Maintaining These Instructions

When a change introduces new conventions, pitfalls, or architectural decisions, **update the relevant instruction file** (this file, or `.github/instructions/*.instructions.md`). Keep them accurate and lean.

## Working Process: Maintaining Docs

- Update architectural changes in `Architecture.md`.
- Track deferred work in `Implementation-Plan.md`.

<!-- Add project-specific doc maintenance rules here. -->

---

### Layer-Specific Instructions

Create these files alongside this template:

**`.github/instructions/backend.instructions.md`**
```markdown
---
applyTo: "backend/**"
---
# Backend Instructions

## Deferred until go-live
- **Security & auth**: not implemented. Mark with `# TODO: security`.
- **Migrations**: use Alembic if PostgreSQL, skip if in-memory SQLite.
```

**`.github/instructions/frontend.instructions.md`**
```markdown
---
applyTo: "frontend/**"
---
# Frontend Instructions

## What "only the necessary" means here
- **No complex state management.** Plain `useState`/`useEffect` is sufficient.
- The backend is the priority. Frontend must not block backend development.
```


