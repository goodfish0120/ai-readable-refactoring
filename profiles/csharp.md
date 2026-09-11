# C# Profile

Run these concerns separately.

## Runtime attributes and reflection

Inspect attributes, reflection, dynamic proxies, interception, source/runtime registration, and framework conventions that change behavior outside the visible call graph.

Keep consequential framework behavior behind explicit integration boundaries when practical.

## Dependency injection and ownership

Inspect ambiguous runtime bindings, service-locator access, broad `IServiceProvider` use, and interfaces whose selected implementation is difficult to discover.

## LINQ and deferred execution

Inspect long LINQ chains when they contain several domain stages, repeated enumeration, important deferred execution, hidden I/O, or mutation.

Prefer named intermediate stages when they preserve when work happens and what each stage means.

## Events and delegates

Inspect event/delegate flows whose subscribers are difficult to discover. Important event systems should expose a dispatch or subscription map.

## Async and resource lifetime

Make Task ownership, cancellation, fire-and-forget behavior, `IDisposable` / `IAsyncDisposable` lifetime, and transaction scope visible when they affect correctness.

## Extension methods

Use extension methods for locally obvious convenience. Keep important behavior on a discoverable owner or boundary when an extension would obscure where the implementation lives.
