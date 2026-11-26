<!--
@license
Copyright (c) ggsuite

Use of this source code is governed by terms that can be
found in the LICENSE file in the root of this package.
-->

# Set the layers of dna_ggsuite

## Motivation

- Follow-up 1 of
  [dna_check_only](../tickets/2026-11-15-dna_check_only-check-the-dna-and-update-it-at-night.md)
  chooses the layers the umbrella layer `dna_ggsuite` carries
- It must be published before the maintenance run
  `gg do maintain --upgrade-dna` brings the new DNA to every ggsuite repo

## Strategy

- Take the layers the user chose on 2026-11-15
- Implement them in ticket `dna_ggsuite_layers`
- Note in the follow-up what is done and what is held back

## Implementation

- `dna_ggsuite` now carries dna_readme, dna_guides, dna_translate,
  dna_index, dna_blog, dna_install, dna_vscode, dna_clean_code, dna_scripts and
  dna_github
- `dna_gg` is out, the gg workspace brings it; `dna_install` stays,
  unlike first chosen
- A major release of `dna_ggsuite`

## Open Points

- `dna_dart` is held back: the published package still carries `dna_gg`
  and `dna_install` and needs `dna_translate` ^0.3.0. It needs a new
  release with only the Dart specifics, on pub and npm, before it can
  join
- Follow-up 2, the maintenance run, comes next
