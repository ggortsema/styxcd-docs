# StyxCD Planner Migration Architecture

## Purpose

This document captures the transition from Jenkins-owned workflow planning to orchestrator-owned workflow planning.

## Previous Model

Jenkins owned:

- workflow planning
- stage parameter generation
- stage execution

The Jenkins shared library parsed the YML, decided which stages were needed, called each stage's `getParams(...)`, built the execution map, and executed the stages.

## New Model

The orchestrator owns planning.

Jenkins becomes an execution agent.

```text
YML
  -> Orchestrator Workflow Planner
  -> Stage Param Planners
  -> Persisted Execution Plan
  -> Jenkins pulls plan by executionId
  -> Jenkins executes stages
```

## Key Boundary

```text
Stage planning belongs in the orchestrator.
Stage execution belongs in the execution agent.
```

## Current Validated Milestone

The orchestrator successfully generated an execution plan using:

- Spring service layer
- Groovy `CloudWorkflowPlanner`
- Java stage planner classes
- persisted JSONB execution plan

Jenkins successfully consumed a remotely retrieved execution plan and ran the existing execution engine unchanged.

## Migration Strategy

1. Keep Jenkins execution logic intact.
2. Move workflow planning into orchestrator.
3. Move stage `getParams(...)` logic into orchestrator.
4. Persist execution plans in PostgreSQL.
5. Let Jenkins retrieve by `executionId`.
6. Remove planning logic from Jenkins only after equivalent orchestrator planners exist.
