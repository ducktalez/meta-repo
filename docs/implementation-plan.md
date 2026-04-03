# Implementation Plan — Meta-Repo

> This document tracks the current and planned implementation tasks for the meta-repo.
> Newest entries at the top. Completed items move to the bottom.

## Current Status

**Phase:** Initial Development
**Last Updated:** 2026-04-02

## Roadmap

| Phase | Description | Target Date | Status |
|-------|------------|-------------|--------|
| 1 — Foundation | Standards, templates, catalog, ADRs, data models | 2026-Q1 | ✅ done |
| 2 — Governance hardening | Repo classification, dev methodology docs, UI standards | 2026-Q2 | 🔧 in progress |
| 3 — Security & deployment | Central security concept, deployment automation standard | 2026-Q3 | planned |
| 4 — Automation | Agent evaluation, auto-commits, ADR validation, changelog | 2026-Q4 | planned |

---

## Current Sprint / Focus

- [ ] Establish repository type classification in catalog format (see §1)
- [ ] Add pictasia catalog entry (see §2)
- [ ] Document the development methodology ("lean instructions" approach) (see §3)

---

## Backlog

### §1 — Repository Type Classification

**Origin:** ideas.md — "Wichtige Unterscheidung bei Repositories"
**Priority:** high

Repos need a `Type` field in the catalog metadata to distinguish:

| Type | Description | Example |
|------|-------------|---------|
| `code` | Programming repo with agent support | dialectree, hometools, plagih, playbox |
| `data` | Personal/knowledge repo, agent generates blueprints | job-application-hub |
| `hybrid` | Mix of both | — |

Tasks:
- [ ] Add `Repository Type` field to `catalog/README.md` field reference
- [ ] Add `Repository Type` row to `catalog/_example-repo.md`
- [ ] Update all existing catalog entries with the new field
- [ ] Add a note about personal data controls for `data`-type repos (release checks)

---

### §2 — Add pictasia Catalog Entry

**Origin:** ideas.md — "pictasia hinzufügen"
**Priority:** high (quick win)

- [ ] Create `catalog/pictasia.md` — mark as external/non-conforming, deviation documented
- [ ] Verify catalog index in `catalog/README.md` is up to date

> Already partially done — `catalog/pictasia.md` exists. Verify completeness.

---

### §3 — Document Development Methodology

**Origin:** ideas.md — "Kurzbeschreibung und Analyse der besonderen Entwicklungsmethodik"
**Priority:** high

Write a concise standard document explaining the lean-instructions development approach used across all repos:

1. **Copilot Instructions** (`.github/copilot-instructions.md`) — lean, general, self-updating
2. **Architecture.md** — living document, reviewed regularly
3. **Implementation-Plan.md** — task tracking, newest on top
4. **Code comments** — detailed intent lives in code, not in instructions
5. **Pitfalls** — documented inline or in architecture

Tasks:
- [ ] Create `standards/development-methodology.md`
- [ ] Reference it from `standards/README.md`
- [ ] Reference it from the copilot-instructions template

---

### §4 — Formalize Implementation Step-Stack

**Origin:** ideas.md — "meta-Instructions Ablauf"
**Priority:** high

Define the standard workflow that every implementation task must follow:

1. Update `implementation-plan.md` (new entry on top)
2. Write instructions / comments describing intent (incl. gotchas, functionality)
3. Implement (incl. tests, docs)
4. Update architecture if needed
5. Git commit + push when tests pass

Tasks:
- [ ] Add step-stack as a section in `standards/development-methodology.md` (see §3)
- [ ] Add to copilot-instructions template as a standard workflow reference

---

### §5 — UI Design Standards

**Origin:** ideas.md — "Allgemeine Anweisungen für Benutzeroberflächen"
**Priority:** medium

Create a reusable UI standard applicable to all repos with a frontend:

- No repetitive/trivial info shown by default — show on hover
- Focus on clarity and scannability
- Consistent patterns across repos (navigation, error display, loading states)

Tasks:
- [ ] Create `standards/ui-conventions.md`
- [ ] Reference from `standards/README.md`
- [ ] Reference from copilot-instructions template (conditional: "if repo has frontend")

---

### §6 — Security Concept & Deployment Standard

**Origin:** ideas.md — "Sicherheitskonzept/deployment-automatisierung"
**Priority:** medium

Central standard that all repos must follow once they reach release status:

- Deployment process (Docker, GitHub Actions)
- Security tests (regular scans)
- HTTPS / encryption of sensitive data
- Centralized user management (roles, permissions) — ties to identity-concept
- Backups & recovery testing
- Automated alerts for suspicious activity

Tasks:
- [ ] Create `standards/security-and-deployment.md`
- [ ] Reference from `standards/README.md`
- [ ] Create ADR `004-security-and-deployment-standard.md` if decisions are needed
- [ ] Update `infrastructure/services.md` with deployment pipeline references

---

### §7 — Agent Evaluation Framework

**Origin:** ideas.md — "Effektivität von verschiedenen Agenten evaluieren"
**Priority:** medium

Evaluate and compare AI coding agents (Opus, Sonnet, OpenAI, etc.):

- How many files need to be read for full context?
- What information was missing to start a task?
- Session summaries for deeper analysis
- Comparison on complex/subjective tasks

Tasks:
- [ ] Create `automation/agent-evaluation.md` — define evaluation criteria and process
- [ ] Document first comparison results after running parallel agent sessions
- [ ] Consider storing/summarizing Copilot chat sessions periodically

---

### §8 — Auto-Commit & Changelog Automation

**Origin:** ideas.md — "AutoCommits mit Co-Pilot" + "Umgesetzte Punkte automatisch in Changelog"
**Priority:** low

- Auto-commit after implementation-plan section passes tests
- Auto-generate changelog from completed implementation-plan items
- Evaluate feasibility with GitHub Actions or local git hooks

Tasks:
- [ ] Research: git hook vs. GitHub Action vs. Copilot-driven approach
- [ ] Prototype in one repo (e.g., hometools or plagih)
- [ ] If successful, document as standard in `standards/`

---

### §9 — ADR Compliance Validation

**Origin:** ideas.md — "Automatisierte Überprüfung von ADRs"
**Priority:** low

Automated check whether ADR-proposed solutions actually match technology targets.

Tasks:
- [ ] Define validation rules (e.g., ADR references a non-target tech → warning)
- [ ] Prototype as a simple Python script or GitHub Action
- [ ] Add to `automation/`

---

### §10 — Setup.py / Makefile / Shell Strategy

**Origin:** ideas.md — "Setup vs shell file vs make file"
**Priority:** low

Decide and document when to use which:

- `setup.py` / `pyproject.toml` — package installation + tech composition overview
- `Makefile` — server management, `make clean`, common dev tasks
- Shell files — avoid in general (document why)

Tasks:
- [ ] Add section to `standards/technology-targets.md` or create `standards/build-tooling.md`
- [ ] Review existing repos for consistency

---

## Blockers

| Blocker | Impact | Owner | Status |
|---------|--------|-------|--------|
| No CI/CD pipelines yet | Blocks automation tasks (§8, §9) | — | open |

## Completed

- [x] Initial meta-repo setup (standards, templates, catalog, ADRs, data models, infrastructure)
- [x] Catalog entries for all existing repos
- [x] Playbox repo planned and catalog entry created
- [x] Brainstorm ideas extracted to `ideas.md`
- [x] Implementation plan created (`docs/implementation-plan.md`)

## Dependencies

- §6 (Security) depends on §4 (Step-Stack) being formalized first
- §8 (Auto-Commit) depends on CI/CD pipelines being available
- §9 (ADR Validation) depends on §8 or at least a basic automation setup

## Notes

- New project ideas (family tree, Haushaltsplan, TV-Sender, Drei-Fragezeichen-Generator, etc.) remain in `ideas.md` until they get a catalog entry and their own repo
- This plan covers meta-repo tasks only — sub-repo implementation plans live in their respective repos

