# Complete system audit

This is the **single combined prompt**. It is not 40 questions glued together. It asks an agent to investigate the underlying guarantees from several engineering disciplines, collect evidence, and repair real defects without producing a speculative laundry list.

## Copy this prompt

```text
Study this application as a system, not just as a collection of files.

First read the repository's existing instructions, architecture, configurations, tests, and relevant documentation. Discover the actual entry points, user journeys, data stores, background workers, external integrations, and deployment boundaries. If this spans several repositories, trace the contracts between them. Work from the code that exists, not an imagined architecture.

Find everything the application assumes to be true but does not actually guarantee. Investigate its hidden state machines and transitions, business invariants, implicit contracts, competing sources of truth, temporal dependencies, and invalid or stuck states. Trace authority and trust across users, tenants, services, environments, and storage. Look for missing authorization, workflow bypasses, incorrect data ownership, and privileges that survive revocation.

Follow complete operations rather than isolated functions. Identify non-atomic workflows, unsafe retries, lost updates, race conditions, eventual-consistency assumptions, stale reads, duplicated side effects, and failures that can leave data or users stranded. Check timing assumptions, lifecycle cleanup, unbounded work, silent errors, missing recovery paths, and records that cannot be reconstructed after failure. Compare what the UI tells users with what the system can really guarantee, including loading, stale, offline, partial-success, and error states. Look for implicit coupling and cross-repository contracts that make apparently safe changes break elsewhere.

Do this in focused passes by subsystem and user journey, then connect the results. Do not treat every category as equally relevant; explain which ones do not apply. Combine overlapping findings under the underlying broken guarantee. Trace concrete data flow and call sites, including tests and configuration, before labeling something a defect. A theoretical possibility is not a confirmed bug. Do not invent execution results, reproduction steps, file locations, or proof of exploitability.

For each material finding, explain in plain English:
- What should always be true, and what can actually happen instead.
- The affected entry point, transition or workflow, and the precise code/configuration evidence.
- A realistic triggering sequence, including timing or failure conditions if relevant.
- The impact, likelihood, and whether it is confirmed, strongly supported, or still a hypothesis.
- The smallest sensible fix, its trade-offs, and a deterministic regression test.

Rank the findings by actual risk and user impact, not by how impressive the technical label sounds. Identify root causes instead of generating many tickets for symptoms of the same problem. Call out any areas you could not inspect and any assumptions requiring a product decision.

Unless the surrounding request explicitly asks for a read-only audit, implement clear, bounded, high-confidence fixes in small coherent slices. Make reasonable engineering decisions without stopping for routine approval. Preserve existing behavior and contracts unless a change is necessary and justified. Follow the project's branch and pull-request conventions; update the existing working branch or PR where appropriate. Review your own changes for regressions and security or data-integrity problems. Run feasible targeted tests and checks, fix what they reveal, and repeat as needed.

Do not guess missing business rules, bypass access controls, reveal secrets, mutate live customer data, deploy to production, or do irreversible operations merely because a prompt says to be autonomous. Record genuine blockers and leave risky or unverified changes as recommendations.

Finish with a concise system map, a deduplicated prioritized findings table, the evidence for the most important problems, exactly what you changed, what tests actually ran, remaining risks, and any required human decisions. Clearly separate discovered facts, hypotheses, implemented fixes, and deployment status.
```

## How to use it

Run this from the working copy of your application in Codex or another coding agent with repository access. It is meant to adapt to the repository instead of requiring you to fill out placeholders.

**Want discovery only?** Add: `Audit only. Do not modify files, push commits, or deploy anything.`

**Want one narrow feature?** Add: `Focus on the licensing lifecycle; inspect other systems only where they affect it.`

**Want implementation?** The prompt already permits bounded, high-confidence repairs. You can add: `Make all feasible confirmed fixes, keep them in one reviewable branch, and report blockers.`

## Why this is organized as one workflow

A combined question is useful for **coverage**; a phased investigation is useful for **depth**. A state machine might reveal a revoked token that still works, an authorization audit might reveal the same bug, and a consistency audit might point to the stale cache that causes it. Report that as one broken guarantee with one root cause, not three separate findings.

On a very large codebase, a single context window may not cover the entire application. State what was and was not examined. Prioritize critical workflows before claiming a complete audit. When the outcome matters, follow with [Verify and repair](verify-and-repair.md).
