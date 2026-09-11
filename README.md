# AI-Readable Refactoring

A post-implementation refactoring method for making working code easier for future humans and coding agents to understand, search, extend, and verify.

The working assumption is simple:

```text
let the implementation model solve the problem freely
-> establish behavior with tests
-> refactor for recoverable intent
-> re-run tests after every focused pass
```

This repository treats source code as part of the collaboration interface between the current author and future readers. Good code should let a cold-start reader recover the workflow, causality, state ownership, dependency boundaries, and next place to inspect without reconstructing the whole repository.

## Core shape

```text
purpose
-> structure
-> mechanism
-> implementation detail
```

High-level code should read like a conceptual map. Lower layers add one level of resolution at a time.

## Operating rule

Refactor one concern per pass.

```text
naming
-> tests
-> inspect diff

abstraction height
-> tests
-> inspect diff

state ownership
-> tests
-> inspect diff

hidden control flow
-> tests
-> inspect diff

dependency boundaries
-> tests
-> inspect diff

narrative bridges
-> tests
-> inspect diff

language-specific hazards
-> tests
-> inspect diff
```

The order can change when a repository has an obvious blocking problem. The single-concern-per-pass rule stays.

## Rule layers

Apply only what the current code needs:

```text
CORE_RULES.md
+ one language profile from profiles/
+ a small project-specific profile when necessary
```

Do not load every language rule into every refactor.

## Repository map

- `CORE_RULES.md` — language-independent readability and traceability rules.
- `REFACTORING_WORKFLOW.md` — the sequential pass protocol and acceptance criteria.
- `profiles/python.md` — Python-specific semantic hazards.
- `profiles/java.md` — Java-specific semantic hazards.
- `profiles/kotlin.md` — Kotlin-specific semantic hazards.
- `profiles/csharp.md` — C#-specific semantic hazards.
- `profiles/c.md` — C-specific ownership and memory hazards.
- `profiles/cpp.md` — C++-specific lifetime and abstraction hazards.
- `PROJECT_PROFILE_TEMPLATE.md` — a small template for repository-local rules.

## Design target

The goal is not maximum verbosity. The goal is minimum reconstruction cost with recoverable:

```text
causality
ownership
intent
boundaries
state transitions
dependency decisions
workflow position
```

Extra explanation is valuable where those things would otherwise disappear. Ordinary local code should stay ordinary.
