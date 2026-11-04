# Agent Guidance

Read `_project/HANDOFF.md` first for current state and restart context.

Read these next when relevant:

- `_project/PROJECT_PROFILE.md` for purpose, stack, constraints, and commands
- `_project/WORKFLOW.md` for scope, verification, authorization, and closeout
- `_project/DEV_BRIEF_TEMPLATE.md` when defining a material change's Work Contract
- `_project/MACHINE_CONTINUITY.md` for cross-machine state, branch ownership, and integration
- `_project/ARCHITECTURE.md` for ownership, structure, and refactor triggers
- `_project/DECISIONS.md` for durable project choices
- `_project/INCIDENTS.md` for unresolved or recurring operational failures

Operating rules:

- Inspect the repository before proposing or making changes.
- Do not import assumptions, conventions, or state from another repository.
- Keep work bounded by a stated objective, exclusions, and acceptance criteria.
- Prefer the repository's existing patterns and tools over new abstractions.
- Give each meaningful behavior one clear owner and keep policy separate from adapters and presentation.
- Verify changes at a depth appropriate to their risk; report anything not verified.
- Never expose secrets or commit local credentials, tokens, private keys, or machine-specific configuration.
- Treat Git refs plus `_project/HANDOFF.md` as canonical across machines; never synchronize raw Codex state or credentials between hosts.
- Give each active writer a separate checkout/worktree and owned branch; different branches in the same folder are not isolation. One coordinated integration owner advances shared `main`.
- Treat metered services and remote generation as zero-budget until the human explicitly approves an exact call sequence and maximum spend.
- Default to zero subagents. Do not spawn one unless the human explicitly authorizes a bounded delegation in the current task after its purpose and expected count are stated.
- For every authorized subagent, record its id, purpose, and authorization; close it immediately after collecting its result; audit that no task-owned collaborator remains open before the parent task finishes.
- Treat any unknown or UI-reported collaborator as an incident until its identity and runtime state are resolved.
- Update project memory only when a fact, decision, or lesson should survive a new chat.

The optional `.agents/skills/dev-delivery/SKILL.md` guides readiness and closeout.
It follows project policy; it does not grant review, delegation or publication authority.
