# Basewire Project Charter

## Definition

Basewire is a cross-platform, language-neutral, composable host ability runtime. It exposes stable, versioned ability contracts and maps them to one or more replaceable backend implementations through a small kernel.

## Core composition

```text
backends <-> kernel <-> abilities
```

The Core is independent of its consumers. TypeScript, Go, Rust, C++, Python, command-line tools, IDEs, and other applications may use the same protocol.

## Kernel responsibilities

The kernel is the capability mediator and execution nucleus. It owns only mechanisms shared by all components:

- protocol handshake and session management;
- ability and backend registration;
- contract resolution and binding;
- request routing and structured errors;
- deadlines, cancellation, streams, and backpressure;
- component lifecycle and health;
- permission mediation, auditing, and diagnostics.

The kernel must not contain application-domain knowledge.

## Ability responsibilities

Abilities define what a client can request. An ability may use one backend, combine several backends, or select among multiple compatible backend implementations.

Ability contracts must be stable, bounded, cancellable where practical, and independently versioned.

## Backend responsibilities

Backends provide implementation mechanisms. A backend may wrap operating-system APIs or a portable library. Backend identities are diagnostic and internal; normal clients depend only on abilities.

## Boundary

Basewire uses the host operating system's resource, identity, permission, process, file, credential, and network models. It does not create a competing system model.

## Initial capability scope

The initial design work focuses on:

- system information;
- filesystem operations with reliable replacement and rollback semantics;
- process discovery and execution;
- secure credential references and injection;
- optional networking, archive, and remote-runtime components.

## Non-goals

Basewire does not aim to become:

- an operating system or virtual operating environment;
- a service or package manager;
- a desktop UI framework;
- a container or virtual-machine manager;
- a general workflow scheduler;
- an API gateway or protocol conversion platform;
- an application-specific agent manager.

## Change discipline

New kernel mechanisms, public abilities, direct dependencies, and persistent state schemas require an architecture decision record. Application-specific exceptions are not accepted into the Core.
