# Session Extraction Rules

## Read in this order

1. `session_index.jsonl`
2. session `session_meta`
3. the smallest relevant slice of the session file

## Pick only sessions that match

- current `cwd`
- current project root
- current thread goal
- the most recent stable resolution of a repeated issue

## Keep

- project goals
- architecture decisions
- directory layout rules
- coding conventions
- tool/workflow preferences that repeat
- known risk areas
- established cleanup rules

## Drop

- temporary experiments
- one-off debugging chatter
- unresolved guesses
- raw outputs unless they encode a stable fact
- sensitive data

## Archive gate

Only allow cleanup when:

- the durable facts are already written to project memory, **or**
- the user explicitly says to skip memory writing and clean directly (e.g. 闲聊 / 不用写 / 直接清理)

Also require:

- the session is no longer the canonical source for active work
- the session is older than the current working thread or clearly superseded
- never archive the currently active thread

## Cleanup constraints

- Do **not** create backup files during cleanup.
- No `*.bak*`, no `*.bak-clean-*`, no copied session trees “just in case”.
- Prefer `codex archive`; fall back to state DB + projectless list updates without backups.
