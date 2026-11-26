# Wartung

Wie die Abhängigkeiten der Repos eines Oceans aktuell gehalten werden und
was darüber bekannt ist. Die Belege hinter den Anforderungen des Bereichs
[maintain](../../requirements/maintain.md).

## Was es heute gibt

- `gg do maintain` (`gg_multi_maintain`, gelesen am 2026-11-14): pro Repo
  ein frischer Klon, ein Branch `maintain_<id>`, die Aufgaben
  `--upgrade-sdk`, `--upgrade-deps [--major]`, `--upgrade-dna`, danach
  `gg one do commit` und `gg one do publish`, in
  Abhängigkeitsreihenfolge
- Major-Versionen werden nur mit `--major` übersprungen
- Nichts läuft nach Zeitplan: Der einzige Workflow der Repos ist
  `quick_check.yaml` bei Push und Pull Request. Einen nächtlichen Build
  gibt es nicht
- Neue Versionen kommen an, wenn ein Ticket gepusht oder veröffentlicht
  wird: Beides zieht alle Abhängigkeiten jedes Repos des Tickets hoch,
  Major-Versionen eingeschlossen

## Was gilt

- Ein Repo, das in keinem Ticket ist, bekommt gar kein Upgrade; ein Repo,
  das in einem Ticket ist, bekommt Upgrades, um die niemand gebeten hat,
  vermischt mit der Änderung des Tickets
- Ein Upgrade ändert keinen Code, nur Versionen; deshalb darf ein
  nächtlicher Build es ohne Review veröffentlichen, siehe
  [maintain-001](../decisions/maintain-001.md)

## Seit dem Ticket `lean_publish`

- `gg do maintain --nightly` ist `--upgrade-deps --major`: der Lauf, den
  ein eigener Rechner jede Nacht startet
- Ein Lauf mit einem gescheiterten oder blockierten Repo endet mit einem
  Fehler und schreibt `<workspace>/.maintain/<lauf-id>/report.txt`
- Push und Publish eines Tickets ziehen nichts hoch; neue Versionen kommen
  nur noch über den nächtlichen Build
