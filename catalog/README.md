# Repository Catalog

This directory contains one Markdown file per managed sub-repository. Each file provides a structured overview of the repository's purpose, status, technology, and alignment with meta-repo standards.

## How to Add a Repository

1. Copy `_example-repo.md` and rename it to match the repository name (e.g., `my-project.md`)
2. Fill in all sections
3. Submit a pull request to the meta-repo

## Catalog Entry Format

Every catalog entry should contain the following sections:

### Metadata Table

| Field                  | Description                                              |
|------------------------|----------------------------------------------------------|
| **Name**               | Repository name                                          |
| **Purpose**            | One-sentence description of what the project does        |
| **Status**             | `active` · `maintenance` · `archived` · `planned`       |
| **Priority**           | `high` · `medium` · `low`                                |
| **Tech Stack**         | Key technologies (e.g., React, FastAPI, PostgreSQL)      |
| **Architecture Type**  | `monolith` · `microservice` · `library` · `cli` · `static` |
| **Database**           | Database engine(s) used                                  |
| **Auth Model**         | Auth approach (e.g., JWT, session, OAuth, none)          |
| **Documentation Status** | `complete` · `partial` · `missing`                     |
| **Monitoring Relevant** | `yes` · `no`                                            |
| **Automation Level**   | `none` · `basic` · `full`                                |
| **Infrastructure Refs** | Links to relevant infrastructure entries                |

### Additional Sections

- **Deviations** — list of deviations from meta-repo standards
- **Notes** — any additional context
- **Links** — GitHub URL, deployed URL, related docs

## Catalog Index

_Update this list as repositories are added._

| Repository | Status | Priority | Stack |
|-----------|--------|----------|-------|
| [abasicsite](abasicsite.md) | maintenance | low | Python, FastAPI |
| [dialectree](dialectree.md) | active | high | React, FastAPI, PostgreSQL |
| [hometools](hometools.md) | active | high | Python, FastAPI, PWA |
| [job-application-hub](job-application-hub.md) | active | medium | Markdown, Python |
| [pictasia](pictasia.md) | maintenance | low | FastAPI, PostgreSQL, Pillow |
| [plagih](plagih.md) | active | high | Python, NumPy, SymPy |
| [retailer-ml-prediction](retailer-ml-prediction.md) | archived | low | Python, TensorFlow, scikit-learn |
| [your-match-backend](your-match-backend.md) | maintenance | medium | FastAPI, SQLAlchemy, PostgreSQL |
| [_Example Repo (template)](_example-repo.md) | — | — | — |

<!-- Add new entries above this line -->


