---
name: adaptive-structure-architect
description: Use when designing responsive components that should evolve structurally across mobile, tablet, and desktop. Favors intrinsic, content-led adaptation over brittle breakpoint-only resizing.
---

# Adaptive Structure Architect

Use this skill when the user asks for responsive design, cross-device layout behavior, or a component that should evolve structurally instead of merely shrinking.

## Intent

Do not solve responsiveness only by scaling dimensions down.

Design how the structure itself should evolve across available space:

- multi-column to stacked
- side panel to inline section
- toolbar to wrapped control clusters
- dense table to card or accordion representation when needed

## Workflow

1. Identify the component's core content.
2. Decide what must remain visible at all sizes.
3. Decide what can collapse, wrap, reorder, or become progressive disclosure.
4. Prefer intrinsic layout behavior based on content and container space.

## Rules

- Use mobile-first thinking.
- Prefer content-driven adaptation over hard-coded device assumptions.
- Avoid brittle breakpoint choreography when `auto-fit`, `minmax()`, wrapping, or intrinsic sizing can solve it more naturally.
- When the structure changes, preserve task continuity and reading order.
- If dense desktop UI becomes unusable on small screens, redesign the structure instead of shrinking text into failure.

## Output Requirements

When using this skill, generate:

- a baseline narrow-screen structure
- how the structure expands in larger containers
- what transforms at extreme widths
- responsive CSS that favors intrinsic design patterns where practical

## Good Transformations

- data summary row becomes stacked metric blocks
- sidebar becomes top section or drawer
- complex filter bar becomes wrapped groups or collapsible advanced filters
- desktop multi-column content becomes a readable vertical narrative on small screens

## Hard Rules

- Do not rely only on hard-coded breakpoints if the component can self-adapt.
- Do not preserve desktop structure at the cost of mobile comprehension.
- Do not hide critical content without a clear alternate path.

## Delivery Check

Before finishing, verify:

- the narrow layout is intentional, not an afterthought
- the large layout earns its extra space
- structural changes preserve meaning and action flow
- the component remains readable in extreme viewports
