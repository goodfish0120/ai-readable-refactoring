# Python Profile

Run these as focused passes, not as one rewrite.

## Hidden execution

Inspect decorators that alter transactions, retries, caching, authorization, registration, routing, async behavior, or lifecycle. Core behavior should remain discoverable from the call path.

Inspect metaclasses, `__getattr__`, `__getattribute__`, descriptors, monkey patching, and runtime attribute injection when they carry domain behavior.

## Weak interface shape

Inspect `*args` and `**kwargs` across important boundaries, generic dictionaries carrying stable domain state, positional booleans, and magic strings representing events or states.

Prefer explicit signatures, named arguments, dataclasses or small domain types, enums, and discoverable dispatch maps.

## Dense expressions

Inspect nested comprehensions, stacked lambdas, generator pipelines with important evaluation timing, and expressions combining filtering, branching, mutation, and I/O.

Prefer named intermediate stages when several semantic transitions are present.

## State and lifetime

Inspect mutable module-level state, shared mutable defaults, non-obvious context-manager effects, hidden lazy evaluation, and async tasks whose ownership is unclear.

Make state owner, write path, resource lifetime, and task lifetime visible.

## Dynamic capability

Python makes runtime adaptation easy. Keep dynamic behavior near integration boundaries when practical. Domain flow should remain explicit enough that a reader can understand it without simulating Python's object model.
