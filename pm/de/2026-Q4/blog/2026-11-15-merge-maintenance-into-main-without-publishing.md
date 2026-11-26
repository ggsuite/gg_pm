<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Wartung nach main mergen, ohne zu veröffentlichen

## Motivation

- Wartung hält die main-Branches aktuell; ein Release ist eine Entscheidung
  des Entwicklers
- Bisher veröffentlichten `gg do maintain` und sein nächtlicher Build jedes
  geänderte Repo selbst, ohne Review
- Neue Regel: Alles, was irgendwo veröffentlicht wird — in einer Registry,
  als Versions-Tag — läuft über ein normales Ticket und sein Review

## Strategie

- Die Entscheidung [maintain-002](../concepts/decisions/maintain-002.md),
  akzeptiert am 2026-11-15, ersetzt den Veröffentlichungs-Teil von
  maintain-001
- Der nächtliche Build bleibt: ein eigener Rechner, kein Review, Halt, wenn
  eine Major-Version ein Repo bricht
- Er merged jetzt nach main und veröffentlicht nichts

## Umsetzung

- `req-maintain-ngt` und `req-maintain-dna` verlangen jetzt gemergte,
  unveröffentlichte Änderungen auf main
- Ticket-Datei `maintain_merge_only`, Englisch und Deutsch
- `gg do maintain` merged mit `gg one do publish --merge-only`

## Offene Punkte

- Ein Upgrade auf main kommt erst mit dem nächsten Ticket, das das Repo
  veröffentlicht, in die Registry
- Die Aktualitäts-Punkte von pana verfallen 30 Tage nach einer neuen
  Major-Version einer Abhängigkeit für Repos, die kein Ticket veröffentlicht
