---
name: dev-delivery
description: Prepare a bounded development change for execution or close it out against approved intent and evidence. Use for dev-packet readiness, review-route selection, delivery audits, and interrupted-work handoffs; not for ordinary brainstorming or as automatic release approval.
---

# Dev Delivery

Use readiness, closeout, or both. Work in the existing brief, issue or outcome;
do not create a parallel report. A narrow fix can need only a few lines. Project
policy and the owner's instructions govern; this skill grants no permissions.

## Readiness

1. Verify the repository, checkout, branch, dirty state and current decisions.
   Read the current handoff and relevant project guidance, not the whole archive.
   Establish one writer per checkout; a different branch name is not isolation.
2. Put intent above the implementation plan: desired outcome, inherited behavior
   to preserve, intended changes and material assumptions. Ask consequential
   choices that current records cannot answer. If instructed not to pause,
   document scoped assumptions; do not broaden authorization.
3. Define observable acceptance criteria and exclusions. For risky promises,
   pair the original request or approved reference with the expected result and
   suitable evidence. A proof must meet applicable experience guidance too.
   Check one representative integrated path before repeating a treatment widely.
4. Select a proportionate review and verification route using project policy.
   Name essential checks, deliberate deferrals, human judgment gates and stop
   conditions. Check readiness before expensive runs; tools, inputs and required
   permissions being present does not itself prove the behavior works.

## Review Routes

Preserve explicit overrides independently: draft-only stops implementation;
skip-review does not waive verification; no-pause does not waive authority.

- Narrow, preapproved fix: focused implementation and checks can suffice.
- Material design choice: owner clarification or review before execution.
- Experience or visual change: representative proof and human judgment before
  broad verification. Component presence alone does not prove a visual match.
- Cross-system or repeated recovery: consider an authorized independent review.
- Publication, merge or release: use the project's separate approval gates.

An existing owner-approved policy can authorize a named review route. Otherwise ask
before messaging a chat or delegating. Do not create reviewers automatically.
Reviewers compare original intent and evidence, not just the plan's paraphrase.
Their agreement is not owner acceptance or permission to expand the work.

## Closeout

1. Compare acceptance promises to actual artifacts at an identified revision.
   For presentation, compare representative states with approved references;
   for behavior, exercise the real path rather than only a test substitute.
2. Report failures, deviations, unrun checks and prior evidence reused. Preserve
   the first failure if reporting or cleanup also fails; label secondary errors.
   Distinguish product, test-driver, environment and unknown causes before retrying.
   Carry forward attempt limits, remaining budget, holds and protected evidence.
3. Separate implemented, verified, human-accepted and integrated/released states.
   Missing evidence is unverified, not a pass or an invented defect. Keep initial
   misses and required steering visible after recovery. An unmet core promise is
   not optional polish.
4. Update the current documentation owner and compact handoff: exact source,
   remaining limits, next action, and human-editable tuning points when useful.
   If the project measures delivery, use its existing definitions and records;
   do not invent scores, new test runs or a measurement program for this skill.

Use scripts for repeatable mechanics and judgment for intent, risk and usability.
On interruption, preserve state and restrictions rather than restarting counters
or assuming that another chat's memory contains the missing context.
