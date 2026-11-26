<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Set up gg-pm and plan a lean publish

## Motivation

- gg had no place for its plans: goals, requirements and decisions lived in
  chats and in the heads of the people. This repo is that place now
- The first plan in it answers a question from daily work: why does
  publishing a ticket with many repos take so long, and which of its steps
  can go?
- The goal behind it:
  [publish a ticket in minutes](../goals/publish-a-ticket-in-minutes.md)

## Strategy

- Set the repo up after the rules of `dna-plan`: everything planned lives
  in the quarter folder, German copies below `doc/de`
- Read what a publish does today, step by step, before proposing anything
- Engineer the requirements with the product owner, one by one, and write
  down only what was confirmed
- Record the decisions made on the way, with their reason
- Plan only: the code changes after another ticket that touches the same
  function is merged

## The repo

- DNA layers `@ggdna/dna-plan` and `@tssuite/dna-ggsuite`: the guides, the
  skills and the quick check
- No code: the TypeScript skeleton is gone, `package.json` only holds the
  DNA layers
- `doc/2026-Q4` with goals, requirements, concepts, architecture, tickets,
  bugs, team, reports, exports, blog and the note on the prompts
- Requirements are named by three-letter codes, e.g. `req-publish-own`,
  through `dna/doc/guides/pm-repo-guide.overrides.md`
- Public, under the MIT licence, with a protected `main`: branch rules need
  a public repo on the plan of the organization
- README in English and German after the README template

## What a publish does today

- For every repo of a ticket it upgrades all dependencies, major versions
  included, refreshes them twice, and runs analyze, format and tests again
- The tests ran at the commit already, on the same code
- Nothing upgrades dependencies on a schedule: a publish is the place where
  new versions happen to arrive

## The plan

- Five accepted requirements in the areas
  [publish](../requirements/publish.md) and
  [maintain](../requirements/maintain.md)
- A publish changes only the versions of the dependencies the ticket
  published, resolves with get or install, and analyzes instead of
  testing — [publish-001](../concepts/decisions/publish-001.md)
- It still writes the hash of the checks, so the quick check on GitHub
  passes
- `gg do push` upgrades nothing any more
- A nightly build on a computer of its own raises all dependencies,
  publishes without a review and stops when a major version breaks a
  repo — [maintain-001](../concepts/decisions/maintain-001.md)
- The steps and the affected repos are in the
  [ticket plan](../tickets/2026-11-14-lean_publish_process-leave-out-publish-steps-that-maintenance-can-do.md)

## Open Points

- Nothing is implemented; the code follows after the ticket `speed_up_gg`
- The goal is proposed, not confirmed; its measures are proposals
- The team and its roles are not written down yet
- Open in the plan: the credentials of the nightly computer, how a
  developer is told about a broken repo, what replaces `dart analyze` in a
  TypeScript repo, and the version of an upgrade-only release
- No repo names `gg-pm` as its project management repo yet; once one does,
  the prompts of the team land on the public branch `prompts`
