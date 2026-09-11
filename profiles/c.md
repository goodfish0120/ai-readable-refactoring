# C Profile

C often keeps control flow visible while hiding physical-state assumptions. Refactor those assumptions one category at a time.

## Ownership

Inspect every important pointer crossing a boundary for allocation, ownership, borrowing, mutation rights, and release responsibility.

A reader should be able to answer:

```text
who creates it
who owns it
who may mutate it
how long it remains valid
who releases it
```

## Buffers

Keep pointer, length, and capacity relationships visible. Avoid APIs where buffer bounds must be inferred from unrelated state or sentinel conventions unless that convention is stable and explicit.

## Aliasing

Document or encode aliasing assumptions when correctness or optimization depends on them.

## Type erasure and sentinels

Inspect `void *`, magic integers, bit flags, sentinel values, and generic integer error codes when they erase stable domain meaning.

Prefer enums, named constants, typed structs, and small result structures when they make legal states clearer.

## Macros

Inspect macros that hide control flow, mutation, ownership, resource acquisition, or repeated argument evaluation.

Prefer ordinary functions or `static inline` functions when macro semantics are unnecessary.

## Cleanup and errors

Keep cleanup ownership and error propagation consistent. A clear `goto cleanup` can be preferable to duplicated or partially divergent cleanup paths.

## ABI and layout

Explain non-obvious assumptions about struct layout, alignment, packing, endian behavior, binary formats, calling conventions, or external ABI compatibility where those assumptions cross a boundary.

## Globals

Inspect mutable globals and implicit singleton state. Make initialization order and write ownership visible when global state is unavoidable.
