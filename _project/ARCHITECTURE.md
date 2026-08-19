# Architecture

## Philosophy

Use the smallest structure that gives every meaningful responsibility an obvious home. Lightweight does not mean one large file; it means every abstraction must solve a demonstrated problem.

## Core Principles

1. **One owner per behavior.** A rule, state transition, integration, or durable side effect has one obvious owner.
2. **Policy is separate from adapters.** Domain rules should not depend directly on UI frameworks, engines, devices, storage formats, network clients, or test runners.
3. **State is explicit.** Prefer named states and validated transitions over scattered flags and hidden side effects.
4. **Data has a deliberate home.** Configuration and structured content use typed structures or parsers rather than ad hoc string manipulation.
5. **Public surfaces stay small.** Modules expose the minimum contract needed by their consumers.
6. **Dependencies point inward.** Volatile integrations depend on stable project logic, not the reverse.
7. **Optimize for replacement.** An experiment, vendor, UI, or transport should be removable without rewriting unrelated behavior.
8. **Shared code is earned.** Extract reuse only after at least two real consumers demonstrate the same stable need.

## Repository Structure

Do not create empty ceremonial folders. Adapt this example only when the responsibilities exist:

```text
src/             Product or experiment code
tests/           Automated verification
tools/           Project-local automation and diagnostics
docs/            User or technical documentation
_project/        Harness state and durable operating context
```

Framework-specific layouts belong in the project profile or a domain profile.

## Architecture Fit Check

Pause before adding another feature when any of these is true:

- One module owns three or more substantive concerns.
- Product rules, UI or device code, persistence, and dev tooling are entangled.
- A file is difficult to review as a coherent unit, often around 600 lines.
- A change requires editing the same rule in several unrelated places.
- Test-only hooks obscure the production path.
- A new vendor or framework would become the source of project truth.

At the fit check, document current responsibilities and split only proven boundaries. Refactors are behavior-preserving work with explicit verification, not hidden additions to feature work.

## Project Architecture Map

Before a prototype becomes a maintained project, record a compact map in the project profile or a dedicated document:

```text
Primary entry points:
Core behaviors and owners:
State transitions:
External adapters:
Persistent data:
Presentation or interface boundaries:
Verification hooks:
Known split triggers:
```

## Review Questions

- Can a new reader find where each important rule lives?
- Can the interface, device, vendor, or storage layer change without rewriting project policy?
- Is state changed through a clear contract?
- Did the structure solve current complexity rather than imagined reuse?
- Can the changed behavior be verified without fragile global setup?
