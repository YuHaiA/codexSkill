---
name: advanced-color-synthesizer
description: Use when the user provides a brand color or needs a full semantic color system with accessible ramps, neutral surfaces, and dark-mode pairing. Synthesizes color scales and contrast-safe UI tokens.
---

# Advanced Color Synthesizer

Use this skill when the user gives a seed color or asks for a color system, theme tokens, accessible color ramps, semantic statuses, or dark-mode pairings.

## Intent

Do not hand-pick a few similar hex values. Build a semantic system from one brand seed with contrast and perceptual consistency as first-class constraints.

## Inputs

Typical input:

- `primary-color: #XXXXXX`

Optional context:

- product tone
- light only or light + dark
- existing accent families
- whether the result should favor calm enterprise UI or expressive marketing UI

## Workflow

1. Start from the seed color and infer hue character.
2. Build a perceptually smooth ramp, ideally thinking in OKLCH terms even if the final output is hex.
3. Generate semantic families:
   - primary
   - secondary or accent
   - success
   - warning
   - danger if needed
   - neutral
   - surface
4. Verify contrast for text on key surfaces.
5. Produce dark-mode counterparts when the task benefits from them.

## Output Requirements

When using this skill, output:

- a 10-step primary ramp when appropriate
- neutrals and surfaces that harmonize with the seed instead of ignoring it
- semantic token suggestions for foreground, surface, border, hover, active, and focus states
- contrast-safe text/background pair recommendations

## Color Rules

- Prefer softened neutrals over dead grayscale.
- Surface colors should borrow a subtle hue bias from the system instead of becoming detached gray.
- Preserve brand identity without sacrificing readability.
- If a vivid seed color is hard to use as a surface, keep it for accents and derive safer surface tones around it.
- Do not force equal saturation across all states; keep support surfaces quieter than accents.

## Accessibility Rules

- Treat contrast as a hard requirement, not a nice-to-have.
- Prioritize readability for body text, controls, data tables, badges, and alerts.
- When a brand color fails on white or dark surfaces, generate a safer adjacent step for text and interface use.

## Delivery Check

Before finishing, verify:

- the system includes semantic roles, not just pretty swatches
- light surfaces and text combinations are readable
- dark-mode pairs are intentional when present
- neutrals belong to the same family as the brand
- the palette can actually be used in a product UI
