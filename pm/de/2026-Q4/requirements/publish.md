# Publish

## req-publish-own: Ein Publish ändert nur die Abhängigkeiten des Tickets

- Status: done (ticket `lean_publish`)
- Priority: must
- Statement: Ein Publish ändert nur die Versionsangaben von Abhängigkeiten, die im selben Ticket veröffentlicht wurden
- Why: [Ein Ticket in Minuten veröffentlichen](../goals/publish-a-ticket-in-minutes.md),
  Thema `publish`
- Acceptance: Nach einem Publish unterscheidet sich die `pubspec.yaml`
  oder `package.json` eines Repos von der committeten nur in den Zeilen
  der Abhängigkeiten, die das Ticket veröffentlicht hat
- Note: akzeptiert am 2026-11-14

## req-publish-get: Ein Publish löst auf, er zieht nicht hoch

- Status: done (ticket `lean_publish`)
- Priority: must
- Statement: Ein Publish löst Abhängigkeiten mit get oder install auf, nie mit upgrade
- Why: [Ein Ticket in Minuten veröffentlichen](../goals/publish-a-ticket-in-minutes.md),
  Thema `publish`
- Acceptance: Die Prozesse, die ein Publish startet, enthalten
  `dart pub get` oder `<Paketmanager> install` und kein Upgrade oder
  Update von Abhängigkeiten
- Note: akzeptiert am 2026-11-14

## req-publish-chk: Ein Publish wiederholt die Tests nicht

- Status: done (ticket `lean_publish`)
- Priority: must
- Statement: Ein Publish lässt die Tests nicht noch einmal auf Code laufen, der sie beim Commit bestanden hat; er löst auf und analysiert und hält die Prüfungen als bestanden fest
- Why: [Ein Ticket in Minuten veröffentlichen](../goals/publish-a-ticket-in-minutes.md),
  Thema `publish`
- Acceptance: Ein Publish führt pro Repo `dart pub get` und
  `dart analyze` aus und keine Tests; der Quick Check auf GitHub besteht
  auf dem Commit, den der Publish macht
- Note: akzeptiert am 2026-11-14, siehe
  [publish-001](../concepts/decisions/publish-001.md)
