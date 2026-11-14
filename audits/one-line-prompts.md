# One-line software audit prompts

These are copy-and-paste questions, not instructions to blindly rewrite a codebase. Pick one question that matches the failure mode you care about. The explanation beside it is a clue about **what to investigate**, not a claim that your project has that problem.

If you want one prompt to coordinate the whole set, use [the complete system audit](complete-system-audit.md). Simply concatenating every sentence tends to create duplicate, shallow reports.

## State, rules, and contracts

| Ask your agent | What this is about |
| --- | --- |
| Find all of the implicit state machines in my app. | Hidden states, transitions, and guards scattered across code. |
| Find the invariants my app relies on but does not enforce. | Rules that must hold before and after every operation. |
| Find the undocumented contracts between my components. | Callers and callees making incompatible assumptions. |
| Find the operations that only work in a particular order. | Temporal coupling and lifecycle assumptions. |
| Find the states my app can accidentally enter but cannot handle. | Invalid, unreachable-by-design, or stuck states. |
| Find the protocols my app implements without naming them. | Multi-step interaction rules across modules and services. |
| Find every place a business rule exists only in the UI. | Backend bypasses of frontend validation. |
| Find the business decisions this app makes without recording their reasons. | Missing evidence, history, and traceability. |

## Data and distributed systems

| Ask your agent | What this is about |
| --- | --- |
| Find every competing source of truth in my app. | Conflicting state ownership, caches, and replicas. |
| Find the workflows that should be atomic but are not. | Partial commits and inconsistent outcomes. |
| Find the distributed transactions hidden in my app. | Operations crossing service or storage boundaries. |
| Find every operation that is unsafe to retry. | Duplicate side effects and absent idempotency. |
| Find every place stale data can overwrite newer data. | Lost updates and concurrency control. |
| Find all the consistency guarantees my app assumes but does not have. | Eventual consistency treated as immediate consistency. |
| Find the database relationships my app trusts without enforcing. | Orphans, broken links, and missing constraints. |
| Find every way deleted or revoked data can become active again. | Resurrection through caches, imports, backups, and sync. |
| Find the information my app cannot reconstruct after a failure. | Missing durable events, logs, or recovery records. |

## Concurrency, time, and reliability

| Ask your agent | What this is about |
| --- | --- |
| Find the race conditions that are reachable in actual use. | Interleavings in requests, tasks, and callbacks. |
| Find every way my app can fail halfway through a workflow. | Partial failure and missing compensation. |
| Find the failure states with no reliable recovery path. | Permanent blocking and broken resumability. |
| Find the places where retrying a failure makes it worse. | Retry amplification, duplicate work, and overload. |
| Find every operation whose resource use can grow without a bound. | Unbounded work, queries, queues, and memory. |
| Find all the assumptions my app makes about clocks and timing. | Expiration, drift, time zones, deadlines, and scheduling. |
| Find the background work that can outlive the object or session that started it. | Dangling callbacks, listeners, timers, and tasks. |
| Find the failures my app hides instead of surfacing or recording. | Swallowed errors and false success states. |

## Security and ownership

| Ask your agent | What this is about |
| --- | --- |
| Find the trust boundaries my app crosses without checking. | Untrusted input treated as authoritative. |
| Find the authorization rules my app only assumes. | Missing server-side resource and action checks. |
| Find the ways a user can skip a required workflow step. | Business-logic bypass and state transition abuse. |
| Find the confused-deputy problems in my app. | Privileged services misusing their authority on request. |
| Find the places my app fails open when something goes wrong. | Unsafe defaults and error fallback behavior. |
| Find the places where ownership of data or resources is ambiguous. | Cross-user, cross-tenant, and cross-environment access. |
| Find the permissions that are checked once but trusted forever. | Revocation drift and stale credentials. |

## UX, product behavior, and architecture

| Ask your agent | What this is about |
| --- | --- |
| Find the places where my UI promises something the system cannot guarantee. | Optimistic messages and misleading status. |
| Find the user journeys with no successful exit or recovery. | Dead ends, blocked forms, and unclear next steps. |
| Find all the user-visible states my UI does not represent. | Loading, empty, stale, offline, rejected, and partial success. |
| Find where users must understand my implementation to use the product. | Leaky mental models and developer terminology. |
| Find the unnecessary decisions my app makes users take. | Avoidable friction and needless branching. |
| Find the dependencies between modules that are not declared. | Hidden coupling and change propagation. |
| Find the abstractions that leak implementation details. | Interfaces that do not hide their underlying mechanics. |
| Find the assumptions shared across repositories that nobody owns. | Version drift and cross-system contracts. |

## Broad prompts

**Best short discovery question:**

> Find everything this app assumes to be true but never actually guarantees.

**Best condensed technical sweep:**

> Find the hidden state machines, invariants, contracts, trust boundaries, unsafe retries, and partial-failure paths in my app.

**Best way to constrain the agent after discovery:**

> For each finding, show the reachable code path, the broken guarantee, a minimal reproduction, and whether the issue is confirmed or only plausible.

## Choosing one

Start with state machines when a feature has lifecycle stages (licensing, checkout, imports, NFC registration). Start with invariants when a critical rule must always hold. Start with atomicity and retries for multi-step operations. Start with authorization and trust boundaries for access control. Start with UI promises when the backend works but users experience contradictory or misleading behavior.

You don't need to run every prompt. Several describe the same root cause from different angles. A good audit deduplicates by **broken guarantee**, not by wording.
