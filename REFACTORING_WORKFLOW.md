# Refactoring Workflow

This process is intentionally post-implementation.

Let the implementation model solve the problem freely first. Once behavior is working and covered well enough to detect regressions, reshape the code for future readers.

## Lifecycle

```text
free implementation
-> establish working behavior and tests
-> identify language
-> load one language profile
-> load project profile when needed
-> refactor one concern
-> run tests
-> inspect diff
-> checkpoint
-> move to the next concern
```

## One concern per pass

Do not apply the whole rule set in one rewrite.

Each pass gets one dominant concern. This makes the transformation diagnosable and keeps regressions attributable.

Recommended default sequence:

```text
Pass 1: searchable naming and stable terminology
Pass 2: abstraction height and workflow shape
Pass 3: explicit types and state ownership
Pass 4: visible side effects and hidden control flow
Pass 5: dependency boundaries and dependency intent
Pass 6: narrative bridges and local rationale
Pass 7: language-specific hazards
Pass 8: project-specific hazards
```

A repository may reorder passes when one problem blocks the rest. Keep the one-concern rule.

## Pass protocol

For every pass:

```text
1. State exactly one concern.
2. Read the relevant workflow and existing tests.
3. Mark occurrences of that concern only.
4. Refactor the smallest coherent region that resolves them.
5. Preserve behavior unless a separate bug fix has been identified.
6. Run relevant tests.
7. Inspect the diff for accidental semantic changes.
8. Commit or checkpoint independently.
9. Continue only after the pass is stable.
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

Load only the profile for code currently being refactored.

For mixed-language repositories, treat language boundaries as separate passes when practical.

Examples:

```text
Python backend pass
TypeScript frontend pass
HTML/CSS structure pass
C extension pass
```

Do not burden one pass with every hazard from every language.

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
Who owns this state?
Where does this side effect occur?
Why is this dependency here?
Which code should I inspect next for more detail?
What important behavior is intentionally hidden behind a boundary?
What capability should I avoid reimplementing?
What assumptions would make this code wrong if they changed?
```

## Stopping condition

Stop when another pass would mostly produce cosmetic churn rather than lower reconstruction cost.

The target is a repository whose local structure teaches future agents how to continue it.
