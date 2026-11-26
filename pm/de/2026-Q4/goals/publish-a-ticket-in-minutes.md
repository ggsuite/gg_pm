# Ein Ticket in Minuten veröffentlichen

## Status

proposed since 2026-Q4 — am 2026-11-14 aus dem Ticket `speed_up_gg`
abgeleitet, das einen zehnmal schnelleren Publish verlangt; noch nicht
bestätigt. Die Maße sind Vorschläge

## Ergebnis

Ein Entwickler veröffentlicht ein Ticket mit vielen Repos in Minuten. gg
tut beim Publish nur, was in diesem Moment geschehen muss — die Versionen
der Abhängigkeiten schreiben, die das Ticket veröffentlicht hat, mergen,
hochladen, taggen — und überlässt das Hochziehen aller anderen
Abhängigkeiten einem nächtlichen Build. Pakete und Apps bleiben trotzdem
aktuell, weil der nächtliche Build sie jede Nacht hochzieht.

## Maß

- Publish-Zeit: Ein Ticket ist in einem Zehntel der Zeit veröffentlicht,
  die in Schritt 1 des Tickets `lean_publish_process` gemessen wird
- Keine versteckte Arbeit: Ein Publish ändert keine Abhängigkeit, die das
  Ticket nicht veröffentlicht hat
- Aktuelle Versionen: Nach einer Nacht ohne Fehler liegt kein Repo des
  Oceans hinter einer veröffentlichten Version einer seiner
  Abhängigkeiten

## Anforderungen

- [publish](../requirements/publish.md)
- [maintain](../requirements/maintain.md)
- [dna](../requirements/dna.md)
