# Prompts

The prompts the people of this project write to Claude Code, in any repo
whose DNA names this repo as its project management repo. They are kept on
the branch `prompts`, not here:

```text
doc/<yyyy>-Q<n>/prompts/<name>/<yyyy>-<mm>-<dd>_<repo>_<session>.md
```

- One file per Claude Code session, in the quarter it started, the time
  of each prompt as heading
- `<name>` is the first name in [people](../team/people.md) of the newest
  quarter that the git user name is or starts with, or whose `Git` line
  lists it; an unknown name goes to `_unknown`
- Only the prompts, never the answers. Tokens and passwords are replaced
  by `[redacted]`
- The hook of the `dna_gg` layer writes them; never edit them and never
  merge the branch `prompts` into `main`

Read them:

```bash
git fetch origin prompts
git ls-tree -r --name-only origin/prompts
git show origin/prompts:doc/<yyyy>-Q<n>/prompts/<name>/<file>.md
```
