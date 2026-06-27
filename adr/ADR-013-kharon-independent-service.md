# ADR-013: Separate Kharon into an Independent AI Service

## Status
Accepted

## Context

Originally AI capabilities were envisioned as features embedded within the StyxCD
orchestrator. As the architecture evolved it became clear that deterministic
deployment orchestration and probabilistic AI reasoning have different
responsibilities, release cadences, language ecosystems, and scaling concerns.

## Decision

Kharon will be implemented as an independent service.

Responsibilities of Kharon include:

- Chat interface
- Retrieval-Augmented Generation (RAG)
- Knowledge ingestion
- Embeddings
- Semantic retrieval
- YAML generation
- Future operational reasoning

Responsibilities of StyxCD remain:

- Validation
- Planning
- Workflow execution
- Policy enforcement
- Audit
- Deployment orchestration

Communication occurs through a service contract.

## Consequences

Positive:

- Independent deployment cadence
- AI stack can evolve independently
- Python ecosystem can be adopted without affecting StyxCD
- Future implementations in other languages remain possible

Negative:

- Additional service to operate
- Service contract must be maintained

## Principle

StyxCD authorizes.

Kharon advises.
