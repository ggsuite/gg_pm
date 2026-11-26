# Maintenance

How the dependencies of the repos of an ocean are kept current, and what
is known about it. The evidence behind the requirements of the area
[maintain](../../requirements/maintain.md).

## What exists today

- `gg do maintain` (`gg_multi_maintain`, read on 2026-11-14): per repo a
  fresh clone, a branch `maintain_<id>`, the tasks `--upgrade-sdk`,
  `--upgrade-deps [--major]`, `--upgrade-dna`, then `gg one do commit`
  and `gg one do publish`, in dependency order
- Major versions are crossed only with `--major`
- Nothing runs on a schedule: the only workflow of the repos is
  `quick_check.yaml` on push and pull request. A nightly build does not
  exist
- New versions arrive when a ticket is pushed or published: both upgrade
  all dependencies of every repo of the ticket, major versions included

## What holds

- A repo that is in no ticket gets no upgrade at all; a repo that is in a
  ticket gets upgrades nobody asked for, mixed into the change of the
  ticket
- An upgrade changes no code, only versions; that is why a nightly build
  may publish it without a review, see
  [maintain-001](../decisions/maintain-001.md)

## Since the ticket `lean_publish`

- `gg do maintain --nightly` is `--upgrade-deps --major`: the run a
  computer of its own starts every night
- A run with a failed or blocked repo exits with an error and writes
  `<workspace>/.maintain/<run id>/report.txt`
- Push and publish of a ticket upgrade nothing; new versions arrive
  through the nightly build only
