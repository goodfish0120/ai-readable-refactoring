# JavaScript / TypeScript Profile

Frontend and Node.js code can hide execution through callbacks, promises, module side effects, framework conventions, and highly dynamic object shapes. Refactor these concerns separately.

## Async causality

Inspect promise chains, detached promises, timers, event listeners, queues, workers, subscriptions, and callbacks for visible ownership.

A reader should be able to answer:

```text
who starts the work
what event or condition continues it
who awaits or observes completion
who cancels or removes it
what survives the caller
```

Avoid fire-and-forget work whose lifetime is accidental.

## Event and callback topology

Important events should have discoverable producers and consumers. Prefer centralized registration or another searchable mapping when events carry domain behavior.

Keep runtime event names stable and searchable. Avoid constructing important identities from fragments when logs can no longer be traced back to source.

## Dynamic object shape

Inspect generic objects, property bags, string-keyed state, optional fields with many legal/illegal combinations, and runtime property injection.

In TypeScript, use discriminated unions, explicit interfaces/types, branded/domain types, and exhaustiveness checks when they preserve real state distinctions.

## Coercion and implicit semantics

Inspect truthiness-dependent domain decisions, loose equality, implicit number/string coercion, overloaded object shapes, and APIs where `undefined`, `null`, missing, false, and empty carry different meanings without being named.

## Dense functional chains

Inspect long `map/filter/reduce/flatMap` chains when they contain several domain stages, mutation, async work, or hidden error handling.

Use named intermediate stages when the chain stops reading as one transformation.

## Module side effects

Inspect code that performs registration, mutation, network calls, environment detection, or singleton initialization merely by being imported.

Important initialization should have a visible entry point.

## Dependency and build-tool magic

Keep framework, bundler, code-generation, polyfill, transpilation, and runtime-injection assumptions near explicit boundaries or configuration entry points. Preserve why a non-obvious plugin or package is required when removing it could silently change runtime behavior.

## Type escape hatches

Inspect `any`, broad type assertions, unchecked casts, index signatures, and suppression comments when they erase important domain guarantees.

Use escape hatches locally and explain the external constraint when the reason cannot be recovered from the code.
