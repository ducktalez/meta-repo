# Meta-Repo

Central governance, standards, and orchestration repository for all projects in this polyrepo ecosystem.



## Purpose

Meta-Repo serves as the overarching control layer that manages standards, architecture decisions, documentation structure, technology targets, data model governance, infrastructure documentation, and future agent-based automation across all sub-repositories.

It is **not** a regular development project. It is the single source of truth for:

- **Standards & Templates** — unified structure for documentation, instructions, and conventions
- **Architecture Decisions** — recorded as ADRs (Architecture Decision Records)
- **Repository Catalog** — structured overview of all sub-repositories
- **Data Model Governance** — shared core entities, naming conventions, identity concepts
- **Infrastructure Documentation** — hosts, services, storage, environments
- **Monitoring** _(planned)_ — service health, status, warnings across all systems
- **Automation** _(planned)_ — agent-based orchestration, prioritized maintenance

## Principles

1. **Standards central, specifics local** — general rules live here; repo-specific details live in sub-repos but reference these standards.
2. **Deviations must be visible** — any deviation from central standards must be explicitly documented and justified.
3. **Documentation is human- and machine-readable** — structured Markdown wherever possible.
4. **Architecture is not static** — regular reviews and improvements are part of the system.
5. **Good solutions should be reused** — improvements proven in one repo are evaluated for all suitable repos.
6. **Data model consistency is strategic** — unified core models (users, roles, ownership) are a central goal.
7. **Built for future automation** — structure and format are designed so agents can work with them effectively.

## Repository Structure

```
meta-repo/
├── .github/
│   └── copilot-instructions.md    # Copilot instructions for this repo
├── standards/
│   ├── templates/
│   │   ├── architecture.md        # Template for Architecture.md in sub-repos
│   │   ├── implementation-plan.md # Template for Implementation-Plan.md
│   │   └── copilot-instructions.md# Template for copilot-instructions.md
│   ├── deviation-template.md      # Template for documenting deviations
│   ├── technology-targets.md      # Target stacks, conventions, principles
│   └── database-conventions.md    # DB naming, IDs, audit fields, migrations
├── catalog/
│   ├── README.md                  # Catalog format explanation & field reference
│   └── _example-repo.md           # Example catalog entry
├── architecture/
│   ├── README.md                  # ADR process & index
│   └── decisions/
│       ├── 001-polyrepo-with-meta-governance.md
│       ├── 002-react-fastapi-as-default-stack.md
│       └── 003-central-identity-model.md
├── data-models/
│   ├── core-entities.md           # User, Role, Permission, Org, Team
│   ├── shared-vs-local.md         # Shared core + local extensions principle
│   └── identity-concept.md        # Central identity / auth concept
├── infrastructure/
│   ├── hosts.md                   # Machines, servers, PCs
│   ├── services.md                # Services, host mapping, environments
│   └── storage.md                 # Storage locations, backups
├── monitoring/
│   └── README.md                  # Placeholder: scope & planned features
├── automation/
│   └── README.md                  # Placeholder: scope & planned features
├── docs/
│   └── implementation-plan.md     # Implementation plan for meta-repo itself
├── ideas.md                       # Raw brainstorm dump
└── README.md                      # This file
```

## Getting Started

1. **Start here →** [OVERVIEW.md](OVERVIEW.md) — technology overview of all active repositories.
2. Review the [standards](standards/) to understand central conventions.
3. Browse the [catalog](catalog/) for an overview of all managed repositories.
4. Read the [architecture decisions](architecture/) for key technical choices.
5. Check [data-models](data-models/) for shared entity definitions.
6. See [infrastructure](infrastructure/) for the current system landscape.
7. See [ideas.md](ideas.md) for the raw brainstorm / idea backlog.
8. See [docs/implementation-plan.md](docs/implementation-plan.md) for the meta-repo roadmap.

## Status

This repository is in its **initial setup phase**. Monitoring and automation capabilities are planned for future iterations.

