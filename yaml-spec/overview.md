# YAML Specification

The StyxCD YAML specification defines the contract between a workflow author and the StyxCD orchestrator.

The specification describes:

- Workflow structure
- Release metadata
- Applications
- Environments
- Platform configuration

## Philosophy

The YAML specification is intentionally human-readable.

A workflow should describe the desired outcome, while StyxCD determines the execution plan.

## Example

```yaml
workflow: cloud_workflow

release:
  name: hello-world
  version: 0.1.0
```