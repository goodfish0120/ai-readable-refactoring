# Core Rules

These rules are language-independent. Load the minimum necessary language profile set beside them, then add a small project profile only when the repository has domain-specific hazards.

`RULE_FAMILIES.md` explains why the rules exist. Language profiles explain where each language or ecosystem commonly breaks those goals.

## Reading continuity

Optimize for reading continuity.

A reader should be able to follow the current line of thought through the code without repeatedly leaving it to reconstruct naming, ownership, causality, hidden control flow, dependency intent, or workflow position.

The purpose of the rules below is to reduce those interruptions while preserving ordinary language idioms.

## Recoverable causality

Important runtime behavior should have a visible path through the code.

A cold-start reader should be able to move from an observed effect to the operation that caused it, then to its caller and workflow purpose without reconstructing a framework runtime.

Consequential behavior deserves explicit calls, explicit dispatch maps, or another locally discoverable path.

## Visible state ownership

Important mutable state should have an identifiable owner and a named write path.

Prefer:

```text
state owner
-> named transition
-> caller expressing why the transition occurs
```

Avoid mutation that can originate from arbitrary helpers, globals, reflection hooks, callbacks, or unrelated modules.

## Visible side effects

Persistence, network transfer, filesystem I/O, external API calls, resource reservation, shared-state mutation, lifecycle changes, retries, transactions, and asynchronous work should look consequential at the call site.

A short name is fine when the surrounding type already supplies the missing context. Hidden consequence is the problem.

## Searchable semantic naming

Important identifiers should work as search handles.

Prefer:

```text
specific action + specific object + stable boundary
```

Use stable domain words. Keep one important concept under one spelling when practical.

Avoid generic names such as `process`, `handle`, `manage`, `helper`, `utils`, `common`, or `manager` when the local context does not make their responsibility obvious.

Runtime identities that appear in logs, errors, events, protocols, or persisted state should remain searchable back to source. Avoid dynamic string construction when it destroys this property.

## Structural placement

Important logic should live under a discoverable owner and in a location that matches its responsibility.

Inspect files or modules that accumulate unrelated behavior under names such as `utils`, `common`, `helpers`, or `manager`. The goal is not arbitrary file-size reduction. The goal is that a reader can predict where a concept lives and why it lives there.

## Shared semantics, local policy

Consolidate repeated logic when it expresses the same stable semantic contract under an identifiable owner. Similar syntax alone is not enough. A shared predicate or mechanism should let readers trust its name instead of comparing several implementations.

Keep boundary-specific policy visible: admission, error mapping, fallback, provenance, and effect ordering may differ even when the underlying check is shared. Preserve existing compatibility or dispatch seams where consumers depend on them. Use a domain-specific name and an intentional export for a cross-module contract; avoid turning a private generic helper into an accidental shared interface.

Leave small local repetition in place when sharing would add coupling or reader detours without clarifying a common contract.

## Textbook-style semantic layering

Code should reveal intent in this order:

```text
purpose
-> structure
-> mechanism
-> implementation detail
```

High-level functions should read like conceptual maps. Lower functions should add roughly one level of resolution at a time.

One function should usually stay near one abstraction height. Repeated jumps between policy, transport, storage, parsing, index arithmetic, and lifecycle control are a refactoring signal.

## Thin orchestrators

Entry points and workflow coordinators should expose the main sequence without burying it under plumbing.

A reader should be able to inspect the orchestrator and answer:

```text
what is prepared
what runs
what is observed
what is returned or written
```

## Single-use structural methods

Call frequency does not determine abstraction value.

A method with one caller can be valuable when it names a workflow stage, preserves abstraction height, localizes one responsibility, or lets the caller express the system structure directly.

Do not extract a one-off helper merely to shorten a function. The extraction should add semantic structure that helps the reader continue the current line of thought.

## Narrative bridges

A function name explains what the function does.

Add a short opening explanation when a reader entering the function directly would otherwise lose one of these:

```text
why this stage exists here
what the previous stage already established
what conceptual transition this function owns
what the next stage receives
```

Do not add narrative bridges to obvious pure helpers. The purpose is continuity across abstraction boundaries, not comments everywhere.

## Explicit dependency boundaries

External libraries may remain black boxes. Our relationship with them should be visible.

At a dependency boundary preserve only the project-specific information that would be expensive to reconstruct:

```text
why this dependency is used here
which behavior or guarantee we rely on
where our responsibility ends
which replacement-sensitive assumption matters
```

Do not explain the library's whole feature set locally.

Preferred shape:

```text
transparent core
-> explicit adapter / gateway / integration boundary
-> external library
```

Before deleting a dependency or reimplementing substantial infrastructure, search the repository and dependency surface for an existing capability that may already own the job.

## Preserve domain meaning in types

Do not erase stable domain concepts into generic strings, integers, dictionaries, tuples, or untyped metadata when a small explicit type would prevent ambiguity or invalid states.

Avoid boolean arguments that encode a domain decision when the call site becomes opaque. Prefer named options or domain enums.

## Structural regularity

Similar operations should have similar visible shapes.

Examples:

```text
transfer: source, destination, payload, ready_time
scheduler: work, policy, resource, time
state transition: current state, decision, next state
```

A future reader should be able to infer repository grammar from nearby examples.

## Visible deprecation

Legacy paths that remain callable should look deprecated. Search should not present obsolete code as an equally valid implementation path.

## Explanations are worth extra lines when

Use extra explanation for information that cannot be cheaply reconstructed from local code:

```text
crossing an abstraction boundary
entering or leaving a third-party dependency
relying on a non-obvious library guarantee
using a surprising performance tradeoff
using a simplified physical or simulation model
owning concurrency or asynchronous lifetime
owning memory or resource lifetime
depending on ABI, persisted format, protocol, or compatibility behavior
preserving an external workaround
keeping a locally strange step because removing it changes semantics
```

Comments should preserve rationale, assumptions, constraints, provenance, and continuation context. Do not narrate syntax.

## Restricted patterns in core logic

These patterns require strong justification when they carry important domain behavior:

```text
reflection-driven dispatch
runtime proxies hiding important calls
AOP/interceptors changing core semantics invisibly
metaprogramming for ordinary control flow
monkey patching
implicit global mutation
magic boolean arguments
unstructured metadata crossing many layers
stringly typed domain state
callbacks or event buses without a discoverable dispatch map
operator overloading hiding expensive or state-changing work
long chains containing several state transitions
single expressions combining filtering, mutation, branching, and I/O
```

The restriction targets hidden semantics. Idiomatic syntax that remains locally obvious is fine.

## Dependency decision, not dependency encyclopedia

Local code records our decision boundary. The external library remains responsible for documenting itself.

A dependency note should help a future agent answer:

```text
Why is this here?
Which guarantee do we depend on?
Can I safely remove or replace it?
Should I search this library before implementing the same capability again?
```

That is enough.
