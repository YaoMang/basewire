# Basewire Architecture

## Overview

Basewire Core consists of three kinds of components:

```text
backends <-> kernel <-> abilities
```

Clients access abilities through a language-neutral protocol. The kernel resolves each session to one exact contract generation and implementation version per ability namespace.

## Backends

Backends implement low-level contracts using operating-system APIs or portable libraries. Examples may include Win32 process creation, POSIX filesystem operations, system credential stores, HTTP libraries, or OpenSSH.

Backends can be omitted when their abilities are not needed. A platform installation is therefore not required to contain every available backend.

## Kernel

The kernel registers components, resolves contracts, routes calls, manages lifetimes, propagates cancellation, normalizes errors, and records diagnostics. It does not directly expose platform-specific backend interfaces to clients.

The kernel's private platform substrate is limited to what is required to bootstrap itself and communicate with components.

## Abilities

Abilities are stable service contracts such as filesystem reads, atomic file replacement, process execution, or credential binding. Ability granularity should represent a bounded operation rather than mirror individual system calls.

## Version isolation

Versioning is separated into independent axes:

- bootstrap protocol generation;
- kernel protocol generation;
- ability contract generation and implementation version;
- backend contract generation and implementation version;
- persistent state schema generation.

A session binds one version of each ability namespace. Different sessions may bind different generations, but similar versions are not mixed into one unqualified namespace.

Breaking changes create a new contract generation instead of adding `V2`, `Legacy`, or `Ex` methods to the old contract.

## Remote operation

On a new remote connection, a minimal transport may identify the target platform and deploy an exact Basewire runtime version. After startup, normal operations use the Basewire protocol rather than platform-specific shell commands.

WSL is treated as a Linux environment when Basewire runs inside it. Host-driven WSL or virtual-machine management is outside the Core; remote environments can be reached through a transport such as SSH.

## Dependency direction

- Abilities depend on kernel contracts.
- The kernel depends on backend contracts, not specific optional implementations.
- Backends depend on operating-system APIs or implementation libraries.
- Clients depend on ability contracts, not backend details.
