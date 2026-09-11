# Refactoring Rule Families

This file classifies refactoring rules by why they exist.

The execution model stays simple: choose one dominant concern, refactor a coherent region, run tests, inspect the diff, and checkpoint. The classification below keeps different philosophies from collapsing into one undifferentiated list of "best practices."

Language profiles answer a different question: where does this language or ecosystem commonly break one of these goals?

## 1. Reading continuity

Goal: let a reader follow the current line of thought through the code without repeated detours to reconstruct context.

Typical signals:

```text
abstraction height jumps
workflow stages are buried in plumbing
important transitions lack a named step
entering a function loses why this stage exists
understanding one local interaction requires opening many unrelated files
```

Typical remedies include semantic layering, thin orchestrators, structural methods, and narrative bridges.

## 2. Discoverability and searchability

Goal: make important concepts easy to find and trace from names, logs, events, APIs, and call sites.

Typical signals:

```text
generic names such as process / handle / utils / manager
one concept has several spellings
runtime identities cannot be searched back to source
important APIs require repeated archaeology before use
```

Typical remedies include stable domain vocabulary, searchable identifiers, explicit runtime identities, and locally discoverable capability boundaries.

## 3. Structural placement and responsibility

Goal: put important logic where a reader would reasonably expect to find it based on responsibility.

Typical signals:

```text
unrelated logic accumulates in common / utils / manager files
one file owns several unrelated responsibilities
behavior lives far from the concept that explains why it exists
physical file layout contradicts conceptual ownership
```

The purpose is predictable navigation, not arbitrary file-size limits.

## 4. Causal transparency

Goal: make consequential behavior traceable from effect to operation, caller, and workflow purpose.

Typical signals:

```text
reflection-driven dispatch
AOP or interceptors changing core semantics
callbacks with undiscoverable producers or consumers
framework annotations changing runtime behavior invisibly
side effects hidden behind innocent-looking calls
```

The reader should be able to find who caused an important event without reconstructing an entire runtime container.

## 5. State ownership and lifetime

Goal: make it clear who owns state or resources, who may mutate them, how long they remain valid, and who releases or cancels them.

Typical signals:

```text
shared mutable globals
ambiguous dependency-injection ownership
unclear pointer ownership
async work with no visible owner
subscriptions or resources with unclear cleanup
state duplicated across several owners
```

Different languages expose this problem through different mechanisms, but the underlying philosophy is the same.

## 6. Dependency clarity

Goal: preserve the project-specific reason an external dependency exists and the boundary of responsibility around it.

A future reader should be able to recover:

```text
why this dependency is used
which behavior or guarantee the project relies on
where our responsibility ends
what would matter if the dependency were removed or replaced
whether an existing dependency capability should be searched before reimplementation
```

Document the dependency decision, not the dependency encyclopedia.

## 7. Domain meaning and type clarity

Goal: preserve stable domain distinctions in interfaces and state so readers do not have to reconstruct meaning from generic representations.

Typical signals:

```text
important state encoded as strings or magic integers
boolean arguments hiding domain decisions
generic dictionaries or tuples carrying stable concepts
nullable or optional fields creating many invalid combinations
untyped metadata crossing many layers
```

Use explicit types, named options, enums, value objects, discriminated states, or small result structures when they reduce ambiguity.

## Language profiles are hazard maps

Language profiles are not separate philosophies. They describe the mechanisms that commonly damage the rule families above.

Examples:

```text
Kotlin scope-function chains
-> may break reading continuity by hiding receiver identity

Java annotations / AOP
-> may break causal transparency

C pointer boundaries
-> may hide ownership and lifetime

JavaScript event systems
-> may hide causal topology and async lifetime

HTML/CSS selector structure
-> may hide structural ownership and source-to-runtime relationships
```

Load the smallest set of profiles needed for the code being refactored. A primary language profile may explicitly depend on companion profiles, such as C++ with C, Kotlin with JVM framework concerns, or frontend framework code with JavaScript/TypeScript and markup/style rules.

## One rule, one primary home

A rule may improve several qualities at once, but give it one primary family. Cross-reference secondary effects instead of duplicating the same rule across several sections.

This keeps the method explainable: every rule should have a clear reason for existing.

## Adding a new rule

Before adding a rule, answer:

```text
Which rule family does it primarily serve?
What reconstruction cost or failure mode does it reduce?
Is it language-independent or a language-specific hazard?
Is it a stable engineering lesson or only a local style preference?
```

External practices and borrowed industry experience are welcome when their purpose is clear. `INFLUENCES.md` records provenance; this file records why the rule belongs in the method.
