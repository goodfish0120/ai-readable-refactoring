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

A clean codebase also acts as local precedent: future coding agents tend to continue the grammar, naming, layering, and explicitness already visible nearby.

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

Frontend framework work may load more than one related profile because language, markup/style, and reactive runtime have distinct hazards.

Do not load unrelated language rules into a refactor.

## Repository map

- `CORE_RULES.md` — language-independent readability and traceability rules.
- `REFACTORING_WORKFLOW.md` — the sequential pass protocol and acceptance criteria.
- `skill/SKILL.md` — agent-facing instructions for applying the method progressively.
- `profiles/python.md` — Python-specific semantic hazards.
- `profiles/java.md` — Java-specific semantic hazards.
- `profiles/kotlin.md` — Kotlin-specific semantic hazards.
- `profiles/csharp.md` — C#-specific semantic hazards.
- `profiles/c.md` — C-specific ownership and memory hazards.
- `profiles/cpp.md` — C++-specific lifetime and abstraction hazards.
- `profiles/javascript-typescript.md` — JavaScript/TypeScript async, event, dynamic-state, and module hazards.
- `profiles/html-css.md` — markup semantics, DOM identity, CSS ownership, and UI-state visibility.
- `profiles/frontend-frameworks.md` — React/Vue/Svelte/Angular-style reactive state, effects, lifecycle, and server/client boundaries.
- `PROJECT_PROFILE_TEMPLATE.md` — a small template for repository-local rules.
- `INFLUENCES.md` — external work and industry practices that informed this method.

## Using the skill

For ordinary code:

```text
CORE_RULES
+ matching language profile
+ optional project profile
+ one refactoring concern
```

For a TypeScript frontend, for example:

```text
CORE_RULES
+ javascript-typescript
+ html-css when markup/styles are in scope
+ frontend-frameworks when reactive lifecycle/state is in scope
+ project profile
```

The implementation pass and readability pass are deliberately separate. The first optimizes for solving the problem. The second reshapes the working result into a form that future agents can safely continue.

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
