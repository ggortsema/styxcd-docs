# StyxCD Stage Parameter Planners

## Purpose

Stage parameter planners are orchestrator-side classes responsible for producing the parameter maps required by execution agents.

They replace the old Jenkins `getParams(...)` methods.

## Current Package

```text
org.mycroftai.styxcd.orchestrator.workflow.cloud.stage
```

## Current Stage Planners

```text
CloudWorkflowInitializeStagePlanner
CloudWorkflowGradleBuildStagePlanner
CloudWorkflowCleanupStagePlanner
```

## Naming Decision

Stage planners are workflow-scoped rather than globally named.

This avoids premature reuse and naming collisions between workflows.

Example:

```text
CloudWorkflowInitializeStagePlanner
TerraformWorkflowInitializeStagePlanner
ReleaseWorkflowInitializeStagePlanner
```

## Future Reuse

If a stage planner becomes truly reusable, it can later be promoted into a shared package.

Possible future packages:

```text
workflow.shared.stage
stage.common
```

## Current Rule

```text
DB should store actual executed stages later.
DB should not store the stage catalog yet.
```
