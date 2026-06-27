# ADR-014: Adopt Python as the Reference Implementation for Kharon

## Status
Accepted

## Context

Kharon's initial goal is to learn and adopt modern AI engineering practices,
including LangChain, LangGraph, RAG, and agent workflows.

Although Java and .NET are viable ecosystems, the Python ecosystem is the
reference implementation for many AI libraries and examples.

## Decision

The first implementation of Kharon will use:

- Python
- FastAPI
- LangChain
- LangGraph
- PostgreSQL + pgvector

This decision applies only to Kharon.

StyxCD remains Java-based.

## Consequences

Positive:

- Learn the dominant AI ecosystem
- Faster access to examples and documentation
- Easier experimentation
- Architecture can later be ported to Java or .NET

Negative:

- Polyglot solution
- Cross-language service boundary

## Notes

The architecture is considered portable.

Language is an implementation choice.

The service contract is the durable asset.
