# StyxCD YML Specification (Initial Draft)

## Overview

StyxCD uses declarative yml specifications to describe:
- applications
- environments
- deployment intent
- testing intent
- workflow execution behavior

The orchestrator interprets the submitted yml and generates execution plans for execution runtimes such as Jenkins.

---

# Current Direction

The specification intentionally supports:

- flexible schemas
- workflow-specific validation
- rule-driven orchestration
- future plugin workflows

The platform currently parses yml into flexible nested map structures instead of rigid DTO graphs.

---

# Root Structure

```yml
workflow: cloud_workflow

release:
  name: johnny-platform-release
```

---

# Workflow

Defines which orchestration workflow should interpret the document.

Example:

```yml
workflow: cloud_workflow
```

Future examples:

```yml
workflow: project_template_workflow
workflow: environment_destroy_workflow
workflow: build_only_workflow
```

---

# Release

Top-level release metadata.

Example:

```yml
release:
  name: johnny-platform-release
  version: 1.0.0
```

## Fields

| Field | Description | Required |
|---|---|---|
| name | Release name | workflow-specific |
| version | Release version | optional |

---

# Desired State

Represents declarative infrastructure/application intent.

Example:

```yml
desired_state:
  environment: present
  applications: deployed
```

Example future values:

```yml
environment: absent
applications: none
```

```yml
environment: ephemeral
applications: deployed
```

```yml
environment: present
applications: built
```

---

# Applications

Applications are grouped by technology/runtime type.

Example:

```yml
applications:
  spring:
    - name: first-app
```

## Supported Groups (initial)

- spring
- node
- python

---

# Spring Application Example

```yml
applications:
  spring:
    - name: first-app
      repo: someplace
      branch: main
      version: 1.0.0

      build:
        type: maven-docker
        project_path: .
        dockerfile: Dockerfile
        artifact_target: ecr

      runtime:
        container_port: 8080
        health_check_path: /actuator/health
```

---

# Node Application Example

```yml
applications:
  node:
    - name: first-node-app
      repo: someplace
      branch: main

      build:
        type: docker
```

---

# Python Application Example

```yml
applications:
  python:
    - name: fastapi-app

      build:
        type: python-docker
        framework: fastapi
```

---

# Build Section

Describes how the application should be built.

## Example

```yml
build:
  type: maven-docker
```

## Planned Fields

| Field | Example |
|---|---|
| type | maven-docker |
| project_path | . |
| dockerfile | Dockerfile |
| artifact_target | ecr |
| framework | fastapi |

---

# Runtime Section

Runtime deployment metadata.

## Example

```yml
runtime:
  container_port: 8080
  health_check_path: /actuator/health
```

---

# Test Suites

Global reusable test suites.

## Example

```yml
test_suites:
  integration:
    repo: someplace
```

## Planned Types

- integration
- performance
- penetration

---

# Environments

Deployment target definitions.

## Example

```yml
environments:
  dev:
    - name: dev-a
      platform: eks
```

---

# ECS Example

```yml
ecs:
  launch_type: fargate
  cluster: dev-b-cluster
  desired_count: 1
  assign_public_ip: true
```

---

# AKS Example

```yml
aks:
  resource_group: stage-platform-rg
  cluster_name: stage-a-aks
```

---

# Validation Philosophy

Validation is intentionally workflow-specific.

The platform does NOT currently enforce globally rigid DTO schemas.

Instead:

```text
raw yml
  → parsed map
  → workflow mapper
  → Drools facts
  → workflow validation/rules
  → execution plan
```

This allows:
- multiple workflow types
- plugin workflows
- flexible evolution
- customer-specific extensions

---

# Execution Plan Generation

The orchestrator converts yml intent into execution plans.

Current execution plans are persisted as ordered maps:

```json
{
  "CloudWorkflowInitialize": {...},
  "GradleBuild@app": {...},
  "CloudWorkflowCleanup@final": {...}
}
```

---

# Current Working Minimal Example

```yml
workflow: cloud_workflow

release:
  name: johnny-platform-release

  applications:
    spring:
      - name: first-app
        repo: someplace
        branch: main

        build:
          type: maven-docker
```

---

# Future Planned Areas

- Drools validation rules
- workflow plugin modules
- RabbitMQ events
- dashboard execution views
- observability integration
- environment lifecycle orchestration
- reusable project templates
- Ansible/bootstrap workflows
