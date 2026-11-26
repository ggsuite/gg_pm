# publish-001: Ein Publish analysiert statt zu testen und schreibt trotzdem den Hash der Prüfungen

- Status: accepted
- Date: 2026-11-14
- Canonical source: diese Datei
- Open work: keine — umgesetzt mit dem Ticket `lean_publish`

## Entscheidung

Bevor ein Repo veröffentlicht wird, führt gg nur `dart pub get` und
`dart analyze` aus; das vollständige `can commit` mit seinen Tests
entfällt. Die Tests wurden beim Commit bestanden, und die veröffentlichten
Versionen der Geschwister-Repos sind genau die Commits, die über lokale
Refs getestet wurden; ein zweiter Lauf belegt also nichts Neues und kostet
den größten Teil der Zeit eines Publish. Auch der Quick Check auf GitHub
lässt keine Tests laufen: Er prüft nur, dass der Commit mit gg gemacht
wurde, über den Hash, den `can commit` schreibt. Deshalb muss der Publish
diesen Hash für den Commit, den er macht, weiterhin schreiben, sonst
schlägt der Quick Check fehl.
