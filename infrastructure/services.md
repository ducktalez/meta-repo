# Services

> Central documentation of all services, their host assignments, and environment configurations.

## Overview

| Service Name | Repository | Host         | Environment | Port  | Status  |
|-------------|-----------|--------------|-------------|-------|---------|
| _example_   | _repo_    | _host name_  | _prod/test_ | _8000_| _active_|

<!-- Add services as they are documented -->

## Service Details

### [Service Name]

- **Repository:** Link to catalog entry or GitHub URL
- **Host:** Link to [hosts.md](hosts.md) entry
- **Technology:** e.g., FastAPI, React, PostgreSQL
- **Port:** _port number_
- **URL:** _access URL (if applicable)_
- **Health Check:** `GET /health` or _describe_
- **Environment:** Production / Test / Local
- **Dependencies:** Other services this depends on
- **Database:** Database name and host
- **Configuration:** Environment variables or config files needed
- **Status:** Running / Stopped / Degraded
- **Notes:** _any additional context_

<!-- Copy the section above for each service -->

## Environment Matrix

| Service      | Local         | Test          | Production    |
|-------------|---------------|---------------|---------------|
| _example_   | localhost:8000| test.example  | prod.example  |

## Service Dependencies

```
[Service A] ──depends on──> [Database X]
[Service B] ──depends on──> [Service A]
[Service C] ──depends on──> [Database X]
```

<!-- Update the dependency graph as services are added -->

