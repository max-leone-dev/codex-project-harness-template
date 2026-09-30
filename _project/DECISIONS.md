# Decisions

Record only choices that should survive a new task. Routine implementation details belong in code and Git history.

## Harness Baseline

- Repository files are the durable source of project context.
- Domain-specific rules extend this harness through separate profile documents.
- Work is bounded by observable outcomes and explicit acceptance criteria.
- External spend and subagent delegation require exact, current-task human approval.
- Git refs plus `_project/HANDOFF.md` are the durable cross-machine state; raw Codex sessions, credentials, paths, and caches remain host-local.
- A working branch has one active owner at a time, and one coordinated integration operation advances shared `main`.

## Decision Template

### YYYY-MM-DD - Decision Title

- **Status:** Proposed | Accepted | Superseded
- **Context:** What forced the decision.
- **Decision:** The chosen rule or direction.
- **Consequences:** Benefits, costs, constraints, and follow-up.
- **Supersedes:** Prior decision, if any.
