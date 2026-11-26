# Wartung

## req-maintain-maj: Major-Versionen zieht nur die Wartung hoch

- Status: done (ticket `lean_publish`)
- Priority: must
- Statement: Major-Versionen von Abhängigkeiten zieht nur die Wartung hoch, nie Commit, Push oder Publish
- Why: [Ein Ticket in Minuten veröffentlichen](../goals/publish-a-ticket-in-minutes.md),
  Thema `maintain`
- Acceptance: Ist eine neue Major-Version einer Abhängigkeit erschienen,
  lassen Commit, Push und Publish eines Tickets deren Versionsangabe
  unberührt; `gg do maintain --upgrade-deps --major` zieht sie hoch
- Note: akzeptiert am 2026-11-14. `gg do push` zieht gar nichts mehr hoch,
  auch keine Minor- und Patch-Versionen, siehe
  [maintain-001](../concepts/decisions/maintain-001.md)

## req-maintain-ngt: Ein nächtlicher Build hält den Ocean aktuell

- Status: accepted
- Priority: must
- Statement: Ein nächtlicher Build zieht die Abhängigkeiten jedes Repos des Oceans hoch, Major-Versionen eingeschlossen, und merged das Ergebnis selbst nach main, ohne Review und ohne Veröffentlichung
- Why: [Ein Ticket in Minuten veröffentlichen](../goals/publish-a-ticket-in-minutes.md),
  Thema `maintain`
- Acceptance: Nach einer Nacht ohne Fehler liegt kein Repo des Oceans
  hinter einer veröffentlichten Version einer seiner Abhängigkeiten, und
  der main-Branch jedes hochgezogenen Repos trägt die Änderung, ohne dass
  eine Version veröffentlicht wurde; bricht eine Major-Version
  ein Repo, hält der Build an und sagt dem Entwickler, welches Repo
  gebrochen ist und warum
- Note: akzeptiert am 2026-11-14, siehe
  [maintain-001](../concepts/decisions/maintain-001.md); Merge statt
  Veröffentlichung akzeptiert am 2026-11-15, siehe
  [maintain-002](../concepts/decisions/maintain-002.md)

## req-maintain-dna: Ein nächtlicher Wartungslauf hält die DNA aktuell

- Status: accepted
- Priority: must
- Statement: Ein nächtlicher Wartungslauf hält die DNA jedes Repos aktuell — der Repos von ggsuite und aller anderen Repos des Oceans
- Why: [Ein Ticket in Minuten veröffentlichen](../goals/publish-a-ticket-in-minutes.md)
  — wenn Tickets die DNA nicht mehr aktualisieren
  ([req-dna-chk](dna.md#req-dna-chk-eine-prüfung-belegt-dass-die-generierten-dna-dateien-unverändert-sind)),
  ist die Wartung der einzige Ort, an dem neue DNA ankommt
- Acceptance: Nach einer Nacht ohne Fehler liegen die DNA-Schichten keines
  Repos des Oceans hinter ihrer neuesten veröffentlichten Version, die DNA
  ist neu erzeugt und jedes geänderte Repo unveröffentlicht nach main gemerged
- Note: vom Nutzer am 2026-11-15 vorgegeben. `gg do maintain --upgrade-dna`
  gibt es; `--nightly` zieht nur die Abhängigkeiten hoch
