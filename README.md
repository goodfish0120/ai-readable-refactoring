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

## Core philosophy

Protect reading continuity.

A reader should be able to follow the current line of thought through the code without repeatedly leaving it to reconstruct hidden context, ownership, causality, naming, or dependency intent.

Different rule families serve different purposes. `RULE_FAMILIES.md` separates those philosophies. Language profiles then describe where a specific language or ecosystem commonly breaks them.

## Core shape

```text
purpose
-> structure
-> mechanism
-> implementation detail
```

High-level code should read like a conceptual map. Lower layers add one level of resolution at a time.

## Operating rule

Refactor one dominant concern per pass.

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

The order can change when a repository has an obvious blocking problem. Keep one dominant cause per pass. Coupled edits that are necessary to complete the same coherent change may move together.

## Rule layers

Apply only what the current code needs:

```text
CORE_RULES.md
+ RULE_FAMILIES.md
+ the minimum necessary language profile set from profiles/
+ a small project-specific profile when necessary
```

Most work needs one primary language profile. Companion profiles are loaded only when the code genuinely crosses a language/ecosystem boundary or the primary profile explicitly depends on them.

Examples include C++ with C lifetime concerns, Kotlin with JVM framework concerns, and frontend framework work with JavaScript/TypeScript plus markup/style rules.

Do not load unrelated language rules into a refactor.

## Repository map

- `CORE_RULES.md` — language-independent readability and traceability rules.
- `RULE_FAMILIES.md` — the distinct purposes and philosophies behind the rules.
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
+ RULE_FAMILIES
+ matching language profile
+ optional project profile
+ one dominant refactoring concern
```

For a TypeScript frontend, for example:

```text
CORE_RULES
+ RULE_FAMILIES
+ javascript-typescript
+ html-css when markup/styles are in scope
+ frontend-frameworks when reactive lifecycle/state is in scope
+ project profile
```

The implementation pass and readability pass are deliberately separate. The first optimizes for solving the problem. The second reshapes the working result into a form that future agents can safely continue.

## Design target

The goal is not maximum verbosity. The goal is minimum reconstruction cost with recoverable:

```text
reading path
causality
ownership
intent
boundaries
state transitions
dependency decisions
workflow position
```

Extra explanation is valuable where those things would otherwise disappear. Ordinary local code should stay ordinary.
