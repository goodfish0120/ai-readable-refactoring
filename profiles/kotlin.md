# Kotlin Profile

Apply the Java profile where the code uses JVM frameworks, then inspect Kotlin-specific compression separately.

## Scope-function compression

Inspect nested `let`, `run`, `apply`, `also`, and `with` chains when repeated `it` / `this` context switching hides object identity or state ownership.

Prefer ordinary named variables and named operations when the compressed form forces the reader to mentally reconstruct receivers.

## Extension ownership

Inspect extension functions that make consequential behavior look like it belongs to a type that does not actually own it.

Convenience extensions are fine. Core domain behavior should have discoverable ownership.

## DSL and operator magic

Inspect DSLs and operator overloads when ordinary control flow, I/O, mutation, expensive work, or lifecycle transitions become visually invisible.

## Coroutine lifetime

Inspect `launch`, `async`, detached scopes, shared flows, channels, and cancellation paths for explicit ownership.

A reader should be able to answer who starts the work, who waits for it, who cancels it, and what survives the caller.

## Nullability and sealed state

Use Kotlin's type system to preserve state distinctions when it reduces invalid combinations. Avoid collapsing stable domain states into maps, strings, or nullable fields whose legal combinations must be reconstructed manually.
