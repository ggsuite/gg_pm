<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# gg-pm einrichten und einen schlanken Publish planen

## Motivation

- gg hatte keinen Ort für seine Pläne: Ziele, Anforderungen und
  Entscheidungen lebten in Chats und in den Köpfen. Dieses Repo ist jetzt
  dieser Ort
- Der erste Plan darin beantwortet eine Frage aus dem Alltag: Warum dauert
  das Veröffentlichen eines Tickets mit vielen Repos so lange, und welche
  seiner Schritte können weg?
- Das Ziel dahinter:
  [Ein Ticket in Minuten veröffentlichen](../goals/publish-a-ticket-in-minutes.md)

## Strategie

- Das Repo nach den Regeln von `dna-plan` einrichten: Alles Geplante liegt
  im Quartalsordner, deutsche Kopien unter `doc/de`
- Schritt für Schritt lesen, was ein Publish heute tut, bevor etwas
  vorgeschlagen wird
- Die Anforderungen mit dem Product Owner erarbeiten, eine nach der
  anderen, und nur aufschreiben, was bestätigt wurde
- Die Entscheidungen unterwegs festhalten, mit Begründung
- Nur planen: Der Code ändert sich, nachdem ein anderes Ticket gemergt
  ist, das dieselbe Funktion anfasst

## Das Repo

- DNA-Layer `@ggdna/dna-plan` und `@tssuite/dna-ggsuite`: die Guides, die
  Skills und der Quick Check
- Kein Code: Das TypeScript-Gerüst ist weg, `package.json` hält nur die
  DNA-Layer
- `doc/2026-Q4` mit Zielen, Anforderungen, Konzepten, Architektur, Tickets,
  Bugs, Team, Berichten, Exporten, Blog und dem Hinweis zu den Prompts
- Anforderungen tragen Kürzel aus drei Buchstaben, z. B.
  `req-publish-own`, über `dna/doc/guides/pm-repo-guide.overrides.md`
- Öffentlich, unter der MIT-Lizenz, mit geschütztem `main`: Branch-Regeln
  brauchen im Tarif der Organisation ein öffentliches Repo
- README auf Englisch und Deutsch nach der README-Vorlage

## Was ein Publish heute tut

- Für jedes Repo eines Tickets zieht er alle Abhängigkeiten hoch,
  Major-Versionen eingeschlossen, frischt sie zweimal auf und lässt
  analyze, format und Tests noch einmal laufen
- Die Tests liefen schon beim Commit, auf demselben Code
- Nichts zieht Abhängigkeiten nach Zeitplan hoch: Ein Publish ist der Ort,
  an dem neue Versionen zufällig ankommen

## Der Plan

- Fünf akzeptierte Anforderungen in den Bereichen
  [publish](../requirements/publish.md) und
  [maintain](../requirements/maintain.md)
- Ein Publish ändert nur die Versionen der Abhängigkeiten, die das Ticket
  veröffentlicht hat, löst mit get oder install auf und analysiert statt
  zu testen — [publish-001](../concepts/decisions/publish-001.md)
- Den Hash der Prüfungen schreibt er trotzdem, damit der Quick Check auf
  GitHub besteht
- `gg do push` zieht nichts mehr hoch
- Ein nächtlicher Build auf einem eigenen Rechner zieht alle
  Abhängigkeiten hoch, veröffentlicht ohne Review und hält an, wenn eine
  Major-Version ein Repo bricht —
  [maintain-001](../concepts/decisions/maintain-001.md)
- Die Schritte und die betroffenen Repos stehen im
  [Ticketplan](../tickets/2026-11-14-lean_publish_process-leave-out-publish-steps-that-maintenance-can-do.md)

## Offene Punkte

- Umgesetzt ist nichts; der Code folgt nach dem Ticket `speed_up_gg`
- Das Ziel ist vorgeschlagen, nicht bestätigt; seine Maße sind Vorschläge
- Das Team und seine Rollen sind noch nicht eingetragen
- Offen im Plan: die Zugangsdaten des Nacht-Rechners, wie ein Entwickler
  von einem gebrochenen Repo erfährt, was `dart analyze` in einem
  TypeScript-Repo ersetzt, und die Version eines Releases, das nur
  hochzieht
- Noch nennt kein Repo `gg-pm` als sein Projektmanagement-Repo; sobald
  eines das tut, landen die Prompts des Teams auf dem öffentlichen Branch
  `prompts`
