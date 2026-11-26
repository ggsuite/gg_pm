# lean_publish_process: Publish-Schritte weglassen, die die Wartung übernehmen kann

## Ziel

Das Veröffentlichen eines Tickets tut nur noch, was in diesem Moment
geschehen muss: die Versionen der Abhängigkeiten, die das Ticket gerade
veröffentlicht hat, in `pubspec.yaml` oder `package.json` schreiben, mit
`dart pub get` oder `<Paketmanager> install` auflösen, analysieren,
mergen, hochladen und taggen. Zwei Dinge verlassen den Publish: das
Hochziehen aller übrigen Abhängigkeiten — vor allem der Major-Versionen —
und der erneute Lauf der Tests. Die Upgrades übernimmt stattdessen ein
nächtlicher Build über den Ocean, damit Pakete und Apps aktuell bleiben,
ohne dass jedes Ticket dafür bezahlt.

Es ist für Entwickler, die Tickets mit vielen Repos veröffentlichen, und
dient dem Ziel
[Ein Ticket in Minuten veröffentlichen](../goals/publish-a-ticket-in-minutes.md).
Umgesetzt mit dem Ticket `lean_publish` (begonnen am 2026-11-15), nach
dem Merge von `speed_up_gg`.

## Anforderungen

- [req-publish-own, get, chk](../requirements/publish.md): Ein Publish
  ändert nur die Abhängigkeiten des Tickets, löst auf statt hochzuziehen
  und wiederholt die Tests nicht
- [req-maintain-maj, ngt](../requirements/maintain.md): Major-Versionen
  zieht nur die Wartung hoch, und ein nächtlicher Build hält den Ocean
  aktuell

Was ein Publish und die Wartung heute tun, steht in den Themen
[publish](../concepts/topics/publish.md) und
[maintain](../concepts/topics/maintain.md). Die Entscheidungen, auf denen
der Plan beruht: [publish-001](../concepts/decisions/publish-001.md) und
[maintain-001](../concepts/decisions/maintain-001.md).

## Betroffene Repos

- `gg_multi_do_publish`: `_publishRepo` zieht nichts mehr hoch und lässt
  `can commit` nicht mehr laufen; es löst mit get oder install auf und
  führt `Analyze` aus gg_one_core aus. Sein System-Commit hält den Hash
  fest, den `did commit` und der Quick Check lesen
- `gg_one_do_publish`: `gg one do publish` zieht nur mit `--upgrade` hoch
- `gg_one_core`: Der Standard von `do.upgrade.deps.majorVersions` wird
  false. Eine `.gg/gg_rc`, die ein älteres gg geschrieben hat, nennt true
  ausdrücklich und behält es — das zählt nur noch bei einem Upgrade, um
  das jemand bittet
- `gg_one_commit`: Dokumentation und Tests des neuen Standards
- `gg_multi_commit`: `gg do push` zieht nur mit `--upgrade` hoch
- `gg_multi_maintain`: `gg do maintain --nightly` (`--upgrade-deps
  --major`); ein Lauf mit Problemen schreibt `report.txt` in seinen
  Lauf-Ordner; das README erklärt, wie man den Rechner des nächtlichen
  Builds einrichtet
- `dna_gg`: Der Development-Guide und die Skills `/gg-push` und
  `/gg-publish` sagen, was Push und Publish tun und was der nächtliche
  Build tut

## Schritte

1. Einen Publish eines echten Tickets pro Schritt mit dem Prozess-Trace
   messen — offen: Noch kein Ticket wurde mit dem neuen Ablauf
   veröffentlicht
2. Ohne Upgrade veröffentlichen — erledigt
3. Belegen, dass ein Publish nur die Abhängigkeiten des Tickets ändert —
   Unit-Tests zeigen, dass ein Publish `dart pub get` ausführt, kein
   Upgrade, und nur die Constraints der Repos schreibt, die er
   veröffentlicht hat. Ein Test, der die Manifeste eines echten Publish
   vergleicht, steht noch aus
4. `can commit` im Publish durch get und analyze ersetzen — erledigt.
   Eine neue API war nicht nötig: Der System-Commit des Publish hält den
   Hash, den der Quick Check liest, schon fest
5. Upgrades aus Commit, Push und Publish nehmen — erledigt
6. Den nächtlichen Build auf `gg do maintain` aufbauen — erledigt:
   `--nightly`. Ein gebrochenes Repo blockiert die Repos, die von ihm
   abhängen, der Lauf endet mit einem Fehler und schreibt `report.txt`
7. Den Rechner des nächtlichen Builds einrichten — der Guide steht im
   README von `gg_multi_maintain`; der Rechner selbst ist noch
   einzurichten
8. Die Guides schreiben — erledigt
9. Noch einmal messen und mit Schritt 1 vergleichen — offen

Beim Umsetzen entschieden:

- TypeScript: `Analyze` aus gg_one_core führt in einem TypeScript-Repo
  schon das Lint-Skript aus `package.json` aus
- Ein Release, das nur hochzieht, behält die Regel von `gg do maintain`:
  minor, wenn eine Abhängigkeit ihre alte Grenze verlässt, sonst patch
- Der Entwickler erfährt von einem gebrochenen Repo über den Exit-Code
  und die `report.txt` des Laufs
- pana vergibt die Punkte für aktuelle Abhängigkeiten noch 30 Tage, nachdem
  eine neue Major-Version einer Abhängigkeit erschienen ist. Ein Publish
  ohne Upgrade besteht pana deshalb, solange der nächtliche Build läuft

## Offene Fragen

- Wer betreut den Rechner des nächtlichen Builds, und welches Konto hält
  seine Zugangsdaten für GitHub, pub.dev und npm?
- Soll eine gescheiterte Nacht zusätzlich eine Mail schicken oder ein
  Issue anlegen?
