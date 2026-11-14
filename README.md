# Prompts

Small questions that uncover big problems in software.

This is a practical collection of plain-language prompts for exploring, auditing, and improving real applications with coding agents such as Codex. It favors questions that activate a useful engineering concept over vague requests like "find bugs" or unnecessarily long role-playing instructions.

No installation, CLI, framework, or special prompt format is required. Open a file, copy the prompt, and run it in the repository you want to inspect.

## Start here

**One line, broad discovery**

> Find everything this app assumes to be true but never actually guarantees.

**One line, deeper system audit**

> Find the hidden state machines, invariants, contracts, trust boundaries, and failure paths in this app, then show me where the code fails to enforce them.

**Complete audit with evidence and sensible execution**

Use [The complete system audit](audits/complete-system-audit.md). It organizes discovery into passes instead of dumping dozens of loosely related instructions into a single paragraph.

## Browse the collection

| File | When to use it |
| --- | --- |
| [One-line prompts](audits/one-line-prompts.md) | Choose a focused question about state, correctness, concurrency, security, UX, or architecture. |
| [Complete system audit](audits/complete-system-audit.md) | Ask a coding agent to inspect the whole application, validate findings, and plan or execute focused fixes. |
| [Verify and repair](audits/verify-and-repair.md) | Turn an existing audit report into reproducible tests and safe, reviewed changes. |
| [Evidence example](examples/evidence-example.md) | See the difference between a credible finding and an unsupported guess. |
| [Contributing](CONTRIBUTING.md) | Add or improve a prompt while keeping it understandable. |

## How to use

1. Start with **one** focused prompt, especially on a large repository.
2. Ask the agent to point to actual code paths, call sites, tests, and relevant configuration.
3. Separate confirmed defects from plausible risks and unverified questions.
4. Use the verification-and-repair prompt before accepting substantial code changes.

For wide audits, read the complete prompt once. Let the agent divide the work by subsystem, deduplicate overlapping findings, and report what it could **not** inspect. An audit is not proof of a vulnerability, nor is a passing test proof that the system is correct.

### What belongs here?

- Reusable, natural-language prompts.
- A brief explanation of the engineering concept each prompt invokes.
- Ways to verify an answer instead of trusting confident-sounding speculation.
- Tool-agnostic instructions with optional Codex-specific use cases.

Not included: scraped prompt dumps, fake benchmark claims, irrelevant model-specific boilerplate, or a mandatory website.

## Inspiration and further reading

- Steve Ruiz, [@steveruizok](https://x.com/steveruizok), highlighted the question "find all of the implicit state machines in my app" (October 2026).
- [Drix10/awesome-prompts](https://github.com/Drix10/awesome-prompts): a lightweight index with topic-based reference files and short prompts.
- [onamfc/agent-prompt-library](https://github.com/onamfc/agent-prompt-library): separate canonical prompts and usage documentation.
- [f/prompts.chat](https://github.com/f/prompts.chat): a larger collection that separates its prompt catalog from its introductory README.

This repository contains original explanations and adaptations of general software-engineering ideas; it does not claim the underlying concepts or the original state-machine prompt were invented here.

## Scope

Start with software engineering and coding-agent workflows. Expand categories only when there are prompts worth keeping. Prefer a useful small library over a large, repetitive one.

No license has been selected yet. Public visibility alone does not grant reuse rights; contributors should only submit content they have permission to share.
