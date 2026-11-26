# Publish a ticket in minutes

## Status

proposed since 2026-Q4 — derived on 2026-11-14 from the ticket
`speed_up_gg`, which asks for a publish ten times faster; not yet
confirmed. The measures are proposals

## Outcome

A developer publishes a ticket with many repos in minutes. gg does at
publish time only what has to happen then — write the versions of the
dependencies the ticket published, merge, upload, tag — and leaves the
upgrade of all other dependencies to a nightly build. Packages and apps
still stay on current versions, because the nightly build raises them
every night.

## Measure

- Publish time: a ticket is published in a tenth of the time measured in
  step 1 of the ticket `lean_publish_process`
- No hidden work: a publish changes no dependency the ticket did not
  publish
- Current versions: after a night without failures, no repo of the ocean
  is behind a released version of one of its dependencies

## Requirements

- [publish](../requirements/publish.md)
- [maintain](../requirements/maintain.md)
- [dna](../requirements/dna.md)
