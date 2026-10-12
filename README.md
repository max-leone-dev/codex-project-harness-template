# Codex Project Harness Template

A small, project-agnostic operating harness for developing with Codex. It gives a new repository durable context, bounded execution rules, architecture guidance, verification expectations, and clean handoffs without imposing a language, framework, or product methodology.

This is the reusable base layer. Each repository adds its own domain profile for Unity, OpenXR, web development, data work, games, or another specialty.

## What It Provides

- `AGENTS.md`: the always-loaded entry point for Codex.
- `_project/HANDOFF.md`: current state and restart context.
- `_project/PROJECT_PROFILE.md`: project purpose, stack, commands, constraints, and definition of done.
- `_project/WORKFLOW.md`: bounded work, verification, external-service consent, and closeout rules.
- `_project/MACHINE_CONTINUITY.md`: durable cross-machine state, branch ownership, transfer checkpoints, and integration rules.
- `_project/ARCHITECTURE.md`: lightweight ownership and structure guidance.
- `_project/DECISIONS.md`: durable project decisions.
- `_project/INCIDENTS.md`: operational failures and verified resolutions.
- `_project/DEV_REPORT_TEMPLATE.md`: concise implementation handoff format.

## Start A Project

1. Select **Use this template** on GitHub and create the new repository.
2. Replace the placeholders in `_project/PROJECT_PROFILE.md`.
3. Set the initial state in `_project/HANDOFF.md`.
4. Add domain-specific guidance as a separate document, such as `_project/XR_PROFILE.md`.
5. Remove this setup section or adapt the README to describe the real project.
6. Commit the customized harness before beginning implementation.

A useful opening request for a fresh Codex task is:

```text
Read AGENTS.md and _project/HANDOFF.md first, followed by the project profile,
workflow, architecture, and decisions. Do not import assumptions from other
repositories. Inspect this repository, summarize its current state, and help
me define the smallest useful first milestone. Do not implement, spend money,
call metered services, or spawn subagents until the project contract is clear.
```

## Design Principles

- Project facts live in the repository, not only in chat history.
- Work begins with a bounded objective and explicit acceptance criteria.
- Each meaningful behavior has one clear owner.
- Verification scales with risk and is reported honestly.
- Concurrent contributors isolate work on branches while one coordinated integration owner advances shared `main`.
- Git and the project handoff carry durable context across machines; credentials, local paths, and raw Codex state remain host-local.
- External spend, remote generation, and delegation require explicit approval.
- Decisions and incidents are recorded only when they should survive a new task.
- Domain rules extend the generic harness instead of being baked into it.

## When To Change The Template

Change this base only when a rule has proven useful across materially different projects. Put framework-, product-, hardware-, or team-specific rules in the consuming repository instead.

## License

MIT. See `LICENSE`.
