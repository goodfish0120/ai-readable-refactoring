# Refactor Code for AI Readability

Use this skill after a working implementation exists and relevant behavior is testable.

## Goal

Reduce reconstruction cost for future human and AI readers while preserving behavior.

The code should make workflow, causality, state ownership, side effects, dependency intent, and abstraction boundaries recoverable without loading the whole repository.

## Load rules progressively

1. Read `CORE_RULES.md`.
2. Detect the language of the code being refactored.
3. Read only the matching file under `profiles/`.
4. Read the repository's project profile if one exists.
5. Read `REFACTORING_WORKFLOW.md`.

For frontend framework code, load:

```text
profiles/javascript-typescript.md
profiles/html-css.md when markup/styles are in scope
profiles/frontend-frameworks.md when framework lifecycle/state is in scope
```

Do not load unrelated language profiles.

## Work sequentially

Choose one concern for the current pass. Typical concerns are:

```text
searchable naming
abstraction height
state ownership
type/domain meaning
side-effect visibility
hidden control flow
dependency boundaries
narrative bridges
language-specific hazards
project-specific hazards
```

Refactor only that concern in the smallest coherent region.

Run relevant tests after the pass. Inspect the diff for accidental behavior changes. Checkpoint the pass independently before moving to another concern.

## Preserve behavior

This is a structural refactoring skill by default.

When a pass exposes suspicious behavior, stop structural expansion around that issue. Add a focused test for intended semantics, fix the behavioral bug separately, then resume refactoring.

## Do not optimize for short code

Extra lines are justified when they preserve causality, ownership, intent, lifecycle, external constraints, or dependency boundaries.

Ordinary local mechanics should remain concise.

## Do not normalize idioms mechanically

Language profiles identify semantic hazards, not forbidden syntax lists.

Examples:

```text
A clear C `goto cleanup` may improve ownership visibility.
A small Python comprehension may be clearer than three helper functions.
An idiomatic frontend effect may be appropriate when trigger, consequence, and cleanup are obvious.
```

Optimize reconstruction cost, not stylistic uniformity for its own sake.

## Completion report

Keep the report compact:

```text
Pass:
Files changed:
Semantic friction removed:
Behavior changes: none / separately identified
Validation:
Remaining high-value concerns:
```
