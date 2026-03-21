# playbox

## Metadata

| Field                  | Value                                  |
|------------------------|----------------------------------------|
| **Name**               | playbox                                |
| **Purpose**            | Collection of small browser-based party & quiz games — PWA-installable, shared infrastructure |
| **Status**             | planned                                |
| **Priority**           | medium                                 |
| **Tech Stack**         | FastAPI (Python), React (TypeScript), Vite, PWA |
| **Architecture Type**  | monolith (multi-game)                  |
| **Database**           | PostgreSQL (quiz questions, ELO scores, reports); SQLite fallback for local-only games |
| **Auth Model**         | None (local play) / optional lightweight user for quiz ELO tracking |
| **Documentation Status** | partial                              |
| **Monitoring Relevant** | no                                    |
| **Automation Level**   | none                                   |
| **Infrastructure Refs** | —                                     |

## Deviations

| Standard                     | Deviation                          | Reason                                           | Accepted | Temporary |
|-----------------------------|-------------------------------------|--------------------------------------------------|----------|-----------|
| PostgreSQL as default DB     | SQLite for offline-only games       | Imposter & Piccolo need no persistent server DB  | yes      | no        |
| Central identity model       | Optional lightweight user model     | Full identity overkill for party games           | yes      | no        |

## Core Entity Alignment

| Entity       | Aligned | Notes                                      |
|-------------|---------|----------------------------------------------|
| User        | ⬜ No   | Optional lightweight user for quiz ELO only  |
| Role        | ⬜ No   | Not applicable                               |
| Organization| ⬜ No   | Not applicable                               |

## Proposed Structure

```
playbox/
├── backend/
│   ├── app/
│   │   ├── core/              # Shared: FastAPI app factory, config, DB setup
│   │   ├── games/
│   │   │   ├── imposter/      # Imposter — game logic + API
│   │   │   ├── piccolo/       # Piccolo — game logic + API
│   │   │   ├── quiz/          # "Wer wird Elite-Hater?" — quiz logic + API
│   │   │   └── chess/         # LiChess variant — game logic + API (low priority)
│   │   └── main.py            # Unified server, mounts all games
│   ├── alembic/               # DB migrations (for quiz/ELO data)
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── core/              # Shared: PWA shell, layout, offline support, SW
│   │   ├── games/
│   │   │   ├── imposter/      # Imposter game UI
│   │   │   ├── piccolo/       # Piccolo game UI
│   │   │   ├── quiz/          # Quiz game UI (both modes)
│   │   │   └── chess/         # Chess variant UI (low priority)
│   │   └── main.tsx
│   ├── public/
│   │   └── media/             # Quiz media assets (clips, images, documents)
│   ├── package.json
│   └── vite.config.ts
├── .github/
│   └── copilot-instructions.md
├── pyproject.toml
└── README.md
```

### Design Principles

1. **One server, many games** — single FastAPI instance mounts each game as a sub-router (`/api/imposter/`, `/api/piccolo/`, `/api/quiz/`, `/api/chess/`)
2. **Shared PWA shell** — common Service Worker, manifest, offline support, installable on home screen
3. **Game isolation** — each game is a self-contained module (backend + frontend), can be developed independently
4. **Pattern from hometools** — replicates the FastAPI + PWA installability pattern without coupling to media tools
5. **Lightweight** — no heavy dependencies, fast to start
6. **Community-driven content** — users can submit questions, report inappropriate content

---

## Games

### 1. Imposter

| Field       | Value          |
|-------------|----------------|
| **Status**  | planned        |
| **Priority**| high           |
| **Route**   | `/api/imposter/` |

#### Concept

A local multiplayer party game for groups of people physically present together.

#### Gameplay

1. Players enter their names into the app
2. The device is passed around — each player sees a secret word on screen
3. One randomly selected player sees **"Imposter"** instead of the word
4. A **5-minute timer** starts
5. The group discusses and tries to identify who the Imposter is (the person who doesn't know the word)

#### Features

| Feature                        | Description                                                |
|-------------------------------|------------------------------------------------------------|
| Word list                      | Curated list of terms; categories possible                 |
| Random Imposter selection      | Exactly one player per round is the Imposter               |
| Pass-and-play UI               | Screen shows word briefly, then covers it for next player  |
| 5-minute discussion timer      | Configurable timer with audio/vibration alert              |
| Report inappropriate word      | Button to flag a word as unsuitable — stored for review    |
| Offline capable                | Fully playable without internet after initial load         |

#### Data Model

| Entity        | Fields                                      | Storage |
|--------------|----------------------------------------------|---------|
| Word          | `id`, `text`, `category`, `flagged`, `active`| SQLite  |
| WordReport    | `id`, `word_id`, `reason`, `created_at`      | SQLite  |
| GameSession   | `id`, `player_names`, `word_id`, `imposter_index`, `created_at` | in-memory |

---

### 2. Piccolo

| Field       | Value          |
|-------------|----------------|
| **Status**  | planned        |
| **Priority**| high           |
| **Route**   | `/api/piccolo/` |

#### Concept

Reimplementation of the popular Piccolo party game — a social drinking/party game where players take turns and the app gives random challenges, dares, or questions directed at specific players.

#### Features

| Feature                   | Description                                          |
|--------------------------|------------------------------------------------------|
| Player name input         | Enter names of all participants                      |
| Random challenges         | App selects random tasks/dares/questions             |
| Player targeting          | Challenges reference specific players by name        |
| Category system           | Challenge types: dare, question, group, versus, etc. |
| Configurable intensity    | Mild / medium / spicy difficulty levels              |
| Offline capable           | Fully playable without internet after initial load   |

---

### 3. Wer wird Elite-Hater? (Quiz)

| Field       | Value          |
|-------------|----------------|
| **Status**  | planned        |
| **Priority**| high           |
| **Route**   | `/api/quiz/`   |

#### Concept

A quiz game with two play modes, featuring a community-driven question database. Initial thematic focus: **Drachenlord lore**. Users can create, tag, and rate questions. Questions have an ELO score based on difficulty.

#### Play Modes

| Mode                     | Description                                                              |
|--------------------------|--------------------------------------------------------------------------|
| **Wer wird Millionär**   | Single-player, escalating difficulty, lifelines, one wrong answer = game over |
| **Quizduell**            | 1v1 or multiplayer, category selection, alternating turns, score comparison  |

#### Features

| Feature                          | Description                                                              |
|---------------------------------|--------------------------------------------------------------------------|
| Question database                | Persistent DB with questions, correct answer, and multiple wrong answers |
| Arbitrary wrong answer pool      | Each question can have any number of wrong answers; app selects randomly |
| Categories                       | Questions can be assigned to categories                                  |
| Tags                             | Questions can be tagged freely (e.g., `schanze`, `mettigel`, `rundumschlag`) |
| User-submitted questions         | Users can add new questions with answer options (1 correct, N wrong)     |
| ELO score per question           | Difficulty rating calculated like chess tactic puzzles — harder questions gain ELO when answered wrong |
| Media attachments                | Questions can include short video clips, images, or documents            |
| Category/tag-based quizzes       | Create custom quizzes filtered by category or tag                        |
| Leaderboard                      | Track player scores and streaks                                          |

#### Data Model

| Entity          | Fields                                                                                    | Storage    |
|----------------|--------------------------------------------------------------------------------------------|------------|
| Question        | `id`, `text`, `category_id`, `elo_score`, `media_url`, `media_type`, `created_by`, `created_at` | PostgreSQL |
| Answer          | `id`, `question_id`, `text`, `is_correct`                                                  | PostgreSQL |
| Category        | `id`, `name`, `description`                                                                | PostgreSQL |
| Tag             | `id`, `name`                                                                               | PostgreSQL |
| QuestionTag     | `question_id`, `tag_id`                                                                    | PostgreSQL |
| Player          | `id`, `name`, `elo_score`, `games_played`, `correct_answers`                               | PostgreSQL |
| GameSession     | `id`, `mode`, `player_ids`, `score`, `started_at`, `finished_at`                           | PostgreSQL |
| QuestionAttempt | `id`, `session_id`, `question_id`, `player_id`, `answered_correctly`, `time_taken_ms`      | PostgreSQL |

#### ELO System

- Each question starts with a base ELO (e.g., 1200)
- When a player answers correctly → question ELO decreases, player ELO increases
- When a player answers wrong → question ELO increases, player ELO decreases
- In "Wer wird Millionär" mode, questions are ordered by ascending ELO
- Magnitude of ELO change depends on delta between player ELO and question ELO (like chess)

#### Initial Content Theme

- Focus: **Drachenlord / Rainer Winkler lore**
- Example categories: `Biografie`, `Schanze`, `Memes`, `Zitate`, `Rundumschläge`, `Community-Events`
- Media: short clips, screenshots, documents from the lore

---

### 4. Chess Variants (LiChess Extension)

| Field       | Value          |
|-------------|----------------|
| **Status**  | planned        |
| **Priority**| low            |
| **Route**   | `/api/chess/`  |

#### Concept

Custom chess variants inspired by LiChess. Primary idea: chess on a board with fewer rows (e.g., 6×8 or 7×8). Other rule modifications possible in the future.

#### Planned Variants

| Variant             | Description                                          |
|--------------------|------------------------------------------------------|
| Mini Chess (6×8)    | Standard rules, 6 rows instead of 8 — faster games  |
| Mini Chess (7×8)    | Standard rules, 7 rows — slightly less radical       |
| _Future variants_   | Custom piece rules, fog of war, etc.                 |

#### Notes

- Lowest priority of all games
- Evaluate whether to build from scratch or extend/fork an existing open-source chess engine
- LiChess is open source (AGPL) — check license compatibility before forking
- Could use `chess.js` or `python-chess` as engine backend

---

## Notes

- Inspired by the hometools streaming architecture (FastAPI + PWA + Service Worker)
- Each game should be playable offline after first load (especially Imposter & Piccolo)
- Future: GroupGame-App (from brainstorm), multiplayer support
- Quiz media files (clips, images) should be stored locally or on a lightweight file server — not in the DB
- Imposter & Piccolo are fully local/offline games; Quiz requires a backend for persistent data

## Links

- **GitHub:** https://github.com/ducktalez/playbox
- **Deployed:** _not deployed (local PWA)_
- **Architecture.md:** _to be created_

