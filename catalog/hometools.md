# hometools

## Metadata

| Field                  | Value                                  |
|------------------------|----------------------------------------|
| **Name**               | hometools                              |
| **Purpose**            | Personal media library tools — music sanitization, video organizing (TMDB), local audio & video streaming |
| **Status**             | active                                 |
| **Priority**           | high                                   |
| **Tech Stack**         | Python, FastAPI, PWA                   |
| **Architecture Type**  | monolith                               |
| **Database**           | None (file-based)                      |
| **Auth Model**         | None                                   |
| **Documentation Status** | complete                             |
| **Monitoring Relevant** | yes                                   |
| **Automation Level**   | basic                                  |
| **Infrastructure Refs** | —                                     |

## Deviations

| Standard                     | Deviation        | Reason              | Accepted | Temporary |
|-----------------------------|------------------|----------------------|----------|-----------|
| React + FastAPI default stack | No React frontend | PWA with vanilla JS / service workers | yes | no |

## Core Entity Alignment

| Entity       | Aligned | Notes                        |
|-------------|---------|------------------------------|
| User        | ⬜ No   | Single-user tool             |
| Role        | ⬜ No   | Not applicable               |
| Organization| ⬜ No   | Not applicable               |

## Notes

- Offline-first PWA with Service Worker, IndexedDB, download UI
- iOS/iPad tested — see `docs/ios/`
- Pre-commit hooks, Makefile, ruff linting configured
- Key dependencies: FastAPI, pydub, mutagen, tmdbv3api, httpx

## Links

- **GitHub:** https://github.com/ducktalez/hometools
- **Deployed:** _local only_
- **Architecture.md:** _not yet created_

