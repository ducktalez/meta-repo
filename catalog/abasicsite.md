# abasicsite

## Metadata

| Field                  | Value                                  |
|------------------------|----------------------------------------|
| **Name**               | abasicsite                             |
| **Purpose**            | Collection of small web projects (blog, quiz, portfolio, toy shop) with shared auth |
| **Status**             | maintenance                            |
| **Priority**           | low                                    |
| **Tech Stack**         | Python, FastAPI                        |
| **Architecture Type**  | monolith                               |
| **Database**           | SQLite (assumed)                       |
| **Auth Model**         | Custom (auth.py)                       |
| **Documentation Status** | missing                              |
| **Monitoring Relevant** | no                                    |
| **Automation Level**   | none                                   |
| **Infrastructure Refs** | —                                     |

## Deviations

| Standard                     | Deviation        | Reason              | Accepted | Temporary |
|-----------------------------|------------------|----------------------|----------|-----------|
| React + FastAPI default stack | No frontend framework | Simple static sub-projects | yes | no |

## Core Entity Alignment

| Entity       | Aligned | Notes                        |
|-------------|---------|------------------------------|
| User        | ⬜ No   | Custom auth.py               |
| Role        | ⬜ No   | Not implemented              |
| Organization| ⬜ No   | Not applicable               |

## Notes

- Contains multiple sub-projects: blog, portfolio, quiz, toy shop, tutorial
- Single-file FastAPI backend with shared auth and database modules

## Links

- **GitHub:** https://github.com/ducktalez/abasicsite
- **Deployed:** _not deployed_
- **Architecture.md:** _not yet created_

