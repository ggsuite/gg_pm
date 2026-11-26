# maintain_merge_only: Wartung merged nach main, Releases laufen über Tickets

## Ziel

Geplant und umgesetzt am 2026-11-15 im Ticket `maintain_merge_only`.

`gg do maintain`, der nächtliche Build eingeschlossen, merged jedes
geänderte Repo nach main und veröffentlicht nichts. Alles, was irgendwo
veröffentlicht wird, läuft über ein normales Ticket und sein Review. Siehe
[maintain-002](../concepts/decisions/maintain-002.md).

Es dient dem Ziel
[Ein Ticket in Minuten veröffentlichen](../goals/publish-a-ticket-in-minutes.md).

## Anforderungen

- [req-maintain-ngt](../requirements/maintain.md): Der nächtliche Build
  merged seine Upgrades nach main, ohne zu veröffentlichen
- [req-maintain-dna](../requirements/maintain.md): dasselbe für die DNA

## Betroffene Repos

- `gg_pm`: Entscheidung maintain-002, die beiden Anforderungen
- `gg_multi_maintain`: jedes Repo mit `gg one do publish --merge-only`
  mergen; Ergebnis `merged`; Optionen `--version-increment` und `--pana`
  entfernt; Doku
- `gg_multi`: Constraint auf `gg_multi_maintain`, README

## Schritte

1. `mergeOnly: true` an `DoPublish` in `RepoMaintainer` übergeben
2. Ergebnis `published` in `merged` umbenennen, Release-Optionen entfernen
3. READMEs, `index.jsonc` und die Plandokumente aktualisieren

## Getroffene Entscheidungen

- Die Abhängigkeits-Reihenfolge bleibt: Ein Repo wartet weiter auf seine
  Abhängigkeiten, ein fehlgeschlagenes Repo blockiert weiter die davon
  abhängigen
- Nie veröffentlichte Repos und Repos ohne Registry bleiben übersprungen
