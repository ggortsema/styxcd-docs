# StyxCD Event Routing Module

## Purpose

The Event Routing Module is a future core subsystem responsible for:
- ingesting external events
- normalizing payloads
- routing requests based on configuration/rules
- triggering orchestration workflows

This was previously envisioned as a standalone microservice but may become a module inside the control plane.

---

## Supported Input Sources

Potential future inputs:
- GitHub webhooks
- GitLab webhooks
- Bitbucket webhooks
- Jira events
- Slack commands
- REST API calls
- scheduled triggers
- RabbitMQ messages
- Kafka messages
- manual UI actions

---

## Core Concepts

### Configuration-Driven Routing

Example:

```text
repo X + branch Y -> workflow A
event type Z -> workflow B
```

### Payload Normalization

External payloads transformed into internal orchestration contracts.

### Workflow Triggering

Module determines:
- workflow
- environment
- approvals
- orchestration behavior

---

## Future Enhancements

- Drools integration
- retry/dead-letter queues
- signature verification
- async processing
- audit trails
- multi-tenant routing
