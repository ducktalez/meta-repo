# your-match-backend

## Metadata

| Field                  | Value                                  |
|------------------------|----------------------------------------|
| **Name**               | your-match-backend                     |
| **Purpose**            | Backend API for the Your-Match platform |
| **Status**             | maintenance                            |
| **Priority**           | medium                                 |
| **Tech Stack**         | FastAPI (Python), SQLAlchemy, Alembic, PostgreSQL |
| **Architecture Type**  | monolith                               |
| **Database**           | PostgreSQL                             |
| **Auth Model**         | TBD                                    |
| **Documentation Status** | partial                              |
| **Monitoring Relevant** | yes                                   |
| **Automation Level**   | none                                   |
| **Infrastructure Refs** | —                                     |

## Deviations

| Standard                     | Deviation        | Reason              | Accepted | Temporary |
|-----------------------------|------------------|----------------------|----------|-----------|
| GitHub as default host       | Hosted on GitLab | Legacy project       | yes      | yes       |
| Poetry instead of pip        | Uses Poetry      | Team preference      | yes      | no        |

## Core Entity Alignment

| Entity       | Aligned | Notes                        |
|-------------|---------|------------------------------|
| User        | ⬜ No   | Custom user model            |
| Role        | ⬜ No   | TBD                          |
| Organization| ⬜ No   | TBD                          |

## Notes

- Structured FastAPI app: `app/api`, `app/core`, `app/crud`, `app/db`, `app/models`, `app/schemas`
- Database migrations with Alembic
- Poetry for dependency management
- Collaborative project (multiple authors)

## Links

- **GitLab:** https://gitlab.com/your-match/your-match-backend
- **Deployed:** _unknown_
- **Architecture.md:** _not yet created_

