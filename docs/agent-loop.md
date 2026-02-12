## Agent Execution Model (MVP)

The agent operates on a strictly structured execution model.
Free-form execution is forbidden.

### Agent Loop

1. Task received
2. Plan generated (structured)
3. Plan validated against policy
4. Steps executed sequentially
5. Output validated
6. Execution logged

### Allowed Step Types (MVP)

- READ_TABLE
- EXTRACT_FIELD

Each step must be:
- Deterministic
- Policy-checkable
- Loggable
