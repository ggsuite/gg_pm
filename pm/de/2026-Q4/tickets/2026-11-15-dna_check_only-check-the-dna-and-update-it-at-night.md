# dna_check_only: Die DNA in jedem Repo prüfen, aktualisieren nur nachts

## Ziel

Am 2026-11-15 notiert, noch nicht im Detail geplant.

Jedes Repo prüft, dass die von seiner DNA generierten Dateien unverändert
sind, und nicht mehr: Die Prüfung schreibt keine DNA und committet nichts.
Neue DNA kommt über einen nächtlichen Wartungslauf über den ganzen Ocean —
die Repos von ggsuite und alle anderen. Eine Änderung an einem Skill eines
ggsuite-Repos wird in `dna_gg` gemacht, woher die Skills stammen. Und die
DNA eines Repos kommt aus einem Ökosystem: pub oder npm, nicht beides.

Heute tut der DNA-Test eines Repos (`test/dna/dna_test.dart`, helix'
`runDnaTest`) mehr als prüfen: Er kopiert lokal geänderte Instanzen weg und
schreibt den DNA-Inhalt zurück, und er schreibt DNA-Updates und committet
sie als `#gg: generated DNA` — mitten in einem Ticket, während
`gg can commit`. Das ist versteckte Arbeit, um die das Ticket nicht
gebeten hat.

Es dient dem Ziel
[Ein Ticket in Minuten veröffentlichen](../goals/publish-a-ticket-in-minutes.md).

## Anforderungen

- [req-dna-chk](../requirements/dna.md): Eine Prüfung belegt, dass die
  generierten DNA-Dateien unverändert sind, und verändert nichts
- [req-dna-src](../requirements/dna.md): Änderungen an Skills gehen nach
  `dna_gg`
- [req-dna-eco](../requirements/dna.md): Die DNA eines Repos kommt aus
  einem Ökosystem
- [req-maintain-dna](../requirements/maintain.md): Ein nächtlicher
  Wartungslauf hält die DNA jedes Repos aktuell

## Betroffene Repos

- `helix`: ein Prüfmodus für den DNA-Test — die generierten Dateien mit
  dem vergleichen, was die DNA erzeugt, Abweichungen melden, nichts
  schreiben
- Die DNA-Schichten (`dna_gg`, `dna_ggsuite`, die Schichten der anderen
  Organisationen): den reinen Prüftest in jedem Repo installieren
- `gg_multi_maintain`: Der nächtliche Lauf hebt auch die DNA an
  (`--upgrade-dna`), für jede Organisation des Oceans
- `dna_gg`: Der Development-Guide sagt, dass ein Skill in `dna_gg`
  geändert wird, nicht im Repo
- Die Schicht, die `@ggdna/dna-github` in Dart-Repos bringt: ein
  pub-Gegenstück oder eine Schichtenliste je Ökosystem

## Schritte

1. Lesen, wie `runDnaTest` entscheidet, was es schreibt, und wo die reine
   Prüfung hineinpasst
2. Den Prüfmodus in helix einbauen und testen: Eine geänderte generierte
   Datei lässt die Prüfung fehlschlagen, nichts wird geschrieben, nichts
   committet
3. Den reinen Prüftest über die DNA-Schichten in jedes Repo bringen
4. Den nächtlichen Lauf von `gg do maintain` die DNA jeder Organisation
   des Oceans anheben lassen
5. Die Regel für Skills in den Development-Guide von `dna_gg` schreiben
6. Jedem Repo nur Schichten seines eigenen Ökosystems geben und die
   Prüfung bei einer Mischung fehlschlagen lassen
7. Ausrollen: Ein nächtlicher Lauf aktualisiert die DNA überall

## Offene Fragen

- Lebt die Prüfung in helix (ein Modus von `runDnaTest`) oder in einem
  eigenen Skript, das die DNA installiert?
- Was sagt eine fehlgeschlagene Prüfung dem Entwickler: die geänderten
  Dateien, und dass die Änderung in die DNA-Schicht gehört?
- Nimmt `--nightly` `--upgrade-dna` mit, oder startet der nächtliche
  Zeitplan beide Flags?
- Wie werden Repos anderer Organisationen erreicht, deren DNA-Schichten
  nicht `dna_gg` sind?
- Welche Schicht bringt `@ggdna/dna-github` (npm) in die Dart-Repos, und
  gibt es dafür ein pub-Paket?
- Die Dart-Repos führen in `dna/_generated.json` auch gewöhnliche Pakete
  wie `gg_log` und `gg_args` als DNA-Schichten — gewollt?

## Umgesetzt in dna_check_only

- `helix`: `instantiateDna(checkOnly: true)` plant den Lauf und schreibt
  nichts; `checkDna()` schlägt bei von Hand geänderten generierten Dateien
  fehl (mit der DNA-Datei, in die die Änderung gehört) und meldet
  ausstehende DNA-Updates nur, mit `gg dna build`
- `helix`: der abgelegte Check `test/dna/dna_test.dart` ruft `checkDna()`;
  ein Dart-Projekt (`pubspec.yaml`) bekommt den Dart-Check, ein
  TypeScript-Projekt den vitest-Check `test/dna/dna.spec.ts`. `helix init`
  ersetzt den Check immer; das neue `helix upgrade` (`gg dna upgrade`)
  legt ihn ab und baut
- `helix-js`: `checkDna()` für vitest, über dieselbe Engine
- `gg_multi_maintain`: `--upgrade-dna` ruft nach dem Anheben der Schichten
  `gg dna upgrade` statt des DNA-Tests auf

## Folgetickets

1. Schichten von `dna_ggsuite`: festlegen, welche ggdna-Schichten
   `dna_ggsuite` trägt, `dna_gg` entfernen (bringt der gg-Workspace mit),
   veröffentlichen — vor 2.
   Vom Nutzer gewählt am 2026-11-15: dna_readme, dna_guides,
   dna_translate, dna_index, dna_blog, dna_vscode, dna_clean_code,
   dna_scripts, dna_github, dna_dart; raus: dna_gg, dna_install.
   Wird im Ticket `dna_ggsuite_layers` umgesetzt; `dna_install` bleibt
   doch; `dna_dart` bleibt dort
   vorerst draußen, weil das veröffentlichte Paket noch `dna_gg` und
   `dna_install` mitbringt und `dna_translate` ^0.3.0 verlangt
2. Wartung: `gg do maintain --upgrade-dna` über alle ggsuite-Repos, damit
   jedes den neuen DNA-Check bekommt; die TypeScript-Schichten aus
   `dna/_generated.json` der Dart-Repos entfernen (req-dna-eco)
