# ADR-015: Service Boundary Between StyxCD and Kharon

## Status
Accepted

## Context

The UI requires AI responses that may involve retrieval, model invocation,
reasoning, and future long-running workflows.

The orchestration platform should remain responsive and should not depend on AI
execution time.

## Decision

StyxCD communicates with Kharon through a narrow service interface.

Initial capability:

- Chat request
- Chat response

Future capabilities may include:

- YAML generation
- Execution explanation
- Knowledge search

Long-running processing should evolve toward asynchronous request/processing/
callback semantics.

## Consequences

- Clean separation of concerns
- Independent scaling
- Easier future migration of either implementation
