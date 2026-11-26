# gg_pm

English | [Deutsch](README.de.md)

[![Tests](https://github.com/ggsuite/gg_pm/actions/workflows/quick_check.yaml/badge.svg)](https://github.com/ggsuite/gg_pm/actions/workflows/quick_check.yaml)

Project management for gg: goals, requirements, concepts, plans, decisions
and blog. It holds no code.

gg is the command line tool that develops a workspace of many repos ticket
by ticket: it creates the ticket, runs the checks, commits, pushes, opens
the pull requests and publishes the packages. Its code lives in the `gg_*`
repos of the organization `ggsuite`.

## Motivation

- Keep one place where the goals and requirements of gg are written down,
  in the folder of the current quarter
- Engineer the requirements before any ticket
- Plan every ticket here before code changes in a `gg_*` repo
- Record decisions once, with their reason, and never rewrite them
- Show the target architecture across the packages of gg

## Installation

Clone the repo and install the DNA layers.

```bash
git clone git@github.com:ggsuite/gg_pm.git
cd gg_pm
pnpm install
```

## Usage

Plan in Claude Code with the skills of the DNA layers; `/gg-plan-intro`
lists them and says which one comes next.

```text
/gg-plan-requirements   engineer goals and requirements with the team
/gg-plan-schedule       cut the requirements into tickets and plan the time
/gg-plan-report         keep the report of a person for the quarter
/gg-plan-jira-export    export the next sprint of a person for Jira
/gg-ticket              create the ticket whose plan is written here
```

A ticket starts with a plan file in [tickets](pm/en/2026-Q4/tickets). The
plan names the goal it serves, the requirements it fulfils and the repos
it changes. Decisions made on the way land in
[concepts/decisions](pm/en/2026-Q4/concepts/decisions).

## Limitations

- The repo holds no code; the repos the plans name do
- The prompts of the team are kept on the branch `prompts`, never on
  `main`
- Only the current quarter is written to; older quarters are history

## Documentation

| Folder                                               | Content                         |
| ---------------------------------------------------- | ------------------------------- |
| [goals](pm/en/2026-Q4/goals)                           | What the project should achieve |
| [requirements](pm/en/2026-Q4/requirements)             | What the product must do or be  |
| [concepts/topics](pm/en/2026-Q4/concepts/topics)       | Product topics and evidence     |
| [concepts/decisions](pm/en/2026-Q4/concepts/decisions) | Decisions, see the index        |
| [concepts/ux](pm/en/2026-Q4/concepts/ux)               | Surface and flows               |
| [architecture](pm/en/2026-Q4/architecture)             | Target picture of the system    |
| [tickets](pm/en/2026-Q4/tickets)                       | One plan file per ticket        |
| [bugs](pm/en/2026-Q4/bugs)                             | One file per bug                |
| [team](pm/en/2026-Q4/team)                             | People, their areas and roles   |
| [reports](pm/en/2026-Q4/reports)                       | One report per person, quarter  |
| [exports](pm/en/2026-Q4/exports)                       | Ticket exports for Jira         |
| [blog](pm/en/2026-Q4/blog)                             | One post per finished ticket    |
| [guides](doc/en/guides)                                 | How to work in this repo        |

## How it works

Everything planned lives in one folder per quarter, `doc/<yyyy>-Q<n>`:
goals, requirements, team, schedule, concepts, tickets, reports, exports,
blog and prompts. A new quarter copies what still holds — open goals and
requirements, the team, the architecture — and takes the open tickets
along; old quarters stay untouched. So the current quarter is all one has
to read, and the repo does not grow harder to read over the years.

The requirements come first: they are engineered with the team, one
question at a time, before any ticket is cut from them.

German copies of all files live in [doc/de](pm/de), see
[README.de.md](README.de.md).

The [PM repo guide](doc/en/guides/pm-repo-guide.md) describes the structure
and the file names in detail.

## Status

The current quarter is [2026-Q4](pm/en/2026-Q4). One goal is proposed:
[publish a ticket in minutes](pm/en/2026-Q4/goals/publish-a-ticket-in-minutes.md).
Its five [requirements](pm/en/2026-Q4/requirements), in the areas `publish`
and `maintain`, are accepted. The team is not written down yet.

## Contributing

Work on a feature branch and open a pull request. Commit with
`gg one do commit`, never with `git commit`, or the quick check fails.

See the [PM repo guide](doc/en/guides/pm-repo-guide.md).

## License

MIT — see [LICENSE](LICENSE).
