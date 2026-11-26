<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Merge maintenance into main without publishing

## Motivation

- Maintenance keeps the main branches current; a release is a decision of
  the developer
- Until now `gg do maintain` and its nightly build released every changed
  repo on its own, without a review
- New rule: everything that is published anywhere — a registry, a version
  tag — goes through a normal ticket and its review

## Strategy

- Decision [maintain-002](../concepts/decisions/maintain-002.md), accepted
  on 2026-11-15, replaces the publishing part of maintain-001
- The nightly build stays: a computer of its own, no review, a stop when a
  major version breaks a repo
- It now merges into main and releases nothing

## Implementation

- `req-maintain-ngt` and `req-maintain-dna` now ask for merged, unreleased
  changes on main
- Ticket file `maintain_merge_only`, English and German
- `gg do maintain` merges with `gg one do publish --merge-only`

## Open Points

- An upgrade on main reaches the registry only with the next ticket that
  publishes the repo
- pana's up-to-date points expire 30 days after a new major version of a
  dependency for repos that no ticket publishes
