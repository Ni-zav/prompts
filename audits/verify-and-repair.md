# Verify and repair

Use this after a discovery pass, a bug report, or an architecture review. The goal is not to make an agent agree with its earlier findings. The goal is to challenge them, fix real defects, and show what was verified.

## Copy this prompt

```text
Review the reported findings critically against the current repository. Do not assume the previous audit is correct.

For each finding, trace the full entry point and affected code path, including callers, authorization, state transitions, storage, asynchronous work, and relevant tests. Determine whether the claimed failure is reachable under realistic conditions. Separate confirmed defects, well-supported risks, unverified hypotheses, intentional trade-offs, and false positives. Merge duplicates that share a root cause.

Prioritize by severity, reachability, blast radius, and user impact. Fix confirmed issues in small, reviewable changes, starting with those that protect data integrity, authorization, and critical workflows. Preserve public contracts and existing valid behavior. Where a business rule is undecided, describe the decision required and avoid silently inventing it.

Create or improve deterministic regression coverage for each fix: success, rejection, failure halfway through, retry, concurrency, and recovery as applicable. Use controllable clocks and injected failures rather than arbitrary sleeps. Do not claim a test passed unless you ran it and observed the result. Run available checks, inspect the diff for accidental changes, and iterate until the known regression tests pass or an actual blocker is documented.

Continue using the current branch or open pull request when appropriate, following repository instructions. Make reasonable engineering choices without repeatedly requesting approval for routine work. Do not deploy, modify production records, disclose credentials, or perform irreversible operations without the required authorization.

Report a short findings ledger with: confirmed/unverified/false positive; evidence; fix and commit or file changes; tests executed and outcomes; residual risks; and real blockers. Never describe untested work as shipped or a recommendation as an implemented safeguard.
```

## What makes a good result?

A good result shows the difference between **the system is intended to prevent duplicate orders** and **two concurrent requests can both pass an application-level existence check before either creates an order**.

Then it adds an enforceable guarantee, tests the concurrent case, and reports the actual test outcome. It does not call a hypothetical scenario a production incident, and it does not claim a deployment from a local commit.

See the [evidence example](../examples/evidence-example.md).
