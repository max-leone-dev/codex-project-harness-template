# Machine Continuity

## Purpose

Use Git plus `_project/HANDOFF.md` as the durable state shared across computers and contributors. A live chat, editor window, local checkout, or native task handoff may help someone resume, but none of them replaces a reviewed repository checkpoint.

This document assumes a Git remote named `origin` and a shared default branch named `main`. Record different names in the project profile and apply the same rules consistently.

## Durable And Local State

Durable shared state includes:

- reviewed commits, branches, and annotated tags;
- the remote ref and exact commit expected on another host;
- `_project/HANDOFF.md` and other committed project records;
- pull requests, reviews, and verification attached to a contribution;
- intentionally committed source, tests, configuration, and documentation.

Host-local state includes:

- checkout paths, editor state, unsaved buffers, and running processes;
- credentials, tokens, SSH keys, keychains, and authentication helpers;
- Codex session databases, task history, locks, caches, attachments, and application configuration;
- ignored logs, build outputs, dependency caches, and device state;
- tools or SDKs installed only on one machine.

Never copy or synchronize raw Codex state, credentials, locks, or caches between hosts. Set up and authenticate each host independently. Put only documented placeholders and repository-relative paths in durable files.

## Branch Ownership

- One machine or contributor owns a working branch at a time.
- Multiple machines may work concurrently when they use separate branches.
- Do not make independent commits on the same branch and use force-push or conflict automation to pretend the histories were one stream.
- Transfer branch ownership only after the departing owner commits, pushes, verifies the remote SHA, and records the checkpoint.
- Treat an unpushed commit as local recovery state, not shared project state.
- Open a draft pull request early when concurrent contributors need a shared status surface. Keep its base SHA, branch owner, verification, unresolved dependencies, and integration readiness current.

## Host Setup

Before a host participates, verify:

1. The checkout points at the intended remote repository.
2. Git authentication succeeds without relying on another computer.
3. The required runtime, SDKs, and project tools from `_project/PROJECT_PROFILE.md` are installed.
4. Machine-specific paths and credentials are excluded from version control.
5. `AGENTS.md`, the project profile, workflow, handoff, decisions, and applicable domain guidance are readable.

Record supported-platform evidence honestly. Successful work on one operating system is not proof that another host or platform works.

## Departure Checkpoint

Before stopping on one machine or transferring branch ownership:

1. Stop active edits and save all intended files.
2. Update `_project/HANDOFF.md` with accepted state, active branch, owner or host, blockers, and one exact next action.
3. Run verification appropriate to the change.
4. Review `git status` and the complete diff for scope, secrets, generated churn, and unrelated work.
5. Create one coherent commit and push its branch.
6. Confirm the remote branch resolves to the same commit.
7. Record the branch and full commit SHA as the departure receipt.

Useful read-only checks include:

```text
git status --short --branch
git remote -v
git rev-parse HEAD
git rev-parse '@{upstream}'
```

A successful push is not enough if the handoff is stale, required local assets are missing, or the remote ref was not verified.

## Arrival Checkpoint

Before editing on another machine:

1. Verify that the checkout is the intended repository and has no unresolved local work.
2. Fetch remote refs and inspect the active branch, upstream, and commit.
3. Fast-forward only to the expected remote checkpoint. Stop on divergence, unpublished commits, conflicts, or an unexpected branch.
4. Confirm the branch and full commit SHA match the departure receipt.
5. Read `AGENTS.md`, `_project/HANDOFF.md`, the project profile, and any status document named there.
6. Verify required ignored assets, tools, SDKs, or device setup separately.
7. Resume only the recorded next action or deliberately establish a new work contract.

Do not reset a destination checkout merely to make it resemble the source. Preserve unexpected work on a separate branch and reconcile it explicitly.

## Concurrent Work And Integration

Many branches may progress at the same time. Shared `main` has one integration owner during each merge window.

1. Each contributor branches from a known `origin/main` commit and records that base in the draft pull request or handoff.
2. Contributors push only their owned branches while work is under review.
3. Before integration, the designated owner fetches current refs and reviews all known active contributions for dependency or overlap.
4. Integrate one accepted branch or tag at a time into the latest `main`.
5. Resolve conflicts deliberately, rerun relevant verification, and present the exact candidate commit for human approval when the project requires it.
6. Push `main` once, then verify that the remote SHA equals the approved local result.
7. Other machines fetch and reconcile with that new `main` before another integration begins.
8. Remove integrated branches unless the handoff records a concrete retention reason.

The integration owner is temporary. Naming an owner for one merge does not grant permanent authority over future integrations.

## Paused Integration

An integration candidate may need to wait while another machine is active:

1. Preserve the candidate on a clearly named branch.
2. Push and verify that branch.
3. Restore local `main` to the current remote tip without deleting the preserved candidate.
4. Record the candidate branch and reason for pausing in the handoff or draft pull request.
5. Reconcile it with the latest `main` before later approval.

No other machine should infer that a local-only `main` commit is accepted shared state.

## Native Task Handoff

Use a product-native task or chat handoff only as an optional convenience when both hosts support it. Complete the Git departure checkpoint first and perform the arrival checkpoint afterward.

Native handoff may carry conversational context. It does not guarantee transfer of ignored files, credentials, editor state, tools, device state, external repositories, or uncommitted changes. A fresh task on the destination must still be able to resume from Git and the project handoff alone.

## Failure And Recovery

Cross-machine and multi-repository updates are not automatically atomic.

- If a push, fetch, merge, or transfer fails, report which refs changed and which steps did not complete.
- Inspect local and remote branch SHAs before retrying.
- Retry only after the failure is understood or the approach changes.
- Preserve unexpected local commits on a branch before repairing tracking state.
- Never conceal divergence with force-push, destructive reset, or silent conflict selection.
- Record an incident when the failure reveals a reusable operational gap.

A recovery is complete only when the intended worktree is clean, the expected remote ref matches the verified commit, and the handoff describes the state another host will actually receive.

## Harness Self-Governance

Shared harnesses, templates, and infrastructure repositories follow the same rules they publish. Maintain them through focused branches and draft pull requests, keep one owner per branch, use one integration owner for `main`, verify the remote result, and let other hosts reconcile before continuing their own contribution.
