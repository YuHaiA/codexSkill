---
name: element-plus-patterns
description: Implement and refactor robust Element Plus UI flows in Vue 3 projects. Use when Codex needs Element Plus forms, tables, filters, pagination, dialogs, drawers, validation, upload interactions, destructive confirmations, async submit states, or polished create, edit, detail, and review flows built on Element Plus.
---

# Element Plus Patterns

## Overview

Use this skill when the UI is already using Element Plus or should stay aligned with Element Plus conventions. Favor predictable, maintainable form and table behavior over flashy abstractions.

## Core Patterns

### Forms
- Keep labels, required markers, validation rules, and submit feedback consistent.
- Normalize model values before submit when widgets return UI-friendly shapes.
- Disable submit while async save is in flight.
- Preserve user input on failure unless the repo clearly resets forms differently.

### Tables and Filters
- Keep filter controls close to the table they affect.
- Separate query state from display-only state.
- Reset pagination when filters change.
- Show loading, empty, and row-action disabled states explicitly.

### Dialogs and Drawers
- Use dialogs for short, focused edits.
- Use drawers or route pages for longer forms or flows needing more context.
- Reset or rehydrate form state intentionally when opening and closing.
- Keep destructive or submit buttons easy to find and hard to misfire.

### Validation and Feedback
- Prefer inline rule validation for field-level issues.
- Use concise message feedback for save, delete, or request outcomes.
- Distinguish validation failure, business-rule rejection, and transport failure.

## Implementation Order

1. Match existing Element Plus component usage in the repo.
2. Define the state model for query, form, loading, and visibility.
3. Build the happy path interaction first.
4. Add validation, disabled states, and feedback.
5. Polish edge cases like reset, reopen, pagination reset, and failed submit recovery.

## Guardrails

- Do not mix Element Plus with unrelated custom widgets unless the repo already does.
- Do not create overly generic wrappers for a one-off form or table.
- Do not leave dialog visibility, loading, and model reset behavior implicit.
- Keep action buttons and confirmation flows consistent across similar pages.

## Good Defaults

- list pages: filters above table, pagination below, refresh after mutation
- dialog forms: initialize model on open, validate on submit, disable submit while saving
- destructive actions: explicit confirm, loading state, success feedback, table refresh
- async detail loads: skeleton or loading indicator before rendering dependent fields

## Example Triggers

- "Refactor this Element Plus dialog form so reset and submit behavior are correct."
- "Build a searchable Element Plus table with row actions and pagination."
- "Why does this Element Plus form keep stale values when reopened?"
