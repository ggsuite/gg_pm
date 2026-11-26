<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Die Planung in Sprach- und Quartalsordner verschieben

## Motivation

- Planung und Doku teilten sich einen `doc/`-Ordner: das Quartal
  `doc/2026-Q4` stand neben den Guides, die deutsche Kopie in `doc/de/`
- Geplantes von Dokumentiertem und jede Sprache von der anderen zu
  trennen hält das Repo lesbar, auch wenn sich Quartale ansammeln

## Strategie <a id="strategy"></a>

- Alles Geplante zieht nach `pm/<lang>/<yyyy>-Q<n>/`
- Doku ohne Quartalsbezug bleibt in `doc/<lang>/`
- Das Repo legt seine Sprachen in `dna/_dna.json` fest
- Links in den verschobenen Dateien und in den READMEs werden umgeschrieben

## Realisierung 1: Die Planung <a id="implementation-1"></a>

- `doc/2026-Q4/` wurde nach `pm/en/2026-Q4/` verschoben, `doc/de/2026-Q4/`
  nach `pm/de/2026-Q4/`: Ziele, Anforderungen, Konzepte, Tickets, Team,
  Prompts, Berichte, Exporte, Blog
- `README.md` und `README.de.md` verlinken die neuen Ordner

## Realisierung 2: Sprachen und Guides <a id="implementation-2"></a>

- `dna/_dna.json` setzt `"dnaLanguages": "en,de"`
- Guides und Templates liegen jetzt in `doc/en/`, mit deutschen und
  persischen Kopien in `doc/de/` und `doc/fa/`
- Das deutsche Blog-Template ist `doc/de/templates/blog-template.md`
- `.prettierignore` und die neue `.pubignore` erfassen `doc/*/guides/`
  und `doc/*/templates/` für jede Sprache

## Aktualisierte Abhängigkeiten <a id="dependency-updates"></a>

- dna_plan: der PM-Repo-Guide beschreibt die Struktur
  `pm/<lang>/<yyyy>-Q<n>/` mit Meetings und Charts; die Planungs-Skills
  heißen `/gg-plan-…`
- dna_translate und dna_blog: Posts und Übersetzungen landen für jede
  Sprache in `pm/<lang>/<yyyy>-Q<n>/blog`
- dna_readme: `scripts/check-readme.js` prüft `README.<lang>.md` für jede
  Sprache aus `dnaLanguages`
- Der `pm-prompts`-Hook, seine `.claude/settings.json` und
  `.claude/CLAUDE_dna_gg.md` werden hier nicht mehr generiert
