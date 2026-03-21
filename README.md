# Meta-Repo

Central governance, standards, and orchestration repository for all projects in this polyrepo ecosystem.


## Brainstorm




- Einführen von AutoCommits mit Hilfe von Co-Pilot? Oder als Change Log? So könnten alle Updates auch sinnvoll zusammengefasst werden. 
- Vergleich von mehreren Agents bei komplexen oder schwer qualitativ zu bewertenden Aufgaben.
- Automatisierte Überprüfung von ADRs auf Einhaltung der Standards (z.B. ob die vorgeschlagenen Lösungen tatsächlich den Zieltechnologien entsprechen).
- Diskussion über die Verwendung von Makefiles bei Servern zum Cleanen. 
- Kurzbeschreibung und Analyse der für diese Repositories besonderen Entwicklungsmethodik. (bedeutet Lean Instructions, Architecture.md und Implementation-Plan.md)
- Automatische Test-Generierung als Teil vom Instructions-file?
- ~~GroupGame-App!~~ → concretized as **playbox** repo (see [catalog/playbox.md](catalog/playbox.md)): Imposter, Piccolo, "Wer wird Elite-Hater?" Quiz, Chess Variants
- Abstammungsbaum Für die eigene Familie erzeugen und dann mit anderen merken wenn sie sie hochladen. 
- In großen Abständen soll im Implementation Plan ein Chores/aufräumen/Optimierungsschritt eingefügt werden.
- Gedanken sortieren-Repo + Video-Skripte-daraus-generieren-Repo + automatisch-Videos-rendern (Videos sind bloß eingeblendete Quellen)?
- Media view website similar to YouTube showing a lot of videos at the same time 
- Lokales LLM zum Laufen bringen und Architektur verstehen.
- Die Instructions in Kombination mit den Kommentaren in den Files sollen einen guten Leitfaden für die Intention der Implementierung mitgeben. In regelmäßigen Abständen sollte bei allen Repositories überprüft werden ob das gut umgesetzt ist. 
- Allgemeine Anweisungen für Benutzeroberflächen. 
  - In NutzerOberflächen sollten sich wiederholende/triviale Informationen nicht dem Nutzer angezeigt werden. Beim drüber hovern sollte vielleicht eine Beschreibung erscheinen. 
  - Der Fokus Sollte  auf eine gute Übersichtlichkeit gelegt werden.
  - Kann das als verständliche Instruction für alle Repos formuliert werden?
  - Projektidee: automatisches Aufstellen eines Haushaltsplans mit KI-Unterstützung. 
    - Upload der Kontoauszüge und daraus wird dann eine Analyse der Ausgaben erstellt. 
    - Einigbarer Potenzial wird erkannt.
- Sollten eventuell die Co-Pilot Chats über die Repositories gespeichert und analysiert werden? Zumindest in großen Abständen oder so?
- Für den TV-Sender-Repo: Automatisches Erstellen von YouTube-Kacke zusammen geschnitten von Politikern. 
  - Hierfür muss ein Archiv mit transkribierten Clips erstellt werden und dann ein Skript-Erstellungsmechanismus generiert werden.
  - Als Basis für Witze könnten folgende Ideen dienen: 
    - Generelle aktuelle Geschehnisse 
    - Dinge in der Agenda oder im Duktus der Person, die als Juktu-Kacke Basis herhalten muss?
    - Running Gags und andere Jokes oder lustige Themen, die immer gehen. Heißt ja nicht umsonst YouTube-Kacke? 
- Ueberrepo, herrenrepo
- Mett Render Maschine Drachenlord als TV Sender. Ich will das gesamte Leben des Hachenlord als Zeitstrahl, inklusive aller Videos die verfügbar sind, und jedem Content runtergeladen haben und daraus einen Fernsehsender machen, der immer wieder schöne Geschichten und Zeitstränge daraus macht. 
- Auto-Generierung von AI-generated, die drei Fragezeichen folgen anhand von Projektdaten. 
  - Ein allgemeines Instruction-File erhält Informationen zu den einzelnen Akteuren
  - In einem spezifischen Ordner/Fall werden aus potenziellen Rätseln etc. eine Story erzeugt. 
  - Die Story wird als dynamisches Audio-Produkt gerendert. Hierfür muss natürlich auch noch eine audio library erstellt werden, mit sound effekten etc..
- Automatisches Erstellen von Büchertexten auf Basis von wilden Kommentaren. Diese müssten noch initial geordnet werden und könnten dann auf einer Meta-Ebene ausformuliert werden, woraus wiederum ein Buch generiert werden kann oder ein Videoskript etc. 

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
└── README.md                      # This file
```

## Getting Started

1. **Start here →** [OVERVIEW.md](OVERVIEW.md) — technology overview of all active repositories.
2. Review the [standards](standards/) to understand central conventions.
3. Browse the [catalog](catalog/) for an overview of all managed repositories.
4. Read the [architecture decisions](architecture/) for key technical choices.
5. Check [data-models](data-models/) for shared entity definitions.
6. See [infrastructure](infrastructure/) for the current system landscape.

## Status

This repository is in its **initial setup phase**. Monitoring and automation capabilities are planned for future iterations.

