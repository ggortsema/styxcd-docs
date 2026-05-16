# StyxCD Observability Strategy

## Goals

Provide unified observability across:
- orchestrator
- Jenkins execution agents
- infrastructure
- future event routing

---

## Correlation IDs

Primary correlation key:

```text
executionId
```

All logs/events should include executionId.

---

## Logging Architecture

### Jenkins

Current:
- final cleanup/finally reporting

Future:
- stage-level reporting
- structured JSON events

### Orchestrator

Current:
- execution persistence
- status tracking

Future:
- centralized orchestration event processing

---

## Loki / Alloy / Grafana

### Alloy
Collector/transform layer.

### Loki
Log/event storage.

### Grafana
Visualization and querying.

---

## Future Direction

Potential future split:

### Real-Time Events
- stage started
- stage completed
- stage failed

### Final Execution Summary
- durations
- statuses
- errors
- execution metadata
- links/build information

---

## Future Architecture Decisions

Still under evaluation:
- should Jenkins send directly to Loki?
- should orchestrator centralize observability?
- hybrid approach?
