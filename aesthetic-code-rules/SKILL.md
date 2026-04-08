---
name: aesthetic-code-rules
description: Use when the user wants a premium, high-end visual style with strict rules for depth, color balance, rhythm, motion, and typography. Best for UI beautification, visual refinement, design system polishing, and Chinese-first aesthetic direction.
---

# Aesthetic Code Rules

Use this skill when the user wants the UI to feel more高级, 更通透, 更精致, or explicitly asks for visual polish based on strict aesthetic rules.

This skill is for execution, not vague inspiration. Apply it while writing code, CSS, tokens, layout, motion, and component states.

## When To Use

- Beautifying an existing page, dashboard, admin panel, dialog, card, nav bar, or data surface
- Building a polished new UI with a premium, restrained, high-end look
- Creating or refining design tokens, spacing systems, visual hierarchy, and interaction feel
- Aligning multiple pages to one stronger visual language

If an existing design system is already strong, preserve its structure and apply these rules as a refinement layer instead of restyling everything.

## Priority Order

When rules conflict, follow this order:

1. readability and business clarity
2. existing product structure and interaction model
3. this skill's aesthetic rules

Do not damage usability just to chase style.

## Spatial Depth

- Elevated surfaces must use at least 3 shadow layers. Never use a single flat `box-shadow` for premium cards, dialogs, popovers, nav bars, or floating panels.
- Build shadows by increasing blur before increasing opacity.
- Prefer light, airy separation over dark heavy blur blobs.
- On dark or highlighted surfaces, add a subtle inner highlight such as `inset 0 1px 0 rgba(255,255,255,0.08)` to sharpen the edge.
- Use shadows to explain hierarchy, not to decorate every box equally.

Default starting point:

```css
box-shadow:
  0 2px 4px rgba(15, 23, 42, 0.03),
  0 8px 16px rgba(15, 23, 42, 0.05),
  0 20px 40px rgba(15, 23, 42, 0.08);
```

## Perceptual Color Balance

- Do not use absolute `#000000` or `#FFFFFF` for normal UI surfaces or text.
- Replace pure black text with softened deep neutrals such as `#111827` or nearby values.
- Replace pure white backgrounds with slightly warm or cool off-whites.
- Gray support backgrounds should carry a faint tint from the primary brand hue so the UI does not collapse into dead grayscale.
- Use opacity and alpha to create hierarchy before adding extra gray swatches.

Good direction:

- text: deep gray, not hard black
- surface: off-white, not paper white
- support background: gray with `2%` to `5%` hue bias toward the page accent

## Rhythm And Grid

- Default to an `8px` spacing rhythm for margin, padding, gaps, icon sizes, and control heights.
- Prefer `clamp()` for major outer spacing and fluid responsive spacing.
- Related items must sit visibly closer to each other than to surrounding groups.
- Avoid random one-off spacing values unless they are optical corrections with a clear reason.

Good examples:

```css
padding: 16px;
gap: 8px;
border-radius: 16px;
font-size: clamp(1rem, 0.9rem + 0.4vw, 1.125rem);
```

## Motion And Physical Feedback

- Use `cubic-bezier(0.23, 1, 0.32, 1)` for premium state changes, reveals, hover transitions, and `Transition`-driven enters/exits.
- Avoid `linear`, generic `ease`, and `transition: all`.
- Clickable elements should have a restrained press response such as `transform: scale(0.97)`.
- Press feedback should stay around `120ms` to `150ms`.
- Motion should improve hierarchy or physicality, not add noise.

Default interaction pattern:

```css
transition:
  transform 150ms cubic-bezier(0.23, 1, 0.32, 1),
  opacity 240ms cubic-bezier(0.23, 1, 0.32, 1),
  box-shadow 280ms cubic-bezier(0.23, 1, 0.32, 1);
```

```css
:active {
  transform: scale(0.97);
}
```

## Typography Tension

- Large headings should use roughly `letter-spacing: -0.02em` when the typeface and language mix support it.
- Be conservative with negative tracking in full-Chinese headings. Use it more confidently for Latin-heavy, numeric, or mixed-language display text.
- Body copy should stay in the `1.5` to `1.7` line-height range.
- Secondary text should usually step down through opacity or alpha-adjusted foreground values rather than disconnected light-gray hex codes.
- Establish hierarchy through size, weight, spacing, and contrast before adding extra decorative chrome.

## Surface Rules

- Cards are allowed only when they help grouping or interaction. Do not add cards by habit.
- Glass, blur, and gradient treatments should stay restrained and structural.
- If a panel still works as plain layout, remove extra shell treatment.
- Repeated visual effects should be tokenized with CSS variables instead of pasted as one-off styles.

Suggested tokens:

```css
:root {
  --surface-shadow-elevated:
    0 2px 4px rgba(15, 23, 42, 0.03),
    0 8px 16px rgba(15, 23, 42, 0.05),
    0 20px 40px rgba(15, 23, 42, 0.08);
  --surface-highlight: inset 0 1px 0 rgba(255, 255, 255, 0.08);
  --motion-ease-premium: cubic-bezier(0.23, 1, 0.32, 1);
  --motion-duration-press: 150ms;
}
```

## Chinese-First Notes

- Keep Chinese UI copy readable and calm. Do not over-tighten Chinese text.
- Avoid overly thin text, weak contrast, or tiny helper copy.
- For Chinese-heavy enterprise or admin UI, prefer calm structure, clean grouping, and restrained polish over flashy hero-style design.

## Delivery Checklist

Before finishing, verify:

- elevated surfaces use layered shadows
- highlighted surfaces have subtle edge definition
- no absolute black or white is used without a strong reason
- support backgrounds are not dead grayscale
- spacing mostly follows an `8px` rhythm
- interactive elements use premium easing
- clickable elements have crisp press feedback where appropriate
- heading and body typography feel balanced
- the page feels more precise, not more crowded
