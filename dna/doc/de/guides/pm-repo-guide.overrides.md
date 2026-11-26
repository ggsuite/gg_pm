## @write-requirements Anforderungen schreiben <a id="write-the-requirements"></a>

- Anforderungen nach Produktbereich gruppieren, eine Datei pro Bereich:
  `pm/<lang>/<quarter>/requirements/<area>.md`, Bereich auf Englisch in
  Kebab-Case
- Jeder Anforderung eine ID `req-<area>-<abc>` geben: `<abc>` ist ein Code
  aus drei Kleinbuchstaben, der die Anforderung zusammenfasst, z. B.
  `req-results-lst` für die Ergebnisliste. Der Code ist innerhalb seines
  Bereichs über alle Quartale eindeutig; das Präfix hält ihn von
  Entscheidungs-IDs getrennt
- Nie eine Nummer in eine Anforderungs-ID schreiben: Anforderungen werden
  umsortiert, ohne neu zu nummerieren. Eine ID nie wiederverwenden oder
  umbenennen
- Mehrere Anforderungen eines Bereichs über die erste vollständige ID und
  die Codes der übrigen angeben: `req-results-lst, imp, exp`
- Jede Anforderung als eigenen Abschnitt schreiben:

```markdown
## req-results-lst: Result list right after the race

- Status: accepted
- Priority: must
- Statement: The result list is ready two seconds after the last finisher
- Why: [results without desktop software](../goals/results-without-desktop-software.md),
  topic `timing`
- Acceptance: a race with 500 finishers shows the list within two seconds
```

- `Status` — `proposed`, `accepted`, `done` oder `dropped`
- `Priority` — `must`, `should` oder `could`; was gar nicht gewollt ist,
  ist `dropped`
- `Statement` — ein Satz dazu, was das Produkt tun oder sein muss, nie wie
- `Why` — das Ziel, dem sie dient, und das Thema, aus dem sie stammt
- `Acceptance` — die Prüfungen, die sie belegen; bei Bedarf ein
  Aufzählungspunkt pro Prüfung
- Eine Anforderung an Ort und Stelle ändern und angeben, was sich wann
  geändert hat; eine ersetzte Anforderung wird auf `dropped` gesetzt und
  verlinkt ihre Nachfolgerin
- Eine kaputte `done`-Anforderung ist ein Bug, keine neue Anforderung
