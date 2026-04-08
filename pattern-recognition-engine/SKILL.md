---
name: pattern-recognition-engine
description: Use when repeated layout, styling, or component code suggests a reusable pattern. Extracts a generalized design pattern, component, mixin, token set, or API instead of continuing hard-coded duplication.
---

# Pattern Recognition Engine

Use this skill when the codebase or generated UI starts repeating the same visual or structural pattern in slightly different forms.

## Intent

When repetition appears, stop duplicating and synthesize a reusable pattern.

Look for repeated:

- layouts
- card shells
- filter bars
- stat blocks
- button groups
- dialog structures
- shadow, spacing, or motion recipes

## Workflow

1. Identify the repeated pattern.
2. Separate stable structure from variable inputs.
3. Decide whether the right abstraction is:
   - a component
   - a slot-based shell
   - a config-driven renderer
   - a mixin or utility class
   - a token set
4. Keep the abstraction small enough to stay understandable.

## Extraction Rules

- Preserve the strongest existing version of the pattern as the baseline.
- Parameterize the parts that genuinely vary.
- Do not abstract business logic that should remain local.
- Prefer semantic props and slots over a giant prop soup.
- If the abstraction makes the call site harder to understand, it is too clever.

## Output Requirements

When using this skill, produce:

- the proposed reusable pattern
- what remains configurable
- what should stay fixed
- a migration path from hard-coded repetition to the new abstraction

## Atomic Design Guidance

- If the repeated element is primitive, extract a smaller atom.
- If the repeated element is a stable cluster, extract a molecule or shared shell.
- If the pattern crosses screens, consider a system token or shared layout primitive.

## Delivery Check

Before finishing, verify:

- duplication is meaningfully reduced
- the abstraction is easier to reuse than the old copy-paste approach
- variation is parameterized cleanly
- the result still matches the product's visual standard
