<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Move the plans into language and quarter folders

## Motivation

- Plans and documentation shared one `doc/` folder: the quarter
  `doc/2026-Q4` stood next to the guides, the German copy in `doc/de/`
- Separating what is planned from what is documented, and each language
  from the other, keeps the repo easy to read as quarters pile up

## Strategy

- Everything planned moves to `pm/<lang>/<yyyy>-Q<n>/`
- Documentation without a quarter stays in `doc/<lang>/`
- The repo declares its languages in `dna/_dna.json`
- Links in the moved files and in the READMEs are rewritten

## Implementation 1: The plans

- `doc/2026-Q4/` moved to `pm/en/2026-Q4/`, `doc/de/2026-Q4/` to
  `pm/de/2026-Q4/`: goals, requirements, concepts, tickets, team,
  prompts, reports, exports, blog
- `README.md` and `README.de.md` link to the new folders

## Implementation 2: Languages and guides

- `dna/_dna.json` sets `"dnaLanguages": "en,de"`
- The guides and templates now live in `doc/en/`, with German and Farsi
  copies in `doc/de/` and `doc/fa/`
- The German blog template is `doc/de/templates/blog-template.md`
- `.prettierignore` and the new `.pubignore` cover `doc/*/guides/` and
  `doc/*/templates/` for every language

## Dependency updates

- dna_plan: the PM repo guide describes the `pm/<lang>/<yyyy>-Q<n>/`
  structure with meetings and charts; the planning skills are named
  `/gg-plan-…`
- dna_translate and dna_blog: posts and translations go to
  `pm/<lang>/<yyyy>-Q<n>/blog` for every language
- dna_readme: `scripts/check-readme.js` checks `README.<lang>.md` for
  every language in `dnaLanguages`
- The `pm-prompts` hook, its `.claude/settings.json` and
  `.claude/CLAUDE_dna_gg.md` are no longer generated here
