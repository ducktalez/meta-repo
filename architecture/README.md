# Architecture Decisions

This directory contains Architecture Decision Records (ADRs) for cross-cutting decisions that affect multiple repositories in the ecosystem.

## What is an ADR?

An Architecture Decision Record captures a significant architectural decision along with its context and consequences. We follow the format established by [Michael Nygard](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions).

## Format

Each ADR follows this structure:

```markdown
# [Number]. [Title]

**Date:** YYYY-MM-DD
**Status:** Proposed | Accepted | Deprecated | Superseded by [ADR-XXX]

## Context
What is the issue that we're seeing that is motivating this decision or change?

## Decision
What is the change that we're proposing and/or doing?

## Consequences
What becomes easier or more difficult to do because of this change?
```

## How to Create a New ADR

1. Copy the format above
2. Use the next sequential number
3. Set status to `Proposed`
4. Submit for review
5. Once accepted, update status to `Accepted`

## Decision Log

| #   | Title                                  | Status   | Date       |
|-----|----------------------------------------|----------|------------|
| 001 | [Polyrepo with Meta Governance](decisions/001-polyrepo-with-meta-governance.md) | Accepted | 2026-03-18 |
| 002 | [React + FastAPI as Default Stack](decisions/002-react-fastapi-as-default-stack.md) | Accepted | 2026-03-18 |
| 003 | [Central Identity Model](decisions/003-central-identity-model.md) | Proposed | 2026-03-18 |


