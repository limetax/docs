# Wann ein Ticket ins Helpcenter gehört

Leitfrage: **Sieht oder bedient eine Kanzlei nach diesem Release etwas anders in der Limetax App?** Wenn ja, ist es relevant.

## Relevant

- Neue Funktion, neuer Button, neuer Menüpunkt, neue Einstellung, die Kanzleien nutzen.
- Geänderter Ablauf: andere Reihenfolge, anderer Klickweg, umbenannte Elemente, neue Status.
- Neue Fähigkeit von Ava im Chat, die Kanzleien gezielt nutzen können (z. B. „Ava kann jetzt X in DATEV schreiben“).
- Neue Grenze oder geändertes Verhalten, das zu Rückfragen führt (z. B. „nur Belege mit Status Y werden importiert“).
- Ein Bug-Fix, der ein bisher dokumentiertes Verhalten oder einen dokumentierten Workaround ändert. Dann den Workaround von der Seite entfernen.

## Nicht relevant

- Interne Technik: Refactoring, Migrationen, Monitoring, Analytics (PostHog), Feature-Flags, Tests, Sicherheitsupdates ohne sichtbare Änderung.
- Werkzeuge nur für Limetax-Mitarbeitende (HQ, Admin-Oberflächen für das eigene Team).
- Bug-Fixes, die nur das dokumentierte Sollverhalten wiederherstellen.
- Funktionen hinter einem Feature-Flag für einzelne Kanzleien. Hinweise: Ticket erwähnt „flag“, „gate“, „behind“, „selected advisories“, oder der Code prüft ein Flag.

## Nur in die Zusammenfassung

- Bereiche ohne Helpcenter-Seite (bewusst so entschieden): Aufträge, Lohn, BWA, Angebote und Verträge, Dokumentübersetzung, PDF-Tabellen, Meldungen, Mandantenportal, Nutzerverwaltung.
- Alles in der Gruppe Bank (`bank/`), bis Lora die Sperre aufhebt.
- Fälle, in denen du nicht sicher entscheiden kannst. Schreib dazu, was dir fehlt.

## Hinweise zum Lesen der Tickets

- Titel mit `[Idee]`, `[Fehler]`, `[Support]` stammen meist aus Kanzlei-Feedback. Die eigentliche Lösung steht oft erst in den Kommentaren oder im verlinkten PR.
- Englische Tickettitel beschreiben die Technik. Die Begriffe in der App sind Deutsch: im Code von `limetax/atlas` nachsehen.
- Mehrere Tickets eines Linear-Projekts gehören manchmal zu einer Funktion. Nur wenn sie dieselbe sichtbare Änderung beschreiben: eine Seite, ein PR. Jedes Ticket trotzdem einzeln auf Relevanz prüfen.
- Status und Kommentare lesen: Ein Ticket kann in einem Production-Release stecken und trotzdem noch auf „To Test“ stehen. Dann nicht dokumentieren, sondern Lora fragen.
