# maintain-002: Wartung merged nach main, sie veröffentlicht nicht

- Status: accepted
- Date: 2026-11-15
- Canonical source: [die englische Datei](maintain-002.md)
- Replaces: den Veröffentlichungs-Teil von [maintain-001](maintain-001.md)
- Open work: —

## Entscheidung

`gg do maintain`, der nächtliche Build eingeschlossen, merged jedes
geänderte Repo in seinen main-Branch und hört dort auf: keine neue
Version, keine Release-Überschrift in `CHANGELOG.md`, kein Upload in eine
Registry, kein Versions-Tag. Er nutzt `gg one do publish --merge-only`. Die
Änderungen warten unter `## Unreleased`, und der nächste Publish des Repos
durch ein Ticket veröffentlicht sie.

Alles, was irgendwo veröffentlicht wird — in einer Registry, als
Versions-Tag —, läuft über ein normales Ticket und sein Review. Keine
Automatik veröffentlicht selbst.

Warum: Ein Release ist eine Entscheidung des Entwicklers; Wartung hält nur
main aktuell. Der Rest von maintain-001 gilt weiter: ein eigener Rechner,
kein Review, Halt, wenn eine Major-Version ein Repo bricht.

Folge: Ein Repo, das kein Ticket veröffentlicht, behält seine
veröffentlichten Constraints; die Aktualitäts-Punkte von pana verfallen 30
Tage nach einer neuen Major-Version einer Abhängigkeit.
