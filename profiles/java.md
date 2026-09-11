# Java Profile

Run each category as a separate pass.

## Framework-driven hidden execution

Inspect annotations that alter transactions, retries, caching, authorization, async execution, persistence, routing, or lifecycle.

Inspect reflection, dynamic proxies, AOP/interceptors, runtime registration, and framework callbacks when they change core semantics.

Framework magic may remain behind an explicit integration boundary. Domain flow should remain understandable without reconstructing the whole container.

## Dependency injection ambiguity

Inspect injected interfaces whose concrete implementation is difficult to discover, string-based bean/service lookup, conditional runtime bindings, and configuration that changes ownership invisibly.

Keep the selected responsibility and replacement boundary locally recoverable.

## Deep indirection

Inspect large inheritance hierarchies, template-method chains, listeners, factories returning unrelated implementations, and service locator patterns that make active behavior hard to identify.

Prefer composition and explicit domain-facing interfaces when they reduce navigation cost.

## Domain decisions hidden as flags

Replace opaque boolean arguments and generic maps with named options, enums, value objects, or explicit configuration types when the call site otherwise requires lookup.

## Exceptions and lifecycle

Make transaction ownership, retry boundaries, resource ownership, asynchronous lifetime, and exception translation visible where they affect system behavior.
