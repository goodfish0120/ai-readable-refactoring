# Frontend Framework Profile

Load this beside the JavaScript/TypeScript and HTML/CSS profiles when working in React, Vue, Svelte, Angular, or another stateful UI framework.

Frameworks differ in syntax. The recurring readability hazards are state ownership, reactive causality, lifecycle, generated execution, and boundaries between server and client state.

## State ownership

For every important piece of UI state, make the owner recoverable:

```text
server response
router / URL
shared client store
page / feature container
local component
form library
browser storage
```

Avoid duplicating the same conceptual state across several owners without a clear synchronization rule.

## Reactive causality

Inspect effects, watchers, computed reactions, subscriptions, signals, hooks, observers, and framework lifecycle callbacks when they cause important work indirectly.

A reader should be able to recover:

```text
which state change triggers the reaction
what work the reaction performs
which state or external system it changes
what prevents loops or duplicate execution
when the reaction is disposed
```

## Lifecycle ownership

Make mount/unmount, subscription cleanup, timers, async requests, cancellation, observers, and external resources visibly tied to the component or feature that owns them.

## Effect discipline

Keep pure derivation separate from side effects when the framework permits it.

A value that can be derived from existing state should usually look like derivation. Network calls, persistence, analytics, DOM mutation, subscriptions, and synchronization should look consequential.

## Component boundaries

Component extraction should correspond to a meaningful UI concept, state owner, repeated semantic unit, or lifecycle boundary.

Avoid fragmentation into tiny components that require opening many files to understand one local interaction.

Avoid giant components that mix data acquisition, policy, rendering, state transitions, networking, and styling at one abstraction height.

## Props and events

Keep input/output contracts explicit. Avoid large anonymous prop bags, callback collections with generic names, and events whose payload shape must be inferred from implementation.

## Context / provide-inject / global stores

Shared context is useful when ownership is genuinely broader than one subtree. Inspect context and global stores that become invisible dependency injection for ordinary local state.

Important shared state should have a discoverable definition, write path, and consumer boundary.

## Server/client boundary

In SSR, hydration, server components, islands, or hybrid rendering, keep these distinctions recoverable:

```text
where code executes
where data originates
what is serialized across the boundary
what is re-run on the client
what state survives hydration
```

## Framework magic

Compiler transforms, generated routes, auto-imports, convention-based loaders, decorators, directives, dependency injection, and build-time code generation may remain idiomatic.

When they own consequential domain behavior, expose a stable project-facing boundary or short rationale so a future reader does not have to reconstruct the framework compiler before changing the feature.
