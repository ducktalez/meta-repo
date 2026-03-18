# Technology Targets

> This document defines the target technology stacks, conventions, and principles that all sub-repositories should follow unless an explicit deviation is documented.

## Default Technology Stack

| Layer         | Target Technology         | Notes                              |
|---------------|---------------------------|------------------------------------|
| Frontend      | React (TypeScript)        | Preferred for all web UIs          |
| Backend       | FastAPI (Python)          | Preferred for all APIs             |
| Database      | PostgreSQL                | Default relational database        |
| ORM           | SQLAlchemy / SQLModel     | Preferred for Python backends      |
| Auth          | _To be defined_           | See identity concept in data-models|
| CSS/UI        | _To be defined_           | Evaluate Tailwind, MUI, etc.       |
| Deployment    | Docker                    | Containerized deployments          |
| CI/CD         | GitHub Actions            | Standard pipeline platform         |
| Version Ctrl  | Git / GitHub              | All repos on GitHub                |

## API Conventions

- RESTful APIs as default
- JSON request/response bodies
- API versioning via URL prefix (`/api/v1/...`)
- Consistent error response format:
  ```json
  {
    "detail": "Human-readable message",
    "code": "MACHINE_READABLE_CODE"
  }
  ```
- Use HTTP status codes correctly (200, 201, 400, 401, 403, 404, 409, 422, 500)

## Testing Strategy

- Unit tests required for business logic
- Integration tests for API endpoints
- Test framework: `pytest` (Python), `vitest` or `jest` (TypeScript)
- Aim for meaningful coverage, not 100% line coverage

## Logging & Observability

- Structured logging (JSON format in production)
- Log levels: DEBUG, INFO, WARNING, ERROR, CRITICAL
- Include correlation/request IDs where applicable
- _Centralized logging solution: to be defined_

## Code Style & Linting

- Python: `ruff` for linting and formatting
- TypeScript: `eslint` + `prettier`
- Pre-commit hooks recommended

## Deployment Conventions

- Docker-based deployments
- Environment configuration via environment variables (not hardcoded)
- Separate configurations for: `local`, `test`, `production`
- Health check endpoints: `GET /health`

## Project Structure Conventions

### Python / FastAPI

```
project-name/
├── app/
│   ├── api/           # Route handlers
│   ├── models/        # SQLAlchemy/SQLModel models
│   ├── schemas/       # Pydantic schemas
│   ├── services/      # Business logic
│   ├── core/          # Config, security, dependencies
│   └── main.py        # Application entry point
├── tests/
├── alembic/           # Database migrations
├── Dockerfile
├── requirements.txt
└── README.md
```

### React / TypeScript

```
project-name/
├── src/
│   ├── components/    # Reusable UI components
│   ├── pages/         # Page-level components
│   ├── hooks/         # Custom hooks
│   ├── services/      # API clients
│   ├── types/         # TypeScript types
│   ├── utils/         # Utility functions
│   └── App.tsx
├── tests/
├── Dockerfile
├── package.json
└── README.md
```

## Dependency Management

- Python: `requirements.txt` or `pyproject.toml`
- Node: `package.json` with `package-lock.json`
- Pin major versions, allow minor/patch updates
- Regular dependency update reviews

## Documentation Requirements

Every sub-repository must contain:

1. `README.md` — project overview, setup instructions, usage
2. `Architecture.md` — following the [architecture template](templates/architecture.md)
3. `Implementation-Plan.md` — following the [implementation plan template](templates/implementation-plan.md)
4. `.github/copilot-instructions.md` — following the [copilot instructions template](templates/copilot-instructions.md)

