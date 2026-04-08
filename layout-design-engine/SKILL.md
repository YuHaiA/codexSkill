---
name: layout-design-engine
description: Use when designing a component, page section, form, list, card cluster, dashboard area, or information layout from function and priority instead of from a fixed starter template. Generates semantic structure and balanced CSS Grid or Flex layouts.
---

# Layout Design Engine

Use this skill when the user asks to design a component, page section, or UI structure and the main challenge is layout synthesis rather than visual skinning.

## Intent

Do not start from a copied HTML skeleton. First infer:

- the component's main job
- the information priority
- the expected scanning path
- the primary action and secondary action

Then generate the semantic structure and layout from that logic.

## Workflow

Before writing markup, decide:

1. what the user needs to notice first
2. what they need to understand second
3. what they need to do next

Map that into:

- semantic HTML regions
- a reading path
- a layout system using Grid first and Flex where local alignment is enough

## Layout Rules

- Follow Gutenberg, F-pattern, or Z-pattern reading behavior based on the component type.
- Put the visual and informational center of gravity where scanning naturally begins.
- Keep primary information closer to the entry point and higher in the DOM unless accessibility or interaction rules require otherwise.
- Use CSS Grid for macro layout and Flex for micro alignment.
- Default to intrinsic layout behavior before fixed breakpoint choreography.
- Respect the existing spacing rhythm and proximity rules from the active design system.

## Output Requirements

When using this skill, generate:

- semantic HTML structure
- a layout explanation in one or two sentences when needed
- Grid or Flex rules that explain hierarchy instead of merely placing boxes
- a mobile-first layout that still works when content grows

## Common Patterns

For forms:

- label, helper, field, validation, and action zones should read as one task flow
- related fields should cluster together
- primary submit action should be visually obvious and structurally last

For tables and data panels:

- filters and summary controls should sit in a clear pre-table control zone
- the scanning path should lead from title to filters to summary to data

For cards or item lists:

- image, title, metadata, status, and actions should follow narrative priority, not arbitrary columns

## Hard Rules

- Do not start with a random nested `div` tree.
- Do not use Grid and Flex interchangeably without reason.
- Do not place primary actions where scanning reaches them too late.
- Do not let decorative balance override reading efficiency.

## Delivery Check

Before finishing, verify:

- the structure is semantic
- the reading path is obvious
- the layout supports the information priority
- the component works in narrow and wide containers
- the structure feels designed, not scaffolded
