## Threat Model (MVP)

We assume the agent planner (AI) is untrusted by default.
The system is designed to limit blast radius even if plans are malicious or incorrect.

### Threats Considered

- Data exfiltration via malicious agent plans
- Unauthorized domain access
- Agent privilege escalation (executing actions outside policy)
- Tampered extension execution
- Log manipulation or deletion

### Mitigations

- DOM access restricted to browser content scripts only  
- Policy validation before and during execution  
- Append-only audit logs  
- No raw DOM or page content sent to the backend or AI  
