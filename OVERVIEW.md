# Active Repositories — Overview

> Generated: 2026-03-18 · Excludes archived and maintenance-only repositories

## Summary

| Repository | Type | Backend | Frontend | Database | Key Libraries | Testing | Linting |
|---|---|---|---|---|---|---|---|
| [dialectree](catalog/dialectree.md) | Web App | FastAPI, SQLAlchemy | React 19, XY-Flow | SQLite (dev) / PostgreSQL (prod) | pydantic, python-jose, bcrypt | pytest, vitest | — |
| [hometools](catalog/hometools.md) | CLI + Streaming Server | FastAPI, uvicorn | PWA (vanilla) | — (file-based) | pydub, mutagen, tmdbv3api, httpx | pytest, pytest-playwright | ruff, pre-commit |
| [job-application-hub](catalog/job-application-hub.md) | Data Repo + Dashboard | FastAPI (dashboard) | React 18, Tailwind CSS | — (reads YAML/Markdown) | axios, vite | — | — |
| [plagih](catalog/plagih.md) | Python Library | — | — | — | numpy, pandas, sympy, matplotlib, scikit-learn | pytest, pytest-cov | ruff, pre-commit |

---

## dialectree

| | |
|---|---|
| **Purpose** | Structured argument trees — maps debates into PRO / CONTRA / NEUTRAL hierarchies |
| **Priority** | 🔴 high |
| **Architecture** | Monolith (backend + frontend + n8n workflows) |

### Tech Stack

| Layer | Technology |
|---|---|
| Backend | **FastAPI** · SQLAlchemy 2.x · Pydantic 2.x · uvicorn |
| Frontend | **React 19** (TypeScript) · Vite 6 · **@xyflow/react** (argument graph) |
| Database | SQLite in-memory (dev) → PostgreSQL via `DATABASE_URL` (prod) |
| Auth | JWT (python-jose + passlib/bcrypt) |
| Automation | **n8n** (Twitter import workflow) |
| Testing | pytest + pytest-asyncio (backend) · vitest + testing-library (frontend) |

### Key Domain Models

`Topic` → `Argument` (PRO/CONTRA/NEUTRAL) → `Evidence` (typed: Study, Statistic, Law, …) → `Comment`, `Vote`, `Tag`, `Label`

### API Endpoints (Backend)

Topics, Arguments, Argument Groups, Evidence, Comments, Votes, Tags, Labels, Users, Definition Forks

---

## hometools

| | |
|---|---|
| **Purpose** | Personal media library tools — music sanitization, video organizing (TMDB), local audio & video streaming |
| **Priority** | 🔴 high |
| **Architecture** | Installable Python package with CLI entry point + embedded FastAPI streaming server |

### Tech Stack

| Layer | Technology |
|---|---|
| Core | **Python ≥ 3.10** · setuptools · CLI via `hometools.cli:main` |
| Streaming | **FastAPI** · uvicorn · PWA (Service Worker, IndexedDB, offline playback) |
| Audio | **pydub** · **mutagen** (metadata) · librosa (optional analysis) |
| Video | **tmdbv3api** (TMDB metadata) |
| Testing | pytest · pytest-cov · pytest-playwright (UI) |
| Quality | **ruff** · pre-commit · Makefile |

### Modules

| Module | Function |
|---|---|
| `audio.sanitize` | Filename/tag cleanup for music files |
| `audio.metadata` | Read/write audio metadata (mutagen) |
| `audio.compare` | Duplicate / similarity detection |
| `audio.merger` | Merge audio files |
| `audio.silence` | Silence detection / trimming |
| `video.organizer` | TMDB-based video renaming & sorting |
| `streaming.audio` | Local audio streaming server (PWA) |
| `streaming.video` | Local video streaming server (PWA) |
| `streaming.core` | Shared streaming infrastructure |

---

## job-application-hub

| | |
|---|---|
| **Purpose** | Persistent job application hub with AI support — personality analysis, target tracking, CV management |
| **Priority** | 🟡 medium |
| **Architecture** | Markdown/YAML data repo + local React dashboard |

### Tech Stack

| Layer | Technology |
|---|---|
| Data Layer | **Markdown** · **YAML** (structured job/company data) |
| Dashboard Backend | **FastAPI** (port 8009) — parses repo files at runtime |
| Dashboard Frontend | **React 18** (TypeScript) · Vite 5 · **Tailwind CSS** · axios |
| CV Build | **LaTeX** (multiple CV variants, PowerShell build script) |
| Automation | GitHub **Copilot Instructions** for AI-assisted content |

### Dashboard Endpoints

| Endpoint | View |
|---|---|
| `/api/status` | Countdown, Bewerbungsfunnel, Metriken |
| `/api/jobs` | Scraper-Ergebnisse als filterbare Karten |
| `/api/companies` | Sortierbare Tabelle mit Scores |
| `/api/pitches` | Company Pitches ("Sell me this job") |
| `/api/timeline` | Visueller Lebens-Zeitstrahl |

### Pillars

| Pillar | Content |
|---|---|
| 🧠 Profile & Orientation | Personality analysis, preferences, career journal, timeline |
| 📄 CV & Documents | Master-CV + 5 LaTeX variants (standard, extended, AI/data, fullstack, consulting, non-tech) |
| 🎯 Targets & Applications | Company catalog, job listings (YAML), scraper, application log |
| 🔨 Workspace | Active applications (per company: CV + cover letter) |
| 🗂️ Archive | Lessons learned from past positions |

---

## plagih

| | |
|---|---|
| **Purpose** | Explainable Genetic Programming framework — "familiarity" metric (patent filed 2023, Germany) |
| **Priority** | 🔴 high |
| **Architecture** | Installable Python library (MIT) |

### Tech Stack

| Layer | Technology |
|---|---|
| Core | **Python ≥ 3.9** · setuptools |
| Scientific | **NumPy** · **Pandas** · **SymPy** (tree simplification/unification) · **scikit-learn** |
| Visualization | **matplotlib** · LaTeX renderer · tree renderer |
| Testing | pytest · pytest-cov |
| Quality | **ruff** · pre-commit |

### Package Structure

| Module | Function |
|---|---|
| `trees._gp_engine` | Main GP engine |
| `trees._evolution` | Evolution / selection operators |
| `trees._nodes` | Tree node definitions |
| `tree_complexity` | Bytecode complexity · Tree Edit Distance |
| `visualization` | LaTeX + tree rendering |
| `paretofront` | Multi-objective Pareto front |
| `population_merge` | Merged population tree (SymPy) |
| `targeted_optimization` | Targeted optimization strategies |
| `parallel` | Parallel evaluation |
| `monitoring` | Run monitoring |
| `evaluation_context` | Evaluation context management |

### Research Features

- **Familiarity metric** — similarity measure to a reference program
- **SymPy integration** — algebraic simplification and unification of candidate trees
- **Merged population tree** — single tree representing all individuals
- **Pseudo-backpropagation** — in development (focus: `if`/`piecewise` operator)
- **Tree Edit Distance** — structural comparison of GP trees

---

## Cross-Cutting Patterns

| Concern | dialectree | hometools | job-application-hub | plagih |
|---|---|---|---|---|
| **Language** | Python + TypeScript | Python | Python + TypeScript + LaTeX | Python |
| **Backend** | FastAPI | FastAPI | FastAPI | — |
| **Frontend** | React (Vite) | PWA | React (Vite) | — |
| **DB** | SQLAlchemy (SQLite/PG) | file-based | file-based (YAML/MD) | — |
| **Auth** | JWT | — | — | — |
| **Package Mgmt** | pip | pip + setuptools | pip + npm | pip + setuptools |
| **Testing** | pytest + vitest | pytest | — | pytest |
| **Linting** | — | ruff | — | ruff |
| **CI/CD** | — | — | — | — |
| **Pre-commit** | — | ✅ | — | ✅ |
| **Copilot Instructions** | ✅ | ✅ | ✅ | ✅ |

