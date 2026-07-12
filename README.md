# Basewire

Basewire is a cross-platform, language-neutral, and composable host ability runtime.

It connects stable **abilities** to replaceable **backends** through a small **kernel**:

```text
backends <-> kernel <-> abilities
```

Applications communicate with Basewire through a versioned protocol and do not depend on a particular implementation language. Agent managers, IDE tooling, remote development systems, automation tools, and other applications can build on the same infrastructure.

## Status

Basewire is in the architecture and bootstrap phase. Public contracts are not stable yet.

## Design goals

- Cross-platform support for Windows, Linux, and macOS.
- Language-neutral client protocol.
- Small and reviewable kernel.
- Independently versioned abilities and backend implementations.
- Exact runtime version selection and isolated state schemas.
- Optional components instead of a mandatory full installation.
- Remote deployment through a minimal bootstrap transport, followed by normal Basewire protocol operation.

## Non-goals

Basewire is not an operating system, package manager, service manager, workflow engine, API gateway, or general-purpose remote shell abstraction.

## Repository layout

```text
kernel/      Core routing, lifecycle, cancellation, permissions, and diagnostics
backends/    Platform- or implementation-specific providers
abilities/   Stable services exposed to clients
protocol/    Language-neutral contracts and schemas
sdk/         Generated and handwritten client SDKs
docs/        Architecture decisions and project charter
tests/       Contract, integration, and platform tests
```

See [Project Charter](docs/PROJECT_CHARTER.md) and [Architecture](docs/ARCHITECTURE.md).

## License

Apache License 2.0.
