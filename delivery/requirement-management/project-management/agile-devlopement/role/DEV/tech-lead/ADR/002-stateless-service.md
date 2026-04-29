# ADR-002: Stateless Service Design

## Status
Accepted

## Context
System needs to scale horizontally.

## Decision
Use stateless services.

## Alternatives
- Stateful services

## Reason
- Easy scaling
- Better cloud compatibility

## Trade-offs
- Requires external state storage (Redis)

## Date
2026-04-21
