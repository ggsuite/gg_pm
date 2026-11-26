# maintain-001: The nightly build publishes on its own, on a computer of its own

- Status: accepted; publishing replaced by [maintain-002](maintain-002.md)
- Date: 2026-11-14
- Canonical source: this file
- Open work: set up the computer — `gg do maintain --nightly` is
  implemented by the ticket `lean_publish`

## Decision

A nightly build raises the dependencies of every repo of the ocean, major
versions included, and publishes the result itself. It needs no review:
it changes no code, only versions. It runs on a computer of its own that
the team sets up locally, not on GitHub. When a major version breaks a
repo, the build stops and the developer is brought in; nothing is
published on top of a broken repo. Commit, push and publish of a ticket no
longer upgrade any dependency — `gg do push` no minor and patch versions
either — so the nightly build is the one place where new versions arrive.
