---
name: ai-readable-refactoring
description: Refactor already-working code into a form that future humans and coding agents can understand, search, trace, extend, and verify. Use after implementation when behavior is testable; apply one dominant readability concern per pass and load only the minimum necessary language profiles.
---

# Refactor Code for AI Readability

Use this skill after a working implementation exists and relevant behavior is testable.

## Goal

Reduce reconstruction cost for future human and AI readers while preserving behavior.

Protect reading continuity: code should let a reader follow the current line of thought without repeated detours to reconstruct workflow, causality, state ownership, side effects, dependency intent, or abstraction boundaries.

## Load rules progressively

1. Read `CORE_RULES.md`.
2. Read `RULE_FAMILIES.md` and identify the primary reason for the current refactor.
3. Detect the language and ecosystem of the code being refactored.
4. Read the minimum necessary profile set under `profiles/`.
5. Read the repository's project profile if one exists.
6. Read `REFACTORING_WORKFLOW.md`.

Most work needs one primary language profile. Add companion profiles only when the code genuinely crosses a language or ecosystem boundary, or when the primary profile explicitly points to them.

For frontend framework code, for example, load:

```text
profiles/javascript-typescript.md
profiles/html-css.md when markup/styles are in scope
profiles/frontend-frameworks.md when framework lifecycle/state is in scope
```

Do not load unrelated language profiles.

## Work sequentially

Choose one primary rule family and one dominant concern for the current pass.

Typical concerns are:

```text
reading continuity
searchable naming
structural placement
abstraction height
state ownership
type/domain meaning
side-effect visibility
control-flow visibility
dependency boundaries
narrative bridges
language-specific hazards
project-specific hazards
```

Refactor the smallest coherent region that resolves that concern. Coupled edits may move together when they are necessary to complete the same change.

Run relevant tests after the pass. Inspect the diff for accidental behavior changes. Checkpoint the pass independently before moving to another concern.

## Preserve behavior

This is a structural refactoring skill by default.

When a pass exposes suspicious behavior, stop structural expansion around that issue. Add a focused test for intended semantics, fix the behavioral bug separately, then resume refactoring.

## Do not optimize for short code

Extra lines are justified when they preserve causality, ownership, intent, lifecycle, external constraints, dependency boundaries, or reading continuity.

Ordinary local mechanics should remain concise.

## Do not normalize idioms mechanically

Language profiles identify semantic hazards, not forbidden syntax lists.

Examples:

```text
A clear C `goto cleanup` may improve ownership visibility.
A small Python comprehension may be clearer than three helper functions.
An idiomatic frontend effect may be appropriate when trigger, consequence, and cleanup are obvious.
A single-use method may be valuable when it names a workflow stage or preserves abstraction height.
```

Optimize reconstruction cost, not stylistic uniformity for its own sake.

## Completion report

Keep the report compact:

```text
Rule family:
Pass:
Files changed:
Semantic friction removed:
Behavior changes: none / separately identified
Validation:
Remaining high-value concerns:
```
