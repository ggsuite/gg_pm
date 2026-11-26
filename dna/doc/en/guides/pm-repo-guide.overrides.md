## @write-requirements Write the requirements

- Group requirements by area of the product, one file per area:
  `pm/<lang>/<quarter>/requirements/<area>.md`, area in English kebab case
- Give each requirement an ID `req-<area>-<abc>`: `<abc>` is a code of
  three lowercase letters that sums up the requirement, e.g.
  `req-results-lst` for the result list. The code is unique within its
  area across all quarters; the prefix keeps it apart from decision IDs
- Never put a number into a requirement ID: requirements are reordered
  without renumbering. Never reuse or rename an ID
- Refer to several requirements of one area by the first full ID and the
  codes of the others: `req-results-lst, imp, exp`
- Write each requirement as its own section:

```markdown
## req-results-lst: Result list right after the race

- Status: accepted
- Priority: must
- Statement: The result list is ready two seconds after the last finisher
- Why: [results without desktop software](../goals/results-without-desktop-software.md),
  topic `timing`
- Acceptance: a race with 500 finishers shows the list within two seconds
```

- `Status` — `proposed`, `accepted`, `done` or `dropped`
- `Priority` — `must`, `should` or `could`; what is not wanted at all is
  `dropped`
- `Statement` — one sentence on what the product must do or be, never how
- `Why` — the goal it serves and the topic it comes from
- `Acceptance` — the checks that prove it; one bullet per check if needed
- Change a requirement in place and say what changed and when; a requirement
  that is replaced is set to `dropped` and links its successor
- A broken `done` requirement is a bug, not a new requirement
