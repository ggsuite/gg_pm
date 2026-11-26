<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Implement the lean publish

## Motivation

- The plan
  [lean_publish_process](../tickets/2026-11-14-lean_publish_process-leave-out-publish-steps-that-maintenance-can-do.md)
  takes two things out of a publish: the upgrade of all dependencies and
  the second run of the tests. A nightly build takes the upgrades instead
- It serves the goal
  [publish a ticket in minutes](../goals/publish-a-ticket-in-minutes.md)
- The ticket `lean_publish` implements it. A first attempt was discarded
  and started again after gg itself had become leaner: a ticket now gets
  no repos between by default

## Strategy

- Follow the steps of the plan, one repo after the other
- Answer the open questions where the code answers them, and keep the
  others open
- Record in this repo what was done, what was decided on the way and what
  is still open

## What a publish and a push do now

- A publish resolves (`dart pub get`, `<pm> install`) and analyzes; it
  neither upgrades nor runs the tests again
  ([req-publish-own, get, chk](../requirements/publish.md) — done)
- `gg do push` and `gg one do publish` upgrade only with `--upgrade`, and
  an upgrade crosses major versions only when a repository asks for it
  ([req-maintain-maj](../requirements/maintain.md) — done)
- The hash the quick check on GitHub reads is written by the system commit
  of the publish already; no new API was needed

## The nightly build

- `gg do maintain --nightly` is `--upgrade-deps --major`. A broken repo
  blocks the repos that depend on it, the run exits with an error and
  writes `report.txt` into its run folder
- The README of `gg_multi_maintain` describes how to set up its computer
- [req-maintain-ngt](../requirements/maintain.md) stays `accepted` until
  that computer runs

## Decided on the way

- `Analyze` already runs the lint script of a TypeScript repo
- An upgrade-only release keeps the version rule of `gg do maintain`
- pana grants its points for up-to-date dependencies for 30 days after a
  new major version — a publish without upgrade passes it while the
  nightly build runs
- The decisions [publish-001](../concepts/decisions/publish-001.md) and
  [maintain-001](../concepts/decisions/maintain-001.md) name their open
  work anew, the topics [publish](../concepts/topics/publish.md) and
  [maintain](../concepts/topics/maintain.md) say what changed
- The content of this repo now says `gg_pm` instead of `gg-pm`, as the
  repository on GitHub

## Open Points

- Measure a publish before and after (steps 1 and 9 of the plan)
- A test that compares the manifests of a real publish
- Set up the computer of the nightly build, and decide who looks after it
- Whether a failed night should also send a mail or open an issue
