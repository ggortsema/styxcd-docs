# StyxCD Execution Lifecycle

## Current Flow

### 1. YAML Submission

```text
POST /yml/plan
```

### 2. Execution Creation

```text
POST /executions
```

Persists:
- execution metadata
- raw YAML
- execution plan

### 3. Jenkins Trigger

Temporary implementation:
- hardcoded Jenkins trigger
- executionId passed to Jenkins

Future:
- configurable execution agents

### 4. Execution Plan Retrieval

Jenkins retrieves:

```text
GET /executions/{id}/plan
```

Execution plan is parsed into the existing Jenkins engine map structure.

### 5. Workflow Execution

Existing Jenkins engine executes unchanged.

### 6. Final Status Update

Temporary endpoint:

```text
PATCH /executions/{id}/status
```

Initial statuses:
- RUNNING
- SUCCEEDED
- FAILED

### 7. Future Real-Time Reporting

Future architecture:
- execution_stage table
- execution_event table
- stage-level callbacks
- live orchestration state updates
- event timelines
