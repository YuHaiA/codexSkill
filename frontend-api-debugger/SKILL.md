---
name: frontend-api-debugger
description: Diagnose frontend API integration issues in web applications. Use when requests fail, auth headers or tokens are wrong, payloads do not match backend expectations, response mapping breaks the UI, environment or base URL setup is wrong, forms submit incorrect data, or list and detail pages show stale or malformed backend data.
---

# Frontend Api Debugger

## Overview

Use this skill to turn vague "接口不对" or "页面没数据" problems into a concrete failure point. Trace the issue from UI event to request builder to network contract to response mapping before changing code.

## Triage Order

1. Reproduce the exact failing flow.
   - Identify which click, form submit, route load, or lifecycle event triggers the bad request or bad data.
2. Inspect the request contract.
   - Confirm URL, method, query params, body shape, headers, auth token, content type, and environment base URL.
3. Inspect the response contract.
   - Confirm success flag, payload nesting, pagination shape, enum values, nullability, and field names used by the page.
4. Trace the transform layer.
   - Check request helpers, interceptors, API wrappers, store actions, and page-level mapping code.
5. Isolate the source of truth.
   - Decide whether the bug is frontend-only, environment-only, contract drift, or likely backend behavior.
6. Apply the narrowest correct fix.
   - Prefer fixing the incorrect mapping or request builder instead of adding defensive hacks everywhere.

## Common Failure Buckets

- wrong environment or base URL
- missing or stale auth token
- request method or payload shape mismatch
- frontend expects `data.records` while backend returns `data.list`
- enum or boolean value mismatch
- pagination fields mismatch such as `total`, `count`, `pages`, or `items`
- form values not normalized before submit
- stale state after mutation because refresh logic is missing

## Debugging Heuristics

- Compare a working page and a broken page if the repo already has similar flows.
- Prefer logging precise intermediate values over broad console spam.
- Inspect where payloads are shaped, not just where API functions are declared.
- When the UI is empty, verify whether the problem is "request never fired", "response empty", or "response parsed wrong".
- When submit seems successful but the UI is stale, inspect refresh timing and cache or store invalidation first.

## Guardrails

- Do not paper over contract mismatches with silent fallback defaults unless the UI genuinely supports them.
- Do not change backend contracts by assumption; state clearly when a fix is an inference.
- Do not log secrets, tokens, or private user data into source files.
- Keep temporary debugging output easy to remove.

## Output Expectations

- Name the failing layer clearly: trigger, request shaping, transport, response parsing, store mapping, or UI rendering.
- Explain the observed mismatch in one sentence before patching.
- After fixing, mention what was verified and what still depends on backend confirmation.

## Example Triggers

- "This page says success but the table never refreshes."
- "The backend returns data, but the Vue page renders empty rows."
- "Why does this form submit the wrong payload?"
