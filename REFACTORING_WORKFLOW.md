# Refactoring Workflow

This process is intentionally post-implementation.

Let the implementation model solve the problem freely first. Once behavior is working and covered well enough to detect regressions, reshape the code for future readers.

## Lifecycle

```text
free implementation
-> establish working behavior and tests
-> identify the dominant refactoring concern
-> identify language and ecosystem hazards
-> load the minimum necessary profile set
-> load project profile when needed
-> refactor one coherent concern
-> run tests
-> inspect diff
-> checkpoint
-> move to the next concern
```

## One dominant concern per pass

Do not apply the whole rule set in one rewrite.

Each pass gets one dominant concern. This keeps the transformation diagnosable and makes regressions easier to attribute.

Coupled edits may move together when they are necessary to complete the same coherent change.

Recommended default sequence:

```text
Pass 1: searchable naming and stable terminology
Pass 2: abstraction height and workflow shape
Pass 3: structural placement and responsibility
Pass 4: explicit types and state ownership
Pass 5: visible side effects and control-flow visibility
Pass 6: dependency boundaries and dependency intent
Pass 7: narrative bridges and local rationale
Pass 8: language-specific hazards
Pass 9: project-specific hazards
```

A repository may reorder passes when one problem blocks the rest. Keep one dominant reason for each pass.

## Pass protocol

For every pass:

```text
1. State the primary rule family and one dominant concern.
2. Read the relevant workflow and existing tests.
3. Mark occurrences of that concern only.
4. Refactor the smallest coherent region that resolves them.
5. Include coupled edits only when they are necessary to complete the same change.
6. Preserve behavior unless a separate bug fix has been identified.
7. Run relevant tests.
8. Inspect the diff for accidental semantic changes.
9. Commit or checkpoint independently.
10. Continue only after the pass is stable.
```

Large files may require several passes of the same concern.

Do not widen scope merely because adjacent code also looks untidy.

## Behavioral bugs discovered during refactoring

Readability work often exposes latent behavioral bugs.

When that happens:

```text
observe suspicious semantics
-> write a focused test that pins the intended behavior
-> fix the behavior as a separate change
-> return to structural refactoring
```

This separation preserves evidence about what the refactor changed and what the bug fix changed.

## Language selection

Load the smallest profile set needed for the code currently being refactored.

Most passes have one primary language profile. Add companion profiles only when the code genuinely depends on another language or ecosystem layer, or when the primary profile explicitly points to them.

Examples:

```text
Python backend pass

C++ pass
+ C profile where physical ownership or ABI concerns still apply

Kotlin pass
+ Java profile where JVM framework behavior is relevant

TypeScript frontend pass
+ HTML/CSS when markup or styles are in scope
+ frontend-frameworks when reactive lifecycle or state is in scope
```

For mixed-language repositories, treat substantially different language boundaries as separate passes when practical.

Do not burden one pass with unrelated hazards from every language.

## Project profile

A project profile should remain small and capture only local semantics that are unusually expensive to misunderstand.

Examples:

```text
simulation time units must remain visible in names
network routing policy must remain separate from network mechanism
database migrations own persistent format changes
UI state ownership must remain explicit between server, client store, and component
```

Promote a project rule into a language or core rule only after it proves broadly reusable.

## Refactor acceptance questions

A cold-start reader should be able to answer:

```text
What is this subsystem for?
What happens in what order?
Can I keep following the current reading path without unnecessary detours?
Who owns this state?
Where does this side effect occur?
Why is this dependency here?
Which code should I inspect next for more detail?
What important behavior sits behind a boundary?
What capability should I avoid reimplementing?
What assumptions would make this code wrong if they changed?
```

## Stopping condition

Stop when another pass would mostly produce cosmetic churn rather than lower reconstruction cost.

The target is a repository whose local structure teaches future agents how to continue it.
