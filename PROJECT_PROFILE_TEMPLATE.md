# Project Profile Template

Keep this file short. Record only repository-specific semantics that are unusually expensive to misunderstand.

## Domain vocabulary

```text
concept -> canonical spelling
concept -> canonical spelling
```

Use one stable term for one important concept where practical.

## State ownership

```text
state / resource -> owner -> named write path
```

Record only ownership relationships that are not obvious from the language or local type structure.

## Workflow invariants

```text
high-level stage A
-> stage B
-> stage C
```

List only invariants whose accidental reordering or bypass would change behavior.

## External dependency boundaries

```text
dependency:
  project responsibility delegated to it:
  guarantee relied on:
  local adapter / boundary:
  replacement-sensitive assumption:
```

Do not document the library's whole API.

## Domain-specific hazards

Examples:

```text
physical units must remain visible in names
persisted event names are compatibility surface
routing policy must remain separate from transport mechanism
server state and client state must have distinct owners
binary layout is external ABI
```

## Required validation

```text
command / test suite / behavioral comparison
```

## Refactor exclusions

List generated code, vendored code, migration history, or other regions that should not be mechanically normalized unless the task explicitly includes them.
