# StyxCD Control Plane Architecture

## Purpose

The StyxCD control plane is responsible for:
- orchestration planning
- workflow validation
- execution persistence
- orchestration state management
- execution coordination

Execution runtime responsibilities are delegated to execution agents such as Jenkins.

---

## Core Components

### Orchestrator
Responsibilities:
- accept YAML
- validate workflows
- generate execution plans
- persist execution metadata
- coordinate orchestration lifecycle
- future event routing and approvals

### Jenkins Execution Agent
Responsibilities:
- retrieve execution plan by executionId
- execute stages/workflows
- report execution results
- future stage-level event reporting

### PostgreSQL
Stores:
- executions
- execution plans
- future stage/event records

### Observability Stack
- Grafana
- Loki
- Alloy

Future:
- RabbitMQ event streaming

---

## Execution Lifecycle

1. YAML submitted to orchestrator
2. Orchestrator validates YAML
3. Execution plan generated
4. Execution persisted
5. Jenkins triggered with executionId
6. Jenkins retrieves execution plan
7. Jenkins executes workflow
8. Jenkins reports final status
9. Future: stage-level event reporting

---

## Architectural Direction

Execution planning is now orchestrator-owned.

Jenkins is now an execution agent.

Execution plans are:
- persistent
- remotely retrievable
- replayable
- portable JSON contracts

This decouples planning from execution runtime.
