# Build and Complexity Budget

These figures are architecture alarms rather than immutable targets.

## Kernel targets

- Platform-independent kernel: approximately 8,000–15,000 source lines.
- Per-platform bootstrap substrate: approximately 1,500–4,000 source lines.
- Direct kernel dependencies: preferably 2–4.
- Ordinary incremental builds: seconds.
- Kernel management protocol: small and stable.

## Rules

- GUI, JavaScript engines, HTTP stacks, SSH libraries, databases, and application schemas do not become kernel dependencies.
- Public headers must not expose third-party implementation types.
- Heavy or security-sensitive implementations should be optional components.
- Every new direct kernel dependency requires an architecture decision record.
- CI should record build duration, output size, and build-directory size.
