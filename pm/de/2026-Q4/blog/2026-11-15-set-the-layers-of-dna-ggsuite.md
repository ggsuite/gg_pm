<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Die Schichten von dna_ggsuite festlegen

## Motivation

- Folgeticket 1 von
  [dna_check_only](../tickets/2026-11-15-dna_check_only-check-the-dna-and-update-it-at-night.md)
  legt fest, welche Schichten die Dachschicht `dna_ggsuite` trägt
- Es muss veröffentlicht sein, bevor der Wartungslauf
  `gg do maintain --upgrade-dna` die neue DNA in jedes ggsuite-Repo
  bringt

## Strategie

- Die Schichten übernehmen, die der Nutzer am 2026-11-15 gewählt hat
- Sie im Ticket `dna_ggsuite_layers` umsetzen
- Im Folgeticket festhalten, was erledigt ist und was zurückgestellt wird

## Umsetzung

- `dna_ggsuite` trägt jetzt dna_readme, dna_guides, dna_translate,
  dna_index, dna_blog, dna_install, dna_vscode, dna_clean_code, dna_scripts und
  dna_github
- `dna_gg` ist raus, das bringt der gg-Workspace mit; `dna_install`
  bleibt, anders als zuerst gewählt
- Ein Major-Release von `dna_ggsuite`

## Offene Punkte

- `dna_dart` bleibt vorerst draußen: Das veröffentlichte Paket bringt
  noch `dna_gg` und `dna_install` mit und verlangt `dna_translate`
  ^0.3.0. Es braucht ein neues Release nur mit dem Dart-Spezifischen, auf
  pub und npm, bevor es dazukommt
- Als Nächstes folgt Folgeticket 2, der Wartungslauf
