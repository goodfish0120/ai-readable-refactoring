# Influences and External Precedents

This repository combines local design principles with ideas that have independently emerged in the coding-agent ecosystem.

The rules here are rewritten around this project's goals: post-implementation refactoring, recoverable causality, visible ownership, dependency boundaries, narrative continuity, and language-specific hazard passes.

## Modem — write-discoverable-code

- Skill repository: https://github.com/modem-dev/skills
- Background article: https://modem.dev/blog/how-coding-agents-read-your-code

Useful ideas reinforced by this work include:

```text
identifiers as search handles
domain words in names
stable concept spelling
precise types as navigation aids
searchable runtime strings
concept-named modules
thin orchestrators
comments placed where retrieval lands
```

Their experiments are a useful external check that source-code discoverability affects coding-agent retrieval cost and correctness.

## AGENTS.md

- https://agents.md/

AGENTS.md demonstrates the value of a predictable repository-local surface for agent instructions, setup commands, tests, and conventions.

This project uses the same progressive-context idea but pushes more intent into source structure itself so correctness does not depend entirely on an agent reading instructions first.

## Agent Skills

- Anthropic skills repository: https://github.com/anthropics/skills
- OpenAI skills repository: https://github.com/openai/skills

The skill model reinforces progressive disclosure:

```text
small discoverable entry point
-> task-specific instructions
-> deeper references only when needed
```

The same principle informs the separation of core rules, language profiles, project profiles, and sequential refactoring passes.

## Aider repository maps

- https://aider.chat/docs/repomap.html

Aider's repository-map work is a useful precedent for compactly exposing important symbols, signatures, and relationships rather than loading an entire codebase into context.

This project approaches the same problem from the source-code side: make names, boundaries, types, workflow shape, and local explanations informative enough that a compact map or search result carries more usable semantics.

## Local additions in this repository

The following emphases are central here:

```text
traceable causality
visible state and resource ownership
visible consequential side effects
narrative bridges across abstraction boundaries
explicit third-party dependency intent boundaries
post-implementation refactoring rather than constraining initial exploration
one semantic concern per refactoring pass
language-specific profiles instead of one universal syntax style
frontend reactive/lifecycle ownership as a distinct concern
```

External practices are treated as empirical input, not as a fixed authority. Rules should survive because they reduce reconstruction cost in real repositories.
