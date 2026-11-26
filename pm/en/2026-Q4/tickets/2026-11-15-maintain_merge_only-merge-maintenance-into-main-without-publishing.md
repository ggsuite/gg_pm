# maintain_merge_only: Maintenance merges to main, releases go through tickets

## Goal

Planned and implemented on 2026-11-15 in the ticket `maintain_merge_only`.

`gg do maintain`, the nightly build included, merges each changed repo
into main and releases nothing. Everything that is published anywhere goes
through a normal ticket and its review. See
[maintain-002](../concepts/decisions/maintain-002.md).

It serves the goal
[publish a ticket in minutes](../goals/publish-a-ticket-in-minutes.md).

## Requirements

- [req-maintain-ngt](../requirements/maintain.md): the nightly build merges
  its raises into main, without publishing
- [req-maintain-dna](../requirements/maintain.md): the same for the DNA

## Affected repos

- `gg_pm`: decision maintain-002, the two requirements
- `gg_multi_maintain`: merge each repo with `gg one do publish
--merge-only`; outcome `merged`; options `--version-increment` and
  `--pana` removed; docs
- `gg_multi`: constraint on `gg_multi_maintain`, README

## Steps

1. Pass `mergeOnly: true` to `DoPublish` in `RepoMaintainer`
2. Rename the outcome `published` to `merged`, remove the release options
3. Update READMEs, `index.jsonc` and the plan documents

## Decisions taken

- The dependency order stays: a repo still waits for the repos it depends
  on, and a failed repo still blocks its dependents
- Repos that were never published or publish to no registry stay skipped
