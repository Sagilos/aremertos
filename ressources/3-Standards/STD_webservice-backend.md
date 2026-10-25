---
id: STD_webservice-backend
category: external_requirements
title: Backend for webservice
obligation: MUST
requirement_references: []
internal_references: []
normative_vs_informative: normative
---

# Technology used
- Language : Rust
- Framework : 
  - async: tokio
  - http : axum
    - Serialisation : serde
  - gRPC : tonic
    - Serialisation : prost, tonic-prost
  - middleware : tower-http

# Supported protocols
- API REST : 
- API gRPC & gRPC Stream : 

# AuthN & AuthZ
- AuthN : HTTP Bearer
- AuthZ : 
  - Check `aud` with a configured value
  - Check `scope` with a configured RBAC

# Autorisation
- HTTP 

# Interface contract
- REST : Swagger
- gRPC : Protobuf

## Rust backend stack
- HTTP foundation: Axum.
- Async runtime: Tokio.
- REST: Axum handlers; JSON contracts; OpenAPI specification.
- gRPC: Tonic; Protobuf contracts; unary, client/server and bidirectional streaming.
- GraphQL: async-graphql with async-graphql-axum; subscriptions where required.
- Middleware: Tower / tower-http; protocol-appropriate configuration.
- Architecture: thin transport adapters over shared application/domain services.
- Deployment: one service by default; shared or separate protocol listeners according to ingress, security and operational requirements.

## Production design considerations
- Authorization shared at application level; transport-specific authentication.
- Explicit mapping of domain errors to HTTP, gRPC and GraphQL responses.
- Bounded requests/messages, concurrency, queues and stream buffers.
- Streaming cancellation, backpressure, idle limits and graceful shutdown.
- GraphQL depth/complexity limits and batching for N+1 prevention.
- Protocol-level integration tests through the actual production ingress.
- Compatible dependency versions pinned and tested together.
