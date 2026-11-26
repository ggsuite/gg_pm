<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Den schlanken Publish umsetzen

## Motivation

- Der Plan
  [lean_publish_process](../tickets/2026-11-14-lean_publish_process-leave-out-publish-steps-that-maintenance-can-do.md)
  nimmt zwei Dinge aus dem Publish: das Hochziehen aller Abhängigkeiten
  und den zweiten Lauf der Tests. Die Upgrades übernimmt ein nächtlicher
  Build
- Er dient dem Ziel
  [Ein Ticket in Minuten veröffentlichen](../goals/publish-a-ticket-in-minutes.md)
- Das Ticket `lean_publish` setzt ihn um. Ein erster Versuch wurde
  verworfen und neu begonnen, nachdem gg selbst schlanker geworden war:
  Ein Ticket bekommt jetzt standardmäßig keine Repos dazwischen

## Strategie

- Den Schritten des Plans folgen, ein Repo nach dem anderen
- Die offenen Fragen beantworten, wo der Code sie beantwortet, und die
  übrigen offen lassen
- In diesem Repo festhalten, was getan ist, was unterwegs entschieden
  wurde und was noch offen ist

## Was Publish und Push jetzt tun

- Ein Publish löst auf (`dart pub get`, `<pm> install`) und analysiert;
  er zieht nichts hoch und lässt die Tests nicht noch einmal laufen
  ([req-publish-own, get, chk](../requirements/publish.md) — erledigt)
- `gg do push` und `gg one do publish` ziehen nur mit `--upgrade` hoch,
  und ein Upgrade überspringt Major-Versionen nur, wenn ein Repository es
  verlangt ([req-maintain-maj](../requirements/maintain.md) — erledigt)
- Den Hash, den der Quick Check auf GitHub liest, schreibt schon der
  System-Commit des Publish; eine neue API war nicht nötig

## Der nächtliche Build

- `gg do maintain --nightly` ist `--upgrade-deps --major`. Ein gebrochenes
  Repo blockiert die Repos, die von ihm abhängen, der Lauf endet mit
  einem Fehler und schreibt `report.txt` in seinen Lauf-Ordner
- Das README von `gg_multi_maintain` beschreibt, wie man seinen Rechner
  einrichtet
- [req-maintain-ngt](../requirements/maintain.md) bleibt `accepted`, bis
  dieser Rechner läuft

## Unterwegs entschieden

- `Analyze` führt in einem TypeScript-Repo schon das Lint-Skript aus
- Ein Release, das nur hochzieht, behält die Versionsregel von
  `gg do maintain`
- pana vergibt die Punkte für aktuelle Abhängigkeiten noch 30 Tage nach
  einer neuen Major-Version — ein Publish ohne Upgrade besteht, solange der
  nächtliche Build läuft
- Die Entscheidungen [publish-001](../concepts/decisions/publish-001.md)
  und [maintain-001](../concepts/decisions/maintain-001.md) nennen ihre
  offene Arbeit neu, die Themen [publish](../concepts/topics/publish.md)
  und [maintain](../concepts/topics/maintain.md) sagen, was sich geändert
  hat
- Der Inhalt dieses Repos sagt jetzt `gg_pm` statt `gg-pm`, wie das
  Repository auf GitHub

## Offene Punkte

- Einen Publish vorher und nachher messen (Schritte 1 und 9 des Plans)
- Ein Test, der die Manifeste eines echten Publish vergleicht
- Den Rechner des nächtlichen Builds einrichten und klären, wer ihn
  betreut
- Ob eine gescheiterte Nacht zusätzlich eine Mail schicken oder ein Issue
  anlegen soll
