# playbox

## Metadata

| Field                  | Value                                  |
|------------------------|----------------------------------------|
| **Name**               | playbox                                |
| **Purpose**            | Collection of small browser-based games — PWA-installable, shared infrastructure |
| **Status**             | planned                                |
| **Priority**           | medium                                 |
| **Tech Stack**         | FastAPI (Python), React or vanilla TS, Vite, PWA |
| **Architecture Type**  | monolith (multi-game)                  |
| **Database**           | SQLite (local highscores/state)        |
| **Auth Model**         | None (local play)                      |
| **Documentation Status** | partial                              |
| **Monitoring Relevant** | no                                    |
| **Automation Level**   | none                                   |
| **Infrastructure Refs** | —                                     |

## Deviations

| Standard                     | Deviation        | Reason              | Accepted | Temporary |
|-----------------------------|------------------|----------------------|----------|-----------|
| _No deviations documented_  | —                | —                    | —        | —         |

## Core Entity Alignment

| Entity       | Aligned | Notes                        |
|-------------|---------|------------------------------|
| User        | ⬜ No   | Local-only, no user model    |
| Role        | ⬜ No   | Not applicable               |
| Organization| ⬜ No   | Not applicable               |

## Proposed Structure

```
playbox/
├── backend/
│   ├── app/
│   │   ├── core/              # Shared: FastAPI app factory, PWA manifest, SW
│   │   ├── games/
│   │   │   ├── poster/        # "Spiel im Poster" — game logic + API
│   │   │   └── quiz2l/        # quiz2l — game logic + API
│   │   └── main.py            # Unified server, mounts all games
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── core/              # Shared: PWA shell, layout, offline support
│   │   ├── games/
│   │   │   ├── poster/        # Poster game UI
│   │   │   └── quiz2l/        # quiz2l UI
│   │   └── main.tsx
│   ├── package.json
│   └── vite.config.ts
├── .github/
│   └── copilot-instructions.md
├── pyproject.toml
└── README.md
```

### Design Principles

1. **One server, many games** — single FastAPI instance mounts each game as a sub-router (`/api/poster/`, `/api/quiz2l/`)
2. **Shared PWA shell** — common Service Worker, manifest, offline support, installable on home screen
3. **Game isolation** — each game is a self-contained module (backend + frontend), can be developed independently
4. **Pattern from hometools** — replicates the FastAPI + PWA installability pattern without coupling to media tools
5. **Lightweight** — no heavy dependencies, fast to start

## Games (Planned)

| Game | Description | Status |
|------|-------------|--------|
| poster | "Spiel im Poster" — TBD | planned |
| quiz2l | Quiz game — TBD | planned |

## Notes

- Inspired by the hometools streaming architecture (FastAPI + PWA + Service Worker)
- Each game should be playable offline after first load
- Future: GroupGame-App (from brainstorm), multiplayer support

## Links

- **GitHub:** https://github.com/ducktalez/playbox
- **Deployed:** _not deployed (local PWA)_
- **Architecture.md:** _to be created_

