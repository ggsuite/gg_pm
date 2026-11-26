# lean_publish_process: Leave out publish steps that maintenance can do

## Goal

Publishing a ticket does only what has to happen at that moment: write
the versions of the dependencies the ticket has just published into
`pubspec.yaml` or `package.json`, resolve with `dart pub get` or
`<package manager> install`, analyze, merge, upload and tag. Two things
leave the publish: upgrading all the other dependencies — major versions
above all — and running the tests once more. A nightly build over the
ocean takes the upgrades instead, so packages and apps stay on current
versions without every ticket paying for it.

It is for developers who publish tickets with many repos, and it serves
the goal [publish a ticket in minutes](../goals/publish-a-ticket-in-minutes.md).
Implemented by the ticket `lean_publish` (started 2026-11-15), after
`speed_up_gg` was merged.

## Requirements

- [req-publish-own, get, chk](../requirements/publish.md): a publish
  changes only the dependencies of the ticket, resolves instead of
  upgrading, and does not repeat the tests
- [req-maintain-maj, ngt](../requirements/maintain.md): major versions
  are raised by maintenance only, and a nightly build keeps the ocean
  current

What a publish and the maintenance do today is in the topics
[publish](../concepts/topics/publish.md) and
[maintain](../concepts/topics/maintain.md). The decisions the plan rests
on: [publish-001](../concepts/decisions/publish-001.md) and
[maintain-001](../concepts/decisions/maintain-001.md).

## Affected repos

- `gg_multi_do_publish`: `_publishRepo` no longer upgrades and no longer
  runs `can commit`; it resolves with get or install and runs `Analyze`
  of gg_one_core. Its system commit records the hash that `did commit`
  and the quick check read
- `gg_one_do_publish`: `gg one do publish` upgrades only with
  `--upgrade`
- `gg_one_core`: the default of `do.upgrade.deps.majorVersions` becomes
  false. A `.gg/gg_rc` written by an older gg spells out true and keeps
  it — it only matters for an upgrade somebody asks for
- `gg_one_commit`: documentation and tests of the new default
- `gg_multi_commit`: `gg do push` upgrades only with `--upgrade`
- `gg_multi_maintain`: `gg do maintain --nightly` (`--upgrade-deps
  --major`); a run with problems writes `report.txt` into its run folder;
  the README explains how to set up the computer of the nightly build
- `dna_gg`: the development guide and the skills `/gg-push` and
  `/gg-publish` say what push and publish do and what the nightly build
  does

## Steps

1. Measure one publish of a real ticket per step with the process trace
   — open: no ticket was published with the new flow yet
2. Publish without upgrade — done
3. Prove that a publish changes only the dependencies of the ticket —
   unit tests show that a publish runs `dart pub get`, no upgrade, and
   writes only the constraints of the repos it published. A test that
   compares the manifests of a real publish is still open
4. Replace `can commit` in the publish by get and analyze — done. No new
   API was needed: the system commit of the publish already records the
   hash the quick check reads
5. Take upgrades out of commit, push and publish — done
6. Build the nightly build on `gg do maintain` — done: `--nightly`. A
   broken repo blocks the repos that depend on it, the run exits with an
   error and writes `report.txt`
7. Set up the computer of the nightly build — the guide is in the README
   of `gg_multi_maintain`; the computer itself is still to be set up
8. Write the guides — done
9. Measure again and compare with step 1 — open

Decided while implementing:

- TypeScript: `Analyze` of gg_one_core already runs the lint script of
  `package.json` in a TypeScript repo
- An upgrade-only release keeps the rule of `gg do maintain`: minor when
  a dependency leaves its old constraint, otherwise patch
- The developer learns of a broken repo from the exit code and the
  `report.txt` of the run
- pana grants the points for up-to-date dependencies for 30 days after a
  new major version of a dependency is released. A publish without
  upgrade therefore passes pana as long as the nightly build runs

## Open questions

- Who looks after the computer of the nightly build, and which account
  holds its credentials for GitHub, pub.dev and npm?
- Should a failed night also send a mail or open an issue?
