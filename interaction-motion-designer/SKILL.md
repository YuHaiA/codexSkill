---
name: interaction-motion-designer
description: Use when designing hover, active, loading, success, error, reveal, and transition states. Produces motion blueprints that explain state change, attention, and physical response instead of ornamental animation.
---

# Interaction Motion Designer

Use this skill when the user asks for animation, hover behavior, press feedback, state transitions, or motion systems for a component or page.

## Intent

Animation must explain change, not merely decorate it.

For each motion task, infer:

- what changed
- why the user should notice
- whether the motion should confirm, guide, warn, or soften

## Motion Logic

Map common states to motion goals:

- hover: sharpen affordance
- active: convey physical press or commitment
- loading: communicate ongoing work without panic
- success: confirm completion with controlled energy
- error: signal correction without chaos
- enter or reveal: introduce hierarchy
- exit: remove with clarity, not abrupt disappearance

## Rules

- Use premium easing by default, especially `cubic-bezier(0.23, 1, 0.32, 1)` for polished UI.
- Prefer `transform`, `opacity`, and restrained shadow changes.
- Use spring-like emphasis only when success, delight, or release needs it.
- Use micro-shake or small lateral correction only for failure or invalid input, and keep it brief.
- Motion duration should match meaning: shorter for tactile feedback, longer for structural transitions.

## Output Requirements

When using this skill, generate:

- a motion blueprint for each important interaction state
- the intent behind the motion
- concrete CSS or framework-friendly transition suggestions
- physical metaphors when they improve comprehension

## Hard Rules

- Do not animate everything.
- Do not use animation that fights readability or data scanning.
- Do not use the same motion pattern for success and error.
- Do not make loading feel alarming or error feel playful unless the product explicitly wants that tone.

## Delivery Check

Before finishing, verify:

- each motion has a purpose
- press and hover states feel responsive
- success and failure states are clearly different
- motion improves understanding or affordance
- the system feels intentional, not random
