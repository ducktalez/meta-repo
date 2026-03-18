# 1. Polyrepo with Meta Governance

**Date:** 2026-03-18
**Status:** Accepted

## Context

We manage multiple projects across different domains. Each project has its own repository, tech stack choices, and lifecycle. Without central coordination, this leads to:

- Diverging standards and conventions
- Duplicated effort and inconsistent documentation
- Difficulty transferring improvements between projects
- No visibility into cross-project architecture or data model alignment

A monorepo could address some of these issues but introduces tight coupling, complex CI/CD, and makes it harder to manage projects with different lifecycles and contributors.

## Decision

We adopt a **polyrepo architecture with centralized governance** through a dedicated meta-repo.

- Each project remains in its own repository with its own lifecycle
- The meta-repo defines shared standards, templates, technology targets, and data model conventions
- Sub-repos reference meta-repo standards and document deviations explicitly
- The meta-repo maintains a catalog of all sub-repositories
- Regular reviews ensure cross-repo consistency and improvement propagation

This is not a permanent commitment against a monorepo. If future needs demand tighter integration (shared libraries, core modules), a hybrid model or partial monorepo can be evaluated.

## Consequences

**Easier:**
- Independent deployment and release cycles per project
- Onboarding to individual projects without understanding the entire ecosystem
- Gradual adoption of standards (not all-or-nothing)
- Clear separation of governance from implementation

**Harder:**
- Keeping sub-repos in sync with evolving meta-repo standards
- Sharing code between repositories (no built-in mechanism)
- Ensuring all projects actually follow and update to current standards
- Cross-repo refactoring requires coordinated effort


