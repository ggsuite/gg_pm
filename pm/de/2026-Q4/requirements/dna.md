# DNA

## req-dna-chk: Eine Prüfung belegt, dass die generierten DNA-Dateien unverändert sind

- Status: accepted
- Priority: must
- Statement: Jedes Repo hat eine Prüfung, die sicherstellt, dass die von seiner DNA generierten Dateien unverändert sind, und die Prüfung verändert selbst nichts
- Why: [Ein Ticket in Minuten veröffentlichen](../goals/publish-a-ticket-in-minutes.md)
  — keine versteckte Arbeit: Heute schreibt der DNA-Test eines Repos die
  DNA neu und committet sie (`#gg: generated DNA`), mitten in einem Ticket
- Acceptance: Die Prüfung schlägt fehl, wenn eine DNA-generierte Datei von
  dem abweicht, was die DNA erzeugt, nennt die Datei und lässt Arbeitsbaum
  und Historie unberührt — ob sie besteht oder fehlschlägt
- Note: vom Nutzer am 2026-11-15 vorgegeben; die Formulierung der Abnahme
  ist ein Vorschlag

## req-dna-src: Änderungen an Skills gehen nach dna_gg

- Status: accepted
- Priority: must
- Statement: Eine Änderung an einem Skill eines ggsuite-Repos wird nach `dna_gg` übertragen, in die DNA-Schicht, aus der die Skills stammen
- Why: Die Skills eines Repos erzeugt seine DNA; eine Änderung nur im Repo
  geht beim nächsten DNA-Update verloren, und allen anderen Repos fehlt sie
- Acceptance: Nach einem Ticket, das einen Skill in einem ggsuite-Repo
  geändert hat, enthält `dna_gg` dieselbe Änderung, und die Prüfung aus
  [req-dna-chk](#req-dna-chk-eine-prüfung-belegt-dass-die-generierten-dna-dateien-unverändert-sind)
  besteht in diesem Repo
- Note: vom Nutzer am 2026-11-15 vorgegeben

## req-dna-eco: Die DNA eines Repos kommt aus einem Ökosystem

- Status: accepted
- Priority: must
- Statement: Die DNA-Schichten eines Repos kommen aus einem Ökosystem: Die `dna/_generated.json` eines Repos nennt entweder pub-Pakete oder npm-Pakete, nie beides
- Why: Ein Dart-Repo soll für seine DNA weder Node noch npm brauchen, ein
  TypeScript-Repo weder Dart noch pub
- Acceptance: In jedem Repo des Oceans nennen die Schichten in
  `dna/_generated.json`, die ein Ökosystem angeben, dasselbe
- Note: vom Nutzer am 2026-11-15 vorgegeben. An diesem Tag führte jedes
  Dart-Repo des Tickets `lean_publish` `@ggdna/dna-github` (npm) neben
  seinen pub-Schichten
