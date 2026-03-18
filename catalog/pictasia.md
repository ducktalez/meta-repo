# pictasia

## Metadata

| Field                  | Value                                  |
|------------------------|----------------------------------------|
| **Name**               | pictasia                               |
| **Purpose**            | Image management platform with backend API and frontend |
| **Status**             | maintenance                            |
| **Priority**           | low                                    |
| **Tech Stack**         | FastAPI (Python), PostgreSQL, Pillow   |
| **Architecture Type**  | monolith                               |
| **Database**           | PostgreSQL                             |
| **Auth Model**         | JWT (python-jose + passlib)            |
| **Documentation Status** | missing                              |
| **Monitoring Relevant** | no                                    |
| **Automation Level**   | basic                                  |
| **Infrastructure Refs** | —                                     |

## Deviations

| Standard                     | Deviation        | Reason              | Accepted | Temporary |
|-----------------------------|------------------|----------------------|----------|-----------|
| GitHub as default host       | Hosted on GitLab | Legacy project       | yes      | yes       |

## Core Entity Alignment

| Entity       | Aligned | Notes                        |
|-------------|---------|------------------------------|
| User        | ⬜ No   | Custom user model            |
| Role        | ⬜ No   | Not implemented              |
| Organization| ⬜ No   | Not applicable               |

## Notes

- Backend: FastAPI + SQLAlchemy + PostgreSQL
- Frontend: separate directory (framework TBD)
- GitLab CI pipeline configured (`.gitlab-ci.yml`)
- Key dependencies: FastAPI, SQLAlchemy, psycopg2, Pillow, aiofiles

## Links

- **GitLab:** https://gitlab.com/your-match/pictasia
- **Deployed:** _not deployed_
- **Architecture.md:** _not yet created_

