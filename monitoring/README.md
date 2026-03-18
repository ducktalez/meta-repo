# Monitoring

> **Status: Planned** — This area is reserved for a future monitoring and health overview system.

## Scope

The monitoring system will provide a unified view of all services and systems across the ecosystem. It is intended to answer these questions at a glance:

- Is each service running?
- Are there known problems or degraded states?
- Are there critical TODOs or unresolved warnings?
- What is the overall health of the ecosystem?

## Planned Features

### Service Health

- Automated health checks against service endpoints (`GET /health`)
- Status tracking: `healthy` · `degraded` · `down` · `unknown`
- History of status changes

### Problem Tracking

- Known issues per service or host
- Severity levels: `critical` · `warning` · `info`
- Link to related issues or catalog entries

### Dashboard

- Overview page showing all services and their current status
- Filter by status, host, environment, or priority
- Alerts for status changes

### Integration with Catalog

- Each service in the catalog references its monitoring entry
- Monitoring status visible in the catalog overview

## Open Questions

- What technology for health checks? (Simple script, Uptime Kuma, custom service?)
- Where to host the monitoring dashboard?
- How to handle alerts and notifications?
- Should monitoring data be stored in this repo or in a separate system?

## Next Steps

1. Define a minimal health check format for all services
2. Choose a monitoring approach
3. Implement a basic status page or dashboard
4. Integrate with the catalog and infrastructure documentation

