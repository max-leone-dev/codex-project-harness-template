# Workflow

## Bootstrap

1. Read the handoff and project profile.
2. Inspect the repository, worktree, dependencies, and existing verification surfaces.
3. Identify missing project facts instead of inventing domain assumptions.
4. Define the smallest milestone that produces an observable result.
5. Record any domain-specific rules in a separate profile.

## Work Contract

Use the [dev brief](DEV_BRIEF_TEMPLATE.md) as the Work Contract for material work,
or put the same essentials in an existing issue: intent, preserved behavior,
scope/exclusions, acceptance evidence, review route, verification and stop conditions.
Keep intent above the implementation plan so the owner can correct a mistaken
interpretation without reading the entire plan. A dev-packet is this brief plus
necessary linked references, not a second form.

Keep the contract proportional. A narrow fix may need one sentence; architecture, scope, data migration, paid services, hardware, or unresolved product behavior deserves a deliberate plan.

## Review And Questions

Use the review policy in the project profile and the owner's explicit request.
Owner review, an authorized peer, direct execution of a small preapproved fix,
or a combination can all be valid. Do not require a permanent review chat or
create/message reviewers without authorization. Review agreement does not
expand implementation scope or replace required owner acceptance.

Ask about consequential choices that existing decisions do not answer. Do not
ask the owner to repeat settled behavior. If explicitly told not to pause, record
bounded assumptions; stop anyway at a required permission or safety boundary.
Draft-only, skip-review and no-pause overrides are independent, not blanket waivers.

For risky promises, reviewers compare the original request or approved reference
with the planned observable result, not merely the brief's paraphrase. Record
findings and dispositions in the same brief. Unmet core intent is not optional polish.

## Execution Loop

1. Inspect before editing.
2. Implement the smallest coherent change; check a risky representative integrated path before expanding it across content or surfaces.
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
- A prototype or proof may limit scope, but must preserve agreed behavior and
  applicable experience standards within that scope. For visuals, compare actual
  user-facing states with approved references, not just component presence.
- Before costly runs, check commands, dependencies, fixtures, permissions and
  applicable budgets/holds using cheap read-only checks where possible. Readiness
  is not a test pass or permission to run. Follow the project's attempt-counting
  policy; never reset limits by relabeling execution as a preflight.
- Split checks into essential now, consciously deferred, and human judgment.
  Start with a short real-path check; use focused regressions after it works.
  Count new attempts and carry restrictions forward across chats and interruptions.

A handoff includes:

- Changed files or behavior.
- Verification performed and results.
- Known limitations and unverified areas.
- Exact run or review instructions.
- The next recommended decision.

Use the [report template](DEV_REPORT_TEMPLATE.md) only if the brief does not already
hold the outcome. Distinguish implemented, verified, human-accepted and
integrated/released. Preserve original misses and required steering after a fix;
absence of evidence is not a pass, a zero, or proof that a defect exists.

## Documentation Freshness

Keep one current owner for each material fact. Update affected guidance and its
entry links when behavior changes; do not turn every change into a historical
audit. Keep `HANDOFF.md` a compact current-state brief with exact next action and
remaining limits. Replace stale instructions; link detailed outcomes and leave
history in Git. Load older records only when the current task needs them.

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
- Concurrent writers need separate checkouts/worktrees as well as owned branches. Exactly one coordinated integration operation may advance shared `main` at a time.
- Before advancing `main`, fetch the remote state, confirm the intended accepted branches or tags, integrate them one at a time, rerun the relevant verification, and confirm the pushed remote SHA. Other machines fetch and reconcile after that push before beginning another integration.
- An unpushed local `main` commit is not shared state. If integration pauses, preserve the candidate on a named branch and restore local `main` to the remote tip so another machine cannot mistake the candidate for accepted repository state.
- When the repository supports pull requests, open a draft early for concurrent work. Record the source branch, base `main` SHA, branch owner, intended integration owner, verification, and unresolved dependencies there.
- Do not use force-push, destructive reset, or automatic conflict resolution as a machine-synchronization mechanism.
- Commit accepted milestones, pre-risk restore points, and intentional pauses.
- Stage explicit files or hunks and inspect the full staged diff. Do not mix another writer's unfinished work into a commit, even when it shares a filename.
- Prepare a PR at accepted-work closeout when the project's publication policy authorizes it. Acceptance, push, merge and release are distinct gates; never infer public disclosure permission from private implementation approval.
- Before integration, verify the accepted commit, relevant tests, clean diff, and remote state.
- Use an immutable tag for releases, shelves, archives, or other important return points.
- Delete dormant branches after their accepted tips are integrated and protected, unless the handoff records a reason to retain them.

Follow `_project/MACHINE_CONTINUITY.md` when moving work between machines, coordinating concurrent branches, pausing an integration, or recovering from stale or divergent state.

## Timeouts And Failures

- Bound long-running commands and native tools.
- Retry only with a changed hypothesis or a meaningful alternate path.
- Diagnose product behavior, test-driver/fixture problems, environment/readiness
  failures or unknown causes before spending another attempt. Do not weaken an
  assertion merely to pass. Keep the first diagnostic if logging or cleanup also
  fails, and report those secondary errors separately.
- Report the timeout, likely cause, workaround, and remaining uncertainty.
- Record an incident when a failure reveals a reusable operational gap, not for every ordinary bug.
