# Automation

> **Status: Planned** — This area is reserved for future agent-based automation and orchestration.

## Scope

The automation system will enable prioritized, semi-automated or fully automated maintenance and development tasks across all sub-repositories. The meta-repo serves as the coordination layer that provides context, priorities, and rules to automation agents.

## Planned Capabilities

### Prioritized Task Execution

- Agents receive priorities from the meta-repo catalog
- Higher-priority repositories are processed first
- Scope of allowed changes is defined per repository

### Repository Analysis

- Automated analysis of sub-repos for:
  - Technology drift from meta-repo standards
  - Missing or outdated documentation
  - Dependency updates needed
  - Unused or deprecated patterns
  - Alignment with core entity definitions

### Automated Maintenance

- Documentation updates (sync with templates)
- Dependency version bumps
- Linting and formatting fixes
- Boilerplate updates

### Cross-Repo Improvements

- Detect improvements in one repo that could benefit others
- Propose changes via pull requests
- Track adoption of improvements across the ecosystem

### Change Governance

- Agents respect deviation records
- Changes follow defined standards
- All automated changes are submitted as PRs for review

## Per-Repository Configuration

Each catalog entry may define:

| Field              | Description                                        |
|--------------------|----------------------------------------------------|
| `automation_level` | `none` · `basic` · `full`                          |
| `allowed_actions`  | What types of changes agents may make              |
| `priority`         | Processing priority relative to other repos        |
| `review_required`  | Whether automated PRs need manual approval         |

## Open Questions

- Which agent framework to use? (GitHub Actions, custom agents, AI-based?)
- How to authenticate agents across repositories?
- What is the minimal viable first automation?
- How to handle failures and rollbacks?

## Next Steps

1. Define the first automatable task (e.g., documentation sync)
2. Choose an automation approach
3. Implement a proof-of-concept for one repository
4. Expand based on learnings

