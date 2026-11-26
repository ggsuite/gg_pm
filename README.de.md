# gg_pm

[English](README.md) | Deutsch

[![Tests](https://github.com/ggsuite/gg_pm/actions/workflows/quick_check.yaml/badge.svg)](https://github.com/ggsuite/gg_pm/actions/workflows/quick_check.yaml)

Projektmanagement für gg: Ziele, Anforderungen, Konzepte, Pläne,
Entscheidungen und Blog. Code enthält es nicht.

gg ist das Kommandozeilenwerkzeug, das einen Workspace aus vielen Repos
Ticket für Ticket entwickelt: Es legt das Ticket an, lässt die Prüfungen
laufen, committet, pusht, öffnet die Pull Requests und veröffentlicht die
Pakete. Sein Code liegt in den `gg_*`-Repos der Organisation `ggsuite`.

## Motivation

- Einen Ort haben, an dem die Ziele und Anforderungen von gg stehen, im
  Ordner des aktuellen Quartals
- Die Anforderungen vor jedem Ticket erarbeiten
- Jedes Ticket hier planen, bevor sich Code in einem `gg_*`-Repo ändert
- Entscheidungen einmal festhalten, mit Begründung, und nie umschreiben
- Die Zielarchitektur über die Pakete von gg zeigen

## Installation

Das Repo klonen und die DNA-Layer installieren.

```bash
git clone git@github.com:ggsuite/gg_pm.git
cd gg_pm
pnpm install
```

## Verwendung

In Claude Code planen, mit den Skills der DNA-Layer; `/gg-plan-intro`
listet sie auf und sagt, welcher als nächster dran ist.

```text
/gg-plan-requirements   engineer goals and requirements with the team
/gg-plan-schedule       cut the requirements into tickets and plan the time
/gg-plan-report         keep the report of a person for the quarter
/gg-plan-jira-export    export the next sprint of a person for Jira
/gg-ticket              create the ticket whose plan is written here
```

Ein Ticket beginnt mit einer Plandatei in
[tickets](pm/de/2026-Q4/tickets). Der Plan nennt das Ziel, dem es dient,
die Anforderungen, die es erfüllt, und die Repos, die es ändert.
Entscheidungen unterwegs landen in
[concepts/decisions](pm/de/2026-Q4/concepts/decisions).

## Einschränkungen

- Das Repo enthält keinen Code; den enthalten die Repos, die die Pläne
  nennen
- Die Prompts des Teams liegen auf dem Branch `prompts`, nie auf `main`
- Geschrieben wird nur ins aktuelle Quartal; ältere Quartale sind
  Geschichte

## Dokumentation

| Ordner                                                  | Inhalt                                |
| ------------------------------------------------------- | ------------------------------------- |
| [goals](pm/de/2026-Q4/goals)                           | Was das Projekt erreichen soll        |
| [requirements](pm/de/2026-Q4/requirements)             | Was das Produkt können oder sein muss |
| [concepts/topics](pm/de/2026-Q4/concepts/topics)       | Produktthemen und Belege              |
| [concepts/decisions](pm/de/2026-Q4/concepts/decisions) | Entscheidungen, siehe Index           |
| [concepts/ux](pm/de/2026-Q4/concepts/ux)               | Oberfläche und Abläufe                |
| [architecture](pm/de/2026-Q4/architecture)             | Zielbild des Systems                  |
| [tickets](pm/de/2026-Q4/tickets)                       | Eine Plandatei pro Ticket             |
| [bugs](pm/de/2026-Q4/bugs)                             | Eine Datei pro Bug                    |
| [team](pm/de/2026-Q4/team)                             | Personen, ihre Bereiche und Rollen    |
| [reports](pm/de/2026-Q4/reports)                       | Ein Bericht pro Person und Quartal    |
| [exports](pm/en/2026-Q4/exports)                          | Ticket-Exporte für Jira               |
| [blog](pm/de/2026-Q4/blog)                             | Ein Post pro fertigem Ticket          |
| [guides](doc/en/guides)                                    | Wie in diesem Repo gearbeitet wird    |

## Funktionsweise

Alles Geplante liegt in einem Ordner pro Quartal, `doc/<yyyy>-Q<n>`:
Ziele, Anforderungen, Team, Zeitplan, Konzepte, Tickets, Berichte,
Exporte, Blog und Prompts. Ein neues Quartal übernimmt, was noch gilt —
offene Ziele und Anforderungen, das Team, die Architektur — und nimmt die
offenen Tickets mit; alte Quartale bleiben unverändert. So reicht es, das
aktuelle Quartal zu lesen, und das Repo wird über die Jahre nicht
unübersichtlicher.

Die Anforderungen kommen zuerst: Sie werden mit dem Team erarbeitet, eine
Frage nach der anderen, bevor ein Ticket daraus geschnitten wird.

Die englische Fassung ist [README.md](README.md), die englischen Dateien
liegen in [doc](doc).

Der [PM-Repo-Guide](doc/en/guides/pm-repo-guide.md) beschreibt Struktur und
Dateinamen im Detail.

## Status

Das aktuelle Quartal ist [2026-Q4](pm/de/2026-Q4). Ein Ziel ist
vorgeschlagen:
[Ein Ticket in Minuten veröffentlichen](pm/de/2026-Q4/goals/publish-a-ticket-in-minutes.md).
Seine fünf [Anforderungen](pm/de/2026-Q4/requirements), in den Bereichen
`publish` und `maintain`, sind akzeptiert. Das Team ist noch nicht
eingetragen.

## Mitwirken

Auf einem Feature-Branch arbeiten und einen Pull Request öffnen. Mit
`gg one do commit` committen, nie mit `git commit`, sonst schlägt der
Quick Check fehl.

Siehe den [PM-Repo-Guide](doc/de/guides/pm-repo-guide.md).

## Lizenz

MIT — siehe [LICENSE](LICENSE).
