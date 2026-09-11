# C++ Profile

Apply the C profile where physical-state hazards still apply, then inspect C++-specific abstraction and lifetime behavior separately.

## Ownership and lifetime

Inspect raw pointers with unclear ownership, reference captures whose lifetime is non-obvious, shared ownership without a clear reason, and objects whose destruction carries important side effects.

Use RAII when it makes ownership and cleanup more explicit. Explain the non-obvious lifetime relationship, not RAII itself.

## Template complexity

Inspect template metaprogramming, traits, concepts, policy layers, and generated type machinery when a reader must instantiate a large compile-time model to understand ordinary domain behavior.

Keep advanced template machinery behind a clear semantic boundary when possible.

## Operator and conversion behavior

Inspect operator overloads and implicit conversions that hide allocation, I/O, mutation, synchronization, expensive computation, or surprising ownership changes.

## Inheritance and dispatch

Inspect multiple inheritance, deep virtual hierarchies, CRTP, and factory/trait combinations when the active implementation is difficult to identify.

## Macro-heavy abstraction

Apply the C macro rules. Avoid macro systems that create a second hidden language over ordinary control flow unless the project genuinely requires them.

## Concurrency

Make thread/task ownership, lock ownership, shared-state boundaries, atomic assumptions, and callback lifetime visible when correctness depends on them.
