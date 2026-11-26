<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Check the DNA without writing it

## Motivation

- The DNA test of every repo (`test/dna/dna_test.dart`) did hidden work:
  it wrote DNA updates and committed them as `#gg: generated DNA` in the
  middle of a ticket, during `gg can commit`
- The DNA test had been deleted in a repo to stop the automatic update;
  but the check that generated files stay unchanged was wanted
- The plan
  [dna_check_only](../tickets/2026-11-15-dna_check_only-check-the-dna-and-update-it-at-night.md)
  asks for a check that only checks
  ([req-dna-chk](../requirements/dna.md)); it serves the goal
  [publish a ticket in minutes](../goals/publish-a-ticket-in-minutes.md)

## Strategy

- Put the check into helix, where the DNA test came from, and let helix
  place it — no script of its own to keep in sync
- One engine for both languages: helix-js runs the same check compiled to
  WebAssembly
- New DNA arrives through `gg dna upgrade`, not through the tests

## What changed

- helix `checkDna()`: fails on a generated file changed by hand and names
  the DNA file the edit belongs in; reports outstanding DNA updates with
  `gg dna build`; writes, backs up and commits nothing
- The placed check calls `checkDna()`. A Dart repo gets
  `test/dna/dna_test.dart`, a TypeScript repo `test/dna/dna.spec.ts`
- `gg dna init` always replaces the check; the new `gg dna upgrade` places
  it and builds the DNA
- helix-js `checkDna()` for vitest
- `gg do maintain --upgrade-dna` runs `gg dna upgrade` after raising the
  layers

## Decisions

- The check keeps the path `test/dna/dna_test.dart`, so an upgrade
  replaces the old test in place
- Outstanding DNA updates do not fail the check — otherwise every new
  layer version would turn the tests red until somebody builds
- A repo with `pubspec.yaml` and `package.json` counts as a Dart repo
- `gg dna upgrade` raises no packages; `gg do maintain --upgrade-dna` does

## Follow-up tickets

1. `dna_ggsuite`: the layers chosen on 2026-11-15 — dna_readme,
   dna_guides, dna_translate, dna_index, dna_blog, dna_vscode,
   dna_clean_code, dna_scripts, dna_github, dna_dart; dna_gg and
   dna_install leave. Published before 2.
2. Maintenance: `gg do maintain --upgrade-dna` over all ggsuite repos, so
   each one gets the check; remove the TypeScript layers from
   `dna/_generated.json` of the Dart repos

## Open Points

- Steps 4-7 of the plan: the nightly DNA upgrade of every organization,
  the rule for skills in `dna_gg`, one ecosystem per repo
