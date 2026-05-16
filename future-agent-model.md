# StyxCD Future Agent Model

## Current State

Current temporary implementation:
- Jenkins URL hardcoded
- orchestrator URL hardcoded
- direct execution plan retrieval

---

## Future Direction

Execution agents should not hardcode orchestrator locations long-term.

Future execution contracts likely need:
- orchestrator base URL
- callback URLs
- event endpoints
- auth/token metadata

---

## Potential Future Contract

Example:

```json
{
  "executionId": "...",
  "planUrl": "...",
  "callbackUrl": "...",
  "eventUrl": "..."
}
```

---

## Future Agent Concepts

Potential future execution agents:
- Jenkins
- ECS workers
- Kubernetes runners
- standalone Java agents
- Python agents

---

## Long-Term Possibilities

- agent registration
- remote execution pools
- multi-region runners
- air-gapped execution
- execution federation
- queue-based dispatch
