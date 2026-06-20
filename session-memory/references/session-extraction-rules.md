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

- the durable facts are already written to project memory
- the session is no longer the canonical source for active work
- the session is older than the current working thread or clearly superseded
