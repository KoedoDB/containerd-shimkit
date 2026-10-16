# Security policy

## Reporting a vulnerability

Please report security problems **privately**, not as a public issue:

- by email to **security@koedodb.com**, or
- with GitHub's private reporting: **Security → Report a vulnerability** on this repository.

Include what you found, how to reproduce it (a proof of concept helps), and the version or commit you tested. We will acknowledge
your report, look into it, and tell you what we decided. This is a small project with a single maintainer, so please allow a few
days for a first answer; we cannot promise a fixed response time or offer a bounty.

## What this repository is

`containerd-shimkit` here is a cut-down and extended copy of the crate of the same name in
[containerd/runwasi](https://github.com/containerd/runwasi), made for [containerd-cloudhypervisor](https://github.com/KoedoDB/containerd-cloudhypervisor)
(a shim that runs containers in virtual machines). See [KOEDODB.md](KOEDODB.md) for what it is made of and how it differs from upstream.
It is code that runs as root on a node and handles requests from containerd, so a flaw in it matters; we want to hear about it.

- **In scope**: the code in this repository (the task service, the exec and terminal handling, the state machines).
- **Not in scope**: flaws that are in `containerd-shim`, `ttrpc`, `protobuf` and other dependencies (report them to those projects; tell us
  too if we should update), and flaws in upstream runwasi code that we kept unchanged (report them to
  [containerd/runwasi](https://github.com/containerd/runwasi/security); we will take the fix over).

## Supported versions

Only the latest tag (`v0.1.2-koedodb.N`) is supported. There are no long-lived maintenance branches.

## How we handle dependencies

`cargo audit` (RustSec) is run on this crate's dependency tree when we update it, and the advisories of runwasi are checked by hand
(this code is no longer the upstream crate, so a tool that watches the upstream version does not see its flaws).
