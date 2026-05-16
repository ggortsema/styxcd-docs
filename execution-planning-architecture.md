# StyxCD Execution Planning Architecture

## Current Execution Flow

```text
raw yml
  ↓
YmlController
  ↓
ExecutionService
  ↓
ExecutionPlanService
  ↓
ExecutionRepository
  ↓
PostgreSQL
```

## Current API Endpoints

### Parse YML

```http
POST /yml/parse
```

Accepts:
- raw text/plain yml

Returns:
- parsed map structure

### Generate Execution Plan

```http
POST /yml/plan
```

Returns:
- Jenkins-compatible execution plan map

### Create Execution

```http
POST /executions
```

Persists:
- raw yml
- execution plan
- workflow
- status
- timestamp

### Retrieve Execution

```http
GET /executions/{id}
```

### Retrieve Execution Plan

```http
GET /executions/{id}/plan
```

## Planned Future Architecture

```text
ExecutionService
  → YmlParser
  → WorkflowMapperRegistry
  → WorkflowExecutionPlanner
  → Drools Rules Engine
  → ExecutionPlanGenerator
  → EventPublisher
  → ExecutionRepository
```

## Planned Workflow Strategy

```text
CloudWorkflowExecutionPlanner
BuildOnlyWorkflowExecutionPlanner
ProjectTemplateExecutionPlanner
EnvironmentDestroyExecutionPlanner
```

## Planned Plugin Architecture

```text
styxcd-core
  + customer-workflow-module.jar
```

Possible future modules:
- proprietary workflows
- compliance workflows
- deployment workflows
- platform-specific planners

## Planned Dashboard Features

- execution list
- execution detail
- execution plan visualization
- links to Jenkins
- links to Grafana
- validation findings
- event timelines
