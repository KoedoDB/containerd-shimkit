# containerd-shimkit (KoedoDB's cut-down version)

A small Rust library for building a [containerd](https://containerd.io) shim whose containers run **somewhere else**: in a VM, say, where a
guest agent starts them. You implement an `Instance` (create, start, kill, wait, delete, and optionally exec, terminal resize, close
stdin) and the library is the task service containerd talks to: the task API over ttrpc, the state machine of each task and exec,
the events containerd expects, `Wait` before `Start`, exit handling.

It is a start from `containerd-shimkit` of [containerd/runwasi](https://github.com/containerd/runwasi) (v0.1.2, Apache-2.0), with
exec and terminal support added and everything a VM shim does not need taken out (the WebAssembly-oriented parts, libcontainer,
OpenTelemetry, Windows, the zygote helper). **It is no longer the upstream crate**: see [KOEDODB.md](KOEDODB.md) for what it is made of,
what was removed and why, and how it differs. It is built for [containerd-cloudhypervisor](https://github.com/KoedoDB/containerd-cloudhypervisor)
and maintained for that, not as a general-purpose library; use at your own risk.

```
cargo test        # needs protoc
```

Not affiliated with the containerd or runwasi projects. Licensed under the Apache License 2.0 (`LICENSE`); the original copyright
notices of the runwasi authors stay in the history, which is kept.
