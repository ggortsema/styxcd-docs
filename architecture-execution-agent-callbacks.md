# StyxCD Execution Agent Callback Strategy

## Current Tactical Plan

Add a temporary status endpoint:

```http
PATCH /executions/{id}/status
```

Initial statuses:

```text
RUNNING
SUCCEEDED
FAILED
```

Jenkins will call this from cleanup/finally to update the execution row.

## Why Temporary

This is intentionally tactical.

Long-term, Jenkins should not directly mutate job state as the primary model.

Instead, Jenkins should report facts/events and the orchestrator should decide what they mean.

## Future Event Model

Future endpoint:

```http
POST /executions/{id}/events
```

Possible event types:

```text
EXECUTION_STARTED
STAGE_STARTED
STAGE_SUCCEEDED
STAGE_FAILED
EXECUTION_SUCCEEDED
EXECUTION_FAILED
EXECUTION_SUMMARY_REPORTED
```

## Future Tables

```text
execution_stage
execution_event
```

Suggested distinction:

```text
execution_stage = current truth/state of each stage in this run
execution_event = audit/timeline history
```

## Callback URL Design Note

Execution agents should not hardcode orchestrator callback locations long-term.

Future Jenkins trigger contract may need:

```json
{
  "executionId": "...",
  "planUrl": "...",
  "callbackUrl": "...",
  "eventUrl": "..."
}
```

At minimum, agents likely need:

```text
orchestratorBaseUrl
callback path
auth/token metadata
```
