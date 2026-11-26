<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Die DNA prüfen, ohne sie zu schreiben

## Motivation

- Der DNA-Test jedes Repos (`test/dna/dna_test.dart`) tat versteckte
  Arbeit: Er schrieb DNA-Updates und committete sie als
  `#gg: generated DNA` mitten im Ticket, während `gg can commit`
- In einem Repo war der DNA-Test gelöscht worden, um das automatische
  Update zu stoppen; die Prüfung, dass generierte Dateien unverändert
  bleiben, war aber gewollt
- Der Plan
  [dna_check_only](../tickets/2026-11-15-dna_check_only-check-the-dna-and-update-it-at-night.md)
  verlangt einen Check, der nur prüft
  ([req-dna-chk](../requirements/dna.md)); er dient dem Ziel
  [ein Ticket in Minuten veröffentlichen](../goals/publish-a-ticket-in-minutes.md)

## Strategie

- Den Check in helix legen, woher der DNA-Test kam, und helix ihn ablegen
  lassen — kein eigenes Skript, das synchron gehalten werden muss
- Eine Engine für beide Sprachen: helix-js führt denselben Check als
  WebAssembly aus
- Neue DNA kommt über `gg dna upgrade`, nicht über die Tests

## Was sich geändert hat

- helix `checkDna()`: schlägt bei einer von Hand geänderten generierten
  Datei fehl und nennt die DNA-Datei, in die die Änderung gehört; meldet
  ausstehende DNA-Updates mit `gg dna build`; schreibt, sichert und
  committet nichts
- Der abgelegte Check ruft `checkDna()`. Ein Dart-Repo bekommt
  `test/dna/dna_test.dart`, ein TypeScript-Repo `test/dna/dna.spec.ts`
- `gg dna init` ersetzt den Check immer; das neue `gg dna upgrade` legt
  ihn ab und baut die DNA
- helix-js `checkDna()` für vitest
- `gg do maintain --upgrade-dna` ruft nach dem Anheben der Schichten
  `gg dna upgrade` auf

## Entscheidungen

- Der Check behält den Pfad `test/dna/dna_test.dart`, damit ein Upgrade
  den alten Test an Ort und Stelle ersetzt
- Ausstehende DNA-Updates lassen den Check nicht fehlschlagen — sonst
  würde jede neue Schicht-Version die Tests rot machen, bis jemand baut
- Ein Repo mit `pubspec.yaml` und `package.json` gilt als Dart-Repo
- `gg dna upgrade` hebt keine Pakete an; das tut
  `gg do maintain --upgrade-dna`

## Folgetickets

1. `dna_ggsuite`: die am 2026-11-15 gewählten Schichten — dna_readme,
   dna_guides, dna_translate, dna_index, dna_blog, dna_vscode,
   dna_clean_code, dna_scripts, dna_github, dna_dart; dna_gg und
   dna_install fallen heraus. Wird vor 2. veröffentlicht.
2. Wartung: `gg do maintain --upgrade-dna` über alle ggsuite-Repos, damit
   jedes den Check bekommt; die TypeScript-Schichten aus
   `dna/_generated.json` der Dart-Repos entfernen

## Offene Punkte

- Schritte 4-7 des Plans: das nächtliche DNA-Upgrade aller
  Organisationen, die Regel für Skills in `dna_gg`, ein Ökosystem pro Repo
