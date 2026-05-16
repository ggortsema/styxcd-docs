# StyxCD Workflow Planner Contract

## Purpose

Workflow planners convert parsed YML into execution plans.

## Java Interface

```java
package org.mycroftai.styxcd.orchestrator.workflow;

import java.util.Map;

public interface WorkflowPlanner {

    String workflowName();

    Map<String, Object> createJsonStageList(Map<String, Object> yml);
}
```

## Spring Discovery Model

Workflow planners are Spring components.

Future planners may include:

```text
CloudWorkflowPlanner
ECSWorkflowPlanner
EKSWorkflowPlanner
TerraformWorkflowPlanner
ReleaseWorkflowPlanner
```

`ExecutionPlanService` can inject:

```java
List<WorkflowPlanner> workflowPlanners
```

This lets Spring discover all planner implementations automatically.

## Why a List

Injecting `List<WorkflowPlanner>` creates a plugin-style architecture.

The service can select the correct planner based on the workflow name in the YML.

This avoids:

- giant switch statements
- hardcoded registries
- direct Java dependency on Groovy classes
- tight coupling between execution service and workflow implementations
