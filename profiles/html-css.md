# HTML / CSS Profile

Markup and styling become difficult to understand when visual behavior depends on distant selectors, implicit document structure, specificity accidents, or JavaScript that mutates classes and attributes without a clear contract.

## Semantic structure

Use HTML elements and landmarks that express the document's actual structure and interaction role.

Inspect generic `div` / `span` nesting when the hierarchy carries real concepts that deserve semantic elements, stable component boundaries, or explicit naming.

## DOM identity

IDs, classes, data attributes, ARIA relationships, form names, and selectors used by scripts or tests form an API surface. Keep consequential identities stable and searchable.

Avoid selectors whose meaning depends on fragile positional structure when a semantic identity would be clearer.

## Accessibility relationships

Keep label/control relationships, keyboard interaction, focus order, ARIA ownership, live regions, and interactive semantics locally recoverable.

Do not use ARIA as a hidden repair layer for markup whose intended interaction cannot otherwise be understood.

## CSS ownership

A reader should be able to discover which style rule owns a visual behavior.

Inspect:

```text
high-specificity selector chains
frequent `!important`
global selectors with distant side effects
styles depending on deep DOM ancestry
class names with no domain or component meaning
multiple unrelated files mutating the same component state
```

Prefer local component/style ownership and predictable cascade boundaries.

## State encoded in classes and attributes

When JavaScript or a framework changes UI state through classes, attributes, or data values, keep the state vocabulary explicit and searchable.

Prefer named states such as `data-loading`, `aria-expanded`, or a clear component state class over combinations whose meaning emerges only from several selectors.

## Layout and visual constants

Explain only non-obvious layout constraints that encode a real external requirement: browser workaround, embedded environment, print behavior, fixed media geometry, accessibility requirement, or cross-component contract.

Ordinary CSS does not need narration.

## Generated markup and templates

When templates, preprocessors, SSR, hydration, or build tools generate final markup, keep the source-to-runtime relationship discoverable. A reader debugging the browser DOM should have a clear path back to the source template or component.
