# Contributing

This repository is a small, practical prompt library. Clarity and usefulness matter more than the number of entries.

## Adding a prompt

Start by checking whether a similar prompt already exists. Prefer a new question only when it uncovers a meaningfully different class of problem.

A useful contribution includes:

1. **Prompt:** A natural-language question that can be copied as-is.
2. **Concept:** The engineering discipline or behavior it helps reveal.
3. **Use case:** When it is worth running, ideally with a short concrete example.
4. **Verification:** What evidence would distinguish a real finding from a guess.
5. **Attribution:** Credit an identifiable original source when adapting a distinctive idea.

For a short one-liner, a new row in [One-line prompts](audits/one-line-prompts.md) is enough. For a substantial reusable workflow, create a focused Markdown file and link it from the main README.

## Writing style

- Write like one developer talking to another, not as an elaborate AI persona.
- Favor specific engineering ideas over "act as a world-class expert."
- Keep the copyable prompt separate from explanations and examples.
- Avoid unnecessary model-specific commands, dependencies, or invented metrics.
- Ask for evidence and uncertainty rather than promising comprehensive bug detection.
- Don't paste third-party collections wholesale or reproduce proprietary prompts.
- Keep tests, deployment, and claims of correctness clearly distinguished.

## Reviewing a contribution

Ask whether it adds a new angle, whether a coding agent with real repository access could actually act on it, and whether it encourages evidence over hallucinated findings. If it overlaps another entry, improve or merge the existing prompt.

This repository has not selected a reuse license. Please submit only content that you have the right to contribute; do not assume public visibility grants unrestricted reuse.
