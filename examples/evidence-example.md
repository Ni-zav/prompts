# What credible audit evidence looks like

This is a **fictional example**, not a finding about a real application. It illustrates the level of specificity to expect from an agent.

## Weak report

> There may be race conditions in the order creation service. Add a lock.

This gives no reachable sequence, evidence, actual impact, or explanation of why locking is the right solution.

## Better report

**Finding:** Duplicate order creation is possible on concurrent requests. **Status:** Hypothesis pending a concurrency test.

**Expected guarantee:** One accepted idempotency key maps to no more than one order.

**Possible failure path:** The API first checks whether an order with the key exists, then inserts the new order in a separate database operation. If the database has no unique constraint on that key, two concurrent requests can both observe "not found" and each insert an order.

**Evidence to verify in this repository:** The relevant route and service functions, schema/index definitions, transaction boundaries, and existing tests. Cite exact file paths and line ranges from the actual checkout; do not invent them.

**Minimal reproduction:** Send two requests using the same idempotency key, coordinate them to reach the read-before-write boundary together, and inspect the committed rows. Do not use real payment credentials or production data.

**Potential fix:** Enforce uniqueness in the database and handle conflict as a safe idempotent replay. Consider whether the key must be scoped by user, tenant, or operation.

**Regression test:** Confirm one durable order and stable responses for simultaneous requests, repeated requests, and a crash/retry sequence.

**Outcome:** Keep this as a hypothesis until the code, schema, and test evidence confirm the scenario. If a database constraint already provides the guarantee, mark it as a false positive instead.

## Suggested audit ledger

| ID | Broken guarantee | Reachability | Evidence | Severity | Status | Fix or next step |
| --- | --- | --- | --- | --- | --- | --- |
| AUD-01 | One idempotency key creates at most one order | Not yet tested | Route + schema inspection needed | Potentially high | Hypothesis | Inspect, reproduce, then decide |

Use small, honest labels such as **confirmed**, **supported risk**, **hypothesis**, **false positive**, **fixed locally**, and **deployed and verified**. Those labels mean different things.
