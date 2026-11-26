# Maintenance

## req-maintain-maj: Major versions are raised by maintenance only

- Status: done (ticket `lean_publish`)
- Priority: must
- Statement: Major versions of dependencies are raised by maintenance only, never by commit, push or publish
- Why: [publish a ticket in minutes](../goals/publish-a-ticket-in-minutes.md),
  topic `maintain`
- Acceptance: With a new major version of a dependency released, commit,
  push and publish of a ticket leave its constraint untouched;
  `gg do maintain --upgrade-deps --major` raises it
- Note: accepted on 2026-11-14. `gg do push` upgrades nothing at all any
  more, no minor and patch versions either, see
  [maintain-001](../concepts/decisions/maintain-001.md)

## req-maintain-ngt: A nightly build keeps the ocean current

- Status: accepted
- Priority: must
- Statement: A nightly build raises the dependencies of every repo of the ocean, major versions included, and merges the result into main on its own, without a review and without publishing
- Why: [publish a ticket in minutes](../goals/publish-a-ticket-in-minutes.md),
  topic `maintain`
- Acceptance: After a night without failures, no repo of the ocean is
  behind a released version of one of its dependencies, the main branch of every
  raised repo carries the raise, and no version was released; when a major version breaks a repo, the build stops
  and tells the developer which repo broke and why
- Note: accepted on 2026-11-14, see
  [maintain-001](../concepts/decisions/maintain-001.md); merge instead of
  publish accepted on 2026-11-15, see
  [maintain-002](../concepts/decisions/maintain-002.md)

## req-maintain-dna: A nightly maintenance run keeps the DNA current

- Status: accepted
- Priority: must
- Statement: A nightly maintenance run keeps the DNA of every repo current — the repos of ggsuite and all other repos of the ocean
- Why: [publish a ticket in minutes](../goals/publish-a-ticket-in-minutes.md)
  — when tickets no longer update the DNA
  ([req-dna-chk](dna.md#req-dna-chk-a-check-proves-that-the-generated-dna-files-are-unchanged)),
  maintenance is the one place where new DNA arrives
- Acceptance: After a night without failures, the DNA layers of no repo of
  the ocean are behind their newest released version, the DNA is
  generated anew and every changed repo is merged into main, unreleased
- Note: stated by the user on 2026-11-15. `gg do maintain --upgrade-dna`
  exists; `--nightly` upgrades the dependencies only
