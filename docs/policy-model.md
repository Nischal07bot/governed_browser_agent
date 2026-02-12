## Policy Model (MVP)

Policies are declarative and enforced at runtime.
They define what the agent is allowed to do.

### Policy Fields

- allowed_domains  
  List of domains the agent is allowed to operate on.

- allowed_actions  
  List of allowed step actions (e.g., READ_TABLE, EXTRACT_FIELD).

- allowed_fields  
  Whitelisted data fields the agent is allowed to extract.

- max_steps  
  Maximum number of steps allowed in a plan.

### Enforcement Points

Policy is enforced at:

1. Plan validation  
2. Step execution  
3. Data extraction  

Policy evaluation must be:
- Deterministic  
- Side-effect free  
