# Workflow

## Bootstrap

1. Read the handoff and project profile.
2. Inspect the repository, worktree, dependencies, and existing verification surfaces.
3. Identify missing project facts instead of inventing domain assumptions.
4. Define the smallest milestone that produces an observable result.
5. Record any domain-specific rules in a separate profile.

## Work Contract

Use this shape for material work:

```text
Objective:
Scope:
Out of scope:
Observable result:
Acceptance criteria:
Verification:
Stop conditions:
```

Keep the contract proportional. A narrow fix may need one sentence; architecture, scope, data migration, paid services, hardware, or unresolved product behavior deserves a deliberate plan.

## Execution Loop

1. Inspect before editing.
2. Implement the smallest coherent change.
3. Verify the changed behavior and relevant regressions.
4. Review the diff for scope, secrets, generated churn, and accidental rewrites.
5. Report what changed, what passed, what was not tested, and how to continue.
6. Update handoff, decisions, or incidents only when durable context changed.

## Scope Control

- New features, frameworks, services, shared abstractions, or major polish require an explicit scope decision.
- A scope change names its value, cost, risk, and what it displaces.
- Feedback is a decision input, not automatic implementation permission when product behavior or scope remains unresolved.
- Prefer completing or shelving a bounded milestone over polishing indefinitely.

## Verification And Handoff

- Verification depth scales with blast radius and reversibility.
- Use bounded commands and explicit pass markers for asynchronous tools.
- An exit code alone is insufficient when logs can contain warnings or failures.
- Human review remains authoritative for taste, physical-device comfort, usability, and other experiential judgments.
- Never claim a check passed when it was skipped, timed out, or exercised a different surface.
- Before handoff, inspect the exact artifact or behavior the human will review.

A handoff includes:

- Changed files or behavior.
- Verification performed and results.
- Known limitations and unverified areas.
- Exact run or review instructions.
- The next recommended decision.

## External Services And Spend

Remote generation, metered APIs, paid services, and usage-limited trials have a default budget of zero.

Before any call, present:

- The exact service and operation.
- Inputs and whether they contain private data.
- Expected outputs.
- Maximum calls, credits, or currency.
- Current known balance when relevant.
- The human review stop point.

Approval applies only to that written sequence. Retries, polling that consumes quota, extra candidates, changed inputs, or fallback services require fresh approval unless explicitly included.

## Secrets

- Keep secrets in approved local environment or credential stores.
- Commit only documented placeholders such as `.env.example`.
- Never print secrets into chat, logs, screenshots, reports, or Git history.
- Treat accidental exposure as an incident and rotate the credential before continuing.

## Subagent Lifecycle

Subagents default to off. A plan approval, high-effort request, or permission to use tools is not delegation authorization.

1. State the bounded purpose and expected count.
2. Receive explicit human authorization for the current task.
3. Record each returned id and purpose.
4. Collect the result once and assess it.
5. Close the subagent immediately, including completed, errored, interrupted, or abandoned agents.
6. Audit all task-owned collaborators before the parent response.
7. If state cannot be verified or closed, disclose the exception and record an incident instead of reporting a clean closeout.

## Git Checkpoints

- Work on a focused branch unless the project profile explicitly uses another model.
- A working branch has one active machine or contributor owner at a time. Transfer ownership only after a clean, pushed checkpoint records the exact branch and commit.
- Multiple machines or contributors may work concurrently on separate branches, but exactly one coordinated integration operation may advance the shared `main` branch at a time.
- Before advancing `main`, fetch the remote state, confirm the intended accepted branches or tags, integrate them one at a time, rerun the relevant verification, and confirm the pushed remote SHA. Other machines fetch and reconcile after that push before beginning another integration.
- An unpushed local `main` commit is not shared state. If integration pauses, preserve the candidate on a named branch and restore local `main` to the remote tip so another machine cannot mistake the candidate for accepted repository state.
- When the repository supports pull requests, open a draft early for concurrent work. Record the source branch, base `main` SHA, branch owner, intended integration owner, verification, and unresolved dependencies there.
- Do not use force-push, destructive reset, or automatic conflict resolution as a machine-synchronization mechanism.
- Commit accepted milestones, pre-risk restore points, and intentional pauses.
- Do not mix unrelated user work into a commit.
- Before integration, verify the accepted commit, relevant tests, clean diff, and remote state.
- Use an immutable tag for releases, shelves, archives, or other important return points.
- Delete dormant branches after their accepted tips are integrated and protected, unless the handoff records a reason to retain them.

Follow `_project/MACHINE_CONTINUITY.md` when moving work between machines, coordinating concurrent branches, pausing an integration, or recovering from stale or divergent state.

## Timeouts And Failures

- Bound long-running commands and native tools.
- Retry only with a changed hypothesis or a meaningful alternate path.
- Report the timeout, likely cause, workaround, and remaining uncertainty.
- Record an incident when a failure reveals a reusable operational gap, not for every ordinary bug.
