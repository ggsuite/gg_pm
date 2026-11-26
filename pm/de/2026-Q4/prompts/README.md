# Prompts

Die Prompts, die die Personen dieses Projekts an Claude Code schreiben, in
jedem Repo, dessen DNA dieses Repo als Projektmanagement-Repo nennt. Sie
liegen im Branch `prompts`, nicht hier:

```text
doc/<yyyy>-Q<n>/prompts/<name>/<yyyy>-<mm>-<dd>_<repo>_<session>.md
```

- Eine Datei pro Claude-Code-Sitzung, im Quartal ihres Beginns, die
  Uhrzeit jedes Prompts als Überschrift
- `<name>` ist der Vorname in [Personen](../team/people.md) des neuesten
  Quartals, der dem Git-Benutzernamen entspricht oder mit dem er beginnt,
  oder dessen `Git`-Zeile ihn nennt; ein unbekannter Name landet in
  `_unknown`
- Nur die Prompts, nie die Antworten. Tokens und Passwörter werden durch
  `[redacted]` ersetzt
- Der Hook des Layers `dna_gg` schreibt sie; nie von Hand ändern und den
  Branch `prompts` nie in `main` mergen

Lesen:

```bash
git fetch origin prompts
git ls-tree -r --name-only origin/prompts
git show origin/prompts:doc/<yyyy>-Q<n>/prompts/<name>/<file>.md
```
