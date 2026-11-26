# maintain-002: Maintenance merges to main, it does not publish

- Status: accepted
- Date: 2026-11-15
- Canonical source: this file
- Replaces: the publishing part of [maintain-001](maintain-001.md)
- Open work: —

## Decision

`gg do maintain`, the nightly build included, merges every changed repo
into its main branch and stops there: no version increase, no release
heading in `CHANGELOG.md`, no upload to a registry, no version tag. It uses
`gg one do publish --merge-only`. The changes wait below `## Unreleased`
and the next publish of the repo by a ticket releases them.

Everything that is released anywhere — a registry, a version tag — goes
through a normal ticket and its review. No automation releases on its own.

Why: a release is a decision of the developer; maintenance only keeps main
current. The rest of maintain-001 holds: a computer of its own, no review,
stop when a major version breaks a repo.

Consequence: a repo that no ticket publishes keeps its released
constraints; pana's up-to-date points expire 30 days after a new major
version of a dependency.
