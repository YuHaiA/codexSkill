---
name: vue3-admin-crud
description: Build, refactor, and review common Vue 3 admin CRUD pages and back-office workflows. Use when Codex needs to add or modify search forms, tables, pagination, create or edit dialogs, drawers, detail views, route wiring, store integration, page-level loading states, or list-detail CRUD flows in Vue 3 frontend projects.
---

# Vue3 Admin Crud

## Overview

Use this skill to ship the high-frequency pages most admin systems need: searchable lists, detail pages, create or edit forms, and common action flows. Start by matching the repo's existing page structure and component patterns instead of inventing a new architecture.

## Default Flow

1. Inspect nearby pages before editing.
   - Reuse the project's existing layout, request utilities, store usage, route naming, and component split.
   - Match the team's Composition API or Options API style instead of mixing patterns casually.
2. Identify the page type.
   - `list page`: query form, table, pagination, row actions, bulk actions
   - `form page`: create, edit, detail, or audit form
   - `hybrid page`: list plus dialog, drawer, or side panel form
3. Define the data contract early.
   - Confirm request params, response fields, id fields, enum values, and loading or error states before shaping UI code.
   - Map backend fields explicitly when labels and payload names differ.
4. Implement the smallest coherent flow first.
   - Make the main happy path work before polishing secondary actions.
   - Prefer a complete searchable list or complete submit flow over half-finished extras.
5. Finish with state handling.
   - Handle loading, empty states, disabled states, submit-in-progress states, and success refresh behavior.

## Common Page Shape

For a typical admin CRUD page, prefer this order unless the repo clearly uses another one:

- query controls at the top
- primary table or list in the middle
- pagination at the bottom
- row actions close to the row they affect
- create or edit interaction in a dialog, drawer, or route-based form that matches existing patterns

For forms, prefer:

- clear grouping by business meaning
- defaults derived from existing records or route params
- validation that blocks bad submits before hitting the API when feasible
- success handling that closes, resets, or navigates consistently
- precise field-to-payload mapping instead of broad object spreading when contracts are fragile

## Decision Points

- Keep logic inline in the page when the workflow is short and local.
- Extract child components when the table, filter form, or editor is reused or too large to read comfortably.
- Use route pages for larger create or edit experiences.
- Use dialogs or drawers for fast edits that should preserve list context.
- Re-fetch after mutations unless the repo already uses optimistic updates consistently.

## Guardrails

- Do not replace existing project conventions with generic boilerplate.
- Do not mix pagination naming, enum handling, or form schemas across pages without a reason.
- Do not silently swallow API failures; show actionable feedback and preserve recoverability.
- Do not over-abstract a one-off page into a reusable framework unless the repo already leans that way.
- Keep destructive actions explicit with confirmation and disabled states.

## Done Criteria

- The main list or form flow works end to end.
- Loading, empty, and submission states are visible and coherent.
- API field mapping is intentional and easy to trace.
- New code looks like it belongs in the repo beside neighboring pages.

## Example Triggers

- "Add a member management page with filters, table, pagination, and edit dialog."
- "Refactor this Vue 3 list page to match the rest of the admin system."
- "Create a detail plus edit flow for this back-office resource."
