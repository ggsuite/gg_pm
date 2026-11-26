# Publish

## req-publish-own: A publish changes only the dependencies of the ticket

- Status: done (ticket `lean_publish`)
- Priority: must
- Statement: A publish changes only the version constraints of dependencies that were published in the same ticket
- Why: [publish a ticket in minutes](../goals/publish-a-ticket-in-minutes.md),
  topic `publish`
- Acceptance: After a publish, the `pubspec.yaml` or `package.json` of a
  repo differs from the committed one only in the lines of dependencies
  the ticket published
- Note: accepted on 2026-11-14

## req-publish-get: A publish resolves, it does not upgrade

- Status: done (ticket `lean_publish`)
- Priority: must
- Statement: A publish resolves dependencies with get or install, never with upgrade
- Why: [publish a ticket in minutes](../goals/publish-a-ticket-in-minutes.md),
  topic `publish`
- Acceptance: The processes a publish starts contain `dart pub get` or
  `<package manager> install`, and no upgrade or update of dependencies
- Note: accepted on 2026-11-14

## req-publish-chk: A publish does not repeat the tests

- Status: done (ticket `lean_publish`)
- Priority: must
- Statement: A publish does not run the tests again on code that passed them at the commit; it resolves and analyzes, and records the checks as passed
- Why: [publish a ticket in minutes](../goals/publish-a-ticket-in-minutes.md),
  topic `publish`
- Acceptance: A publish runs `dart pub get` and `dart analyze` per repo
  and no tests; the quick check on GitHub passes on the commit the
  publish makes
- Note: accepted on 2026-11-14, see
  [publish-001](../concepts/decisions/publish-001.md)
