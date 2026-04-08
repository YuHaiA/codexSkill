---
name: premium-ui-polish
description: Apply premium visual polish to cards, dialogs, overlays, nav bars, and motion-heavy UI. Use when refining interface quality, interaction feel, shadow depth, typography, glass surfaces, CSS styling systems, or frontend presentation details.
---

# Premium UI Polish

Use this skill when the task depends on making the UI feel sharper, deeper, calmer, and more expensive without changing the product structure.

Default goal: preserve the existing layout and business flow, but upgrade spatial depth, edge definition, easing, typography, and translucent surfaces.

## Core Rules

- Do not use a single `box-shadow` for elevated surfaces. Use layered shadows to simulate ambient light plus directional falloff.
- Cards, dialogs, drawers, popovers, nav bars, and floating panels should have a subtle edge definition. Prefer a translucent `border` or an `inset` highlight.
- Do not use `linear` or plain `ease` for hover, fade, scale, or panel transitions. Use a premium deceleration curve.
- Headline typography should feel optically tightened. Body copy should feel breathable.
- For glass or overlay surfaces, combine blur with a restrained translucent fill so the result feels dense rather than cheap.
- Prefer polish that improves quality perception without adding visual noise.
- Avoid absolute `#000000` and `#FFFFFF` on polished UI surfaces. Prefer softened neutrals and slightly tinted support backgrounds.
- Keep polish aligned to an `8px` spacing rhythm unless a smaller optical correction is clearly justified.

## Physical Shadow Layering

Every elevated container should use at least three shadow layers with different blur radii and opacities.

Use this pattern as the default starting point:

```css
box-shadow:
  0 1px 2px rgba(0, 0, 0, 0.02),
  0 4px 8px rgba(0, 0, 0, 0.02),
  0 12px 24px rgba(0, 0, 0, 0.03);
```

Guidelines:

- Treat the smallest layer as contact depth.
- Treat the middle layer as ambient softness.
- Treat the largest layer as separation from the background.
- Increase blur before increasing opacity.
- Avoid muddy shadows. If the surface feels heavy, reduce alpha before reducing blur.
- On dark UI, prefer cooler and softer shadows rather than dense black blobs.
- Use larger-radius, lower-alpha outer layers before reaching for darker shadows.

## Subtle Inner Border

All cards and dialogs should have a micro edge treatment.

Default options:

```css
border: 1px solid rgba(255, 255, 255, 0.1);
```

or

```css
box-shadow:
  inset 0 1px 0 rgba(255, 255, 255, 0.08);
```

Guidelines:

- Use this especially on dark, blurred, or low-contrast surfaces.
- Keep the border visually quiet. It should sharpen the silhouette, not outline it loudly.
- On light cards, use a slightly darker translucent border instead of bright white if needed.
- On dark or highlighted surfaces, an `inset 0 1px 0 rgba(255,255,255,0.08-0.12)` style highlight is the default move, not a special effect.

## Perceptual Color Balance

- Replace sterile grayscale fills with lightly tinted neutrals that borrow `2%` to `5%` from the current accent hue.
- Use deep gray for primary text instead of pure black, and softened off-white for bright surfaces instead of pure white.
- Build hierarchy with opacity, alpha, and contrast before introducing extra named gray swatches.
- If the UI already has brand tokens, tint support surfaces through those tokens instead of inventing detached decorative colors.

## Apple-Standard Easing

Default transition curve:

```css
transition-timing-function: cubic-bezier(0.23, 1, 0.32, 1);
```

Timing rules:

- Hover and small emphasis changes: `200ms` to `280ms`
- Panel, modal, drawer, and reveal transitions: `280ms` to `400ms`
- Keep opacity, transform, and shadow transitions synchronized unless there is a strong reason not to.
- Active press feedback for clickable controls should be tighter: around `120ms` to `150ms`.

Do not use:

- `transition: all`
- `linear`
- generic `ease`

Prefer targeted transitions such as:

```css
transition:
  transform 260ms cubic-bezier(0.23, 1, 0.32, 1),
  opacity 260ms cubic-bezier(0.23, 1, 0.32, 1),
  box-shadow 320ms cubic-bezier(0.23, 1, 0.32, 1);
```

Clickable-surface feedback default:

```css
transition:
  transform 150ms cubic-bezier(0.23, 1, 0.32, 1),
  box-shadow 260ms cubic-bezier(0.23, 1, 0.32, 1);
```

```css
:active {
  transform: scale(0.97);
}
```

## Retina Typography Tuning

For large headings:

```css
letter-spacing: -0.02em;
```

For body copy:

```css
line-height: 1.6;
```

For fluid type:

```css
font-size: clamp(1rem, 2vw + 0.5rem, 1.5rem);
```

Guidelines:

- Use negative tracking on `h1` to `h3` unless the typeface becomes too tight in Chinese text.
- Be conservative with negative tracking in Chinese UI; use it mainly for Latin-heavy headings, numbers, or mixed-language hero text.
- Use `clamp()` for responsive type and spacing when the page needs to scale smoothly without breakpoint-heavy overrides.
- If the page already uses a consistent type scale, extend that scale instead of inventing a parallel one.
- Keep body copy around `1.5` to `1.7` line-height.
- Establish lower hierarchy through opacity or alpha-adjusted foreground values instead of swapping to random light grays.

## Grainy Glassmorphism

For overlays, sticky nav bars, and floating tool surfaces, start from:

```css
backdrop-filter: blur(12px);
```

Pair it with a translucent fill, ideally in perceptual color space when supported:

```css
background: oklch(1 0 0 / 0.08);
```

Guidelines:

- Keep glass surfaces restrained. Blur should support layering, not become a gimmick.
- Use a very subtle noise or texture treatment when large translucent areas feel too flat.
- If noise is not already part of the project, prefer a tiny pseudo-element texture or a faint gradient stack instead of introducing heavy assets.
- Ensure contrast stays readable over mixed backgrounds.

## CSS Engineering Rules

- Centralize repeated polish tokens in CSS custom properties when the same surface language appears multiple times.
- Prefer variables for shadow stacks, border colors, blur values, easing curves, and duration scales.
- Keep tokens semantic. Good examples: `--surface-shadow-elevated`, `--surface-border-subtle`, `--motion-ease-premium`.
- Do not add decorative one-off effects directly in many files if they can be standardized once.
- Prefer `transform` and `opacity` for interaction animation over layout-triggering properties.

Recommended token starter:

```css
:root {
  --surface-shadow-elevated:
    0 1px 2px rgba(0, 0, 0, 0.02),
    0 4px 8px rgba(0, 0, 0, 0.02),
    0 12px 24px rgba(0, 0, 0, 0.03);
  --surface-border-subtle: rgba(255, 255, 255, 0.1);
  --motion-ease-premium: cubic-bezier(0.23, 1, 0.32, 1);
  --motion-duration-press: 150ms;
}
```

## Rhythm And Grouping

- Use an `8px` spacing grid for padding, margin, icon sizes, and control heights by default.
- Prefer `clamp()` for responsive outer spacing on containers, dialogs, and section padding.
- Respect proximity: spacing inside a semantic cluster should be clearly smaller than spacing between separate clusters.

## Rendering Performance

Premium polish must still feel fast.

- Animate `transform`, `opacity`, `filter`, and carefully chosen shadow changes only when necessary.
- Avoid large constantly animating blur fields or oversized shadow repaints on dense lists.
- Use glass and blur selectively on high-value surfaces, not every container.
- If many cards appear at once, use a lighter resting shadow and stronger hover shadow instead of heavy elevation everywhere.
- Prefer a small number of memorable motions over many simultaneous ones.

## Quality Checks

Before finishing a polished UI task, verify:

- Elevated surfaces use at least three shadow layers.
- Cards or dialogs have a subtle edge treatment.
- Motion uses `cubic-bezier(0.23, 1, 0.32, 1)` or a clearly related premium deceleration curve.
- Clickable elements have crisp physical feedback when the interaction pattern benefits from it.
- Headings and body copy feel optically balanced.
- Glass surfaces use blur plus restrained translucency.
- Support surfaces do not collapse into dead grayscale.
- The page feels more precise and more premium, not more decorated.
