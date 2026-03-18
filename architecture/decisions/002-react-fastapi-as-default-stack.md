# 2. React + FastAPI as Default Stack

**Date:** 2026-03-18
**Status:** Accepted

## Context

Multiple projects require web-based frontends and API backends. Without a standard stack, each project makes independent technology choices, leading to:

- Fragmented expertise across different frameworks
- Inability to share components, patterns, or tooling
- Higher onboarding cost when switching between projects
- Diverging API conventions and frontend architectures

We need a default stack that balances productivity, ecosystem maturity, and consistency across projects.

## Decision

We adopt the following as the **default technology stack** for web projects:

- **Frontend:** React with TypeScript
- **Backend:** FastAPI with Python
- **Database:** PostgreSQL
- **ORM:** SQLAlchemy / SQLModel

This is a **default, not a mandate**. Projects may deviate if there is a justified reason (e.g., different domain requirements, performance constraints, team expertise). All deviations must be documented using the meta-repo deviation template.

See [standards/technology-targets.md](../../standards/technology-targets.md) for the full technology target definition.

## Consequences

**Easier:**
- Shared knowledge and patterns across projects
- Reusable frontend components and backend modules
- Consistent API design and database conventions
- Streamlined tooling (linting, testing, deployment)

**Harder:**
- Projects with genuinely different requirements need explicit deviation documentation
- Team members need proficiency in React + TypeScript and Python + FastAPI
- Emerging technologies or better-suited alternatives require a conscious decision to adopt


