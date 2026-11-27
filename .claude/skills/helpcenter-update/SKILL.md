---
name: helpcenter-update
description: Hält das Limetax Helpcenter (help.limetax.de, dieses Repo) synchron mit der Limetax App. Prüft Production-Releases aus Linear (Pipeline "Atlas - Production") auf Helpcenter-Relevanz, schreibt Seiten nach AGENTS.md mit Screenshot-Platzhaltern und öffnet einen Pull Request. Ersetzt in einer zweiten Session die Platzhalter durch Screenshots aus dem Testmandanten 45000. Verwenden bei "Release prüfen", "Helpcenter nachziehen", "was ist neu released", "Screenshots einsetzen", "Platzhalter ersetzen", "Seite für TEC-XXXX schreiben" oder wenn eine geplante Routine diesen Skill aufruft.
---

# Helpcenter-Update

Dieser Skill hat drei Modi. Lies zuerst `AGENTS.md` im Repo-Root: Das ist die verbindliche Stilvorgabe für jede Zeile, die du schreibst.

| Modus | Wann | Ergebnis |
| --- | --- | --- |
| **Release** | Täglich per Routine oder auf Zuruf („prüfe die Releases seit …“) | Ein PR pro relevantem Ticket, Zusammenfassung des Laufs |
| **Ticket** | „Schreib die Seite für TEC-XXXX“ oder eine Liste von Seiten zum Nachziehen | Ein PR für genau diese Änderung |
| **Screenshots** | Lora öffnet eine Session und will Platzhalter ersetzen | Bilder im Repo, Platzhalter ersetzt, Commit auf dem PR-Branch |

**Probelauf:** Sagt der Auftrag „Probelauf“ oder „dry run“, führst du alle Schritte bis zur Entscheidung aus, legst aber keinen Branch an und pushst nichts. Du lieferst nur die Zusammenfassung.

## Feste Regeln

- **Nie auf `main` pushen, nie mergen.** Lora reviewt und merged jeden PR selbst.
- **Keine Kanzleinamen und keine Personen im Helpcenter.** Tickets nennen Kanzleien als Label und oft auch in der Beschreibung (Namen, E-Mail-Adressen). Das Repo ist öffentlich, all das bleibt draußen, auch in Commits und PR-Texten.
- **Nur dokumentieren, was live und abgenommen ist.** Grundlage ist ein Release in *Atlas - Production*, nicht Staging. Steht das Ticket trotzdem noch auf einem offenen Status (z. B. „To Test“) oder sagen die Kommentare, dass es auf Production noch nicht getestet ist: nur Zusammenfassung plus Frage an Lora, kein PR.
- **Ticketnummer immer in Branch und Commit.** Branch `helpcenter/tec-XXXX-…`, Commit-Nachricht mit `TEC-XXXX`. Nur so findet der nächste Lauf, was schon dokumentiert ist.
- **Bereiche ohne Seite bleiben ohne Seite.** Aufträge, Lohn, BWA, Angebote und Verträge, Mandantenportal, Nutzerverwaltung und ähnliche Bereiche haben bewusst keine Helpcenter-Seite. Lege dafür keine neue Seite an. Erwähne sie nur in der Zusammenfassung.
- **Gruppe Bank (`bank/`) vorerst nicht ändern.** Dort ändert sich gerade viel. Relevante Tickets nur in der Zusammenfassung aufführen.
- **Keine Passwörter eingeben.** Für Screenshots meldet sich Lora selbst an.
- **Unsicherheit nicht überspielen.** Was du aus Ticket und Code nicht sicher ablesen kannst, kommt als `{/* TODO Lora: … */}`-Kommentar an die Stelle und als Frage in den PR.

## Modus Release

### 1. Releases holen

Über den Linear-Connector:

1. `list_releases` mit `pipeline: "atlas-production"`, `orderBy: "createdAt"` und `createdAt: "-P2D"`. Das Werkzeug filtert nicht nach `completedAt`: Filtere selbst auf `completedAt` im Prüfzeitraum. Standard für die tägliche Routine: die letzten 26 Stunden. Auf Zuruf: der genannte Zeitraum (dann `createdAt` passend weiter fassen).
2. Für jedes Release `list_issues` mit `release: <slugId>` und den Feldern `title`, `labels`, `description`, `project`, `status`.

### 2. Schon erledigt?

Überspringe ein Ticket, wenn eines davon zutrifft, und führe es unter „Übersprungen“ auf:

- `get_issue` mit `fields: ["attachments"]` zeigt schon einen PR in `limetax/docs`. Linear verknüpft PRs automatisch, deren Branch die Ticketnummer enthält.
- Es gibt einen offenen Branch mit der Ticketnummer: `git ls-remote --heads origin "*tec-XXXX*"`.
- Die Ticketnummer steht schon in der Historie des Helpcenters: `git log origin/main -i --grep "tec-XXXX"`. Gemergte Branches sind gelöscht, die Commits bleiben.

### 3. Relevanz entscheiden

Lies Titel, Beschreibung und Kommentare (`list_comments`). Kriterien in `references/relevanz.md`.

Für den Code in `limetax/atlas`: in einem eigenen Klon außerhalb dieses Repos (`git clone --filter=blob:none`), nie im Helpcenter-Repo.

- **Diff:** Gemergte PRs landen als Squash-Commit auf `main`. `git log origin/main -i --grep "tec-XXXX"` findet ihn, `git show <sha>` zeigt die Änderung. Hängen mehrere PRs am Ticket, gilt der gemergte; geschlossene ignorieren.
- **Sichtbare Texte der App** stehen in den i18n-Dateien `apps/web/src/lib/i18n/locales/de/*.ts`. Was Ava im Chat sagt oder in Dateien schreibt, steht in deutschen Strings unter `apps/api/src`.
- **Live oder nicht:** Entscheidend ist, ob eine Route in `apps/web/src/routes` (bzw. eine Seite unter `apps/web/src/pages`) die Komponente einbindet und ob ein Feature-Flag sie abschirmt. Ein Ordnername wie `prototypes/` heißt nicht, dass es nicht live ist.

Ergebnis pro Ticket: **neue Seite**, **Seite ergänzen**, **keine Änderung**, **übersprungen** oder **nur Zusammenfassung** (gesperrter Bereich, Bank, nicht abgenommen, unklar).

### 4. Schreiben

Pro relevantem Ticket ein eigener Branch und ein eigener PR. Mehrere Tickets kommen nur dann in einen PR, wenn sie zusammen **dieselbe sichtbare Änderung** beschreiben (z. B. Backend- und Oberflächen-Ticket derselben Funktion). Gleiches Linear-Projekt allein reicht nicht. Dann stehen alle Ticketnummern im Branch-Namen.

1. Branch von aktuellem `origin/main`: `helpcenter/tec-XXXX-<kurzer-slug>`.
2. Finde die passende Seite: `docs.json` (Navigation) lesen, dann nach Begriffen aus dem Ticket suchen. Lieber eine bestehende Seite ergänzen als eine neue anlegen.
3. **Alle Erwähnungen prüfen.** Ändert das Ticket einen Begriff, eine Spalte, einen Status oder ein Verhalten, such mit `git grep -n -i "<alter Begriff>"` alle Seiten, die ihn nennen, und zieh sie im selben PR nach.
4. Schreibe nach `AGENTS.md`: Du-Ansprache, erster Satz beantwortet die Frage, Fachbegriffe exakt, Klickwege in `<Steps>`, UI-Elemente fett, Menüpfade mit Pfeil.
5. **Begriffe aus der App übernehmen, nicht erfinden.** Sichtbare Texte stehen in `apps/web/src/lib/i18n/locales/de/*.ts`. Such sie dort, statt sie aus dem englischen Tickettitel zu übersetzen.
6. Setze für jedes nötige Bild einen Platzhalter an die Stelle, an der es stehen soll. Neue Bilder kommen nach `AGENTS.md` in Unterordner `images/<gruppe>/`, auch wenn ältere Bilder noch flach unter `images/` liegen:

   ```mdx
   {/* TODO Screenshot: <was zu sehen ist, welche Ansicht, welcher Zustand> -> images/<gruppe>/<dateiname>.png */}
   ```

   Ein Bild pro Schritt, nicht mehr. Dateiname klein, mit Bindestrichen, sprechend.
7. Neue Seite: in `docs.json` in die passende Gruppe eintragen. Umbenannte oder verschobene Seite: Redirect in `docs.json` ergänzen.
8. Prüfe vor dem Commit: `docs.json` ist gültiges JSON (`node -e "require('./docs.json')"`), jede Seite hat `title` und `description`, höchstens zwei Callouts pro Seite.

### 5. PR öffnen

Commit-Nachricht und PR-Text auf Deutsch, Vorlage in `references/pr-vorlage.md`. Push des Branches, dann PR gegen `main`, wenn ein Werkzeug dafür da ist (`gh pr create` oder GitHub-Connector). Sonst den Compare-Link in die Zusammenfassung schreiben: `https://github.com/limetax/docs/compare/main...<branch>`.

### 6. Zusammenfassung

Am Ende jedes Laufs, auch wenn nichts zu tun war:

```
Helpcenter-Lauf <Datum>, Releases <v…> bis <v…> [Probelauf]

PRs geöffnet (im Probelauf: PRs vorgeschlagen):
- TEC-XXXX[, TEC-YYYY] <Titel> -> <PR- oder Compare-Link>, Seiten: <pfade>, <n> Screenshots offen

Übersprungen, schon dokumentiert:
- TEC-XXXX <Titel> – <PR oder Commit>

Nur zur Info (gesperrter Bereich, Bank, nicht abgenommen, unklar):
- TEC-XXXX <Titel> – <Grund>

Keine Helpcenter-Relevanz: <Anzahl> Tickets (TEC-…, TEC-…)

Fragen an Lora:
- …
```

Zähle die Tickets nach: Alle Gruppen zusammen ergeben die Zahl der Tickets in den Releases.

## Modus Ticket

Wie Modus Release ab Schritt 2, nur für die genannten Tickets oder Seiten. Bei „Seite X nachziehen“ ohne Ticket: Suche in Linear die abgeschlossenen Tickets zum Thema (`list_issues` mit `query`, `state: "Done"`) und prüfe über `get_issue` mit `includeReleases`, dass sie in *Atlas - Production* released sind.

## Modus Screenshots

Ablauf und Konventionen in `references/screenshots.md`. Kurz:

1. Offene Platzhalter finden: `git grep -n "TODO Screenshot"` auf dem PR-Branch, den Lora nennt, oder auf allen offenen `helpcenter/*`-Branches. Ältere Platzhalter haben keinen Zielpfad (`-> images/…`). Dann legst du den Pfad selbst fest: `images/<ordner der seite>/<sprechender-name>.png`.
2. Lora meldet sich im Browser auf `https://app.limetax.de` an. Du gibst keine Zugangsdaten ein.
3. Nur im Testmandanten 45000 (Limetax GmbH) arbeiten. Dort darf alles ausgelöst werden.
4. Pro Platzhalter: Ansicht herstellen, Screenshot, Bild ansehen und gegen den Platzhaltertext prüfen, unter dem genannten Pfad speichern.
5. Platzhalter ersetzen:

   ```mdx
   <Frame caption="<kurze Bildunterschrift>">
     ![<Alt-Text>](/images/<gruppe>/<datei>.png "<Alt-Text>")
   </Frame>
   ```

6. Commit auf den PR-Branch, push. Dann die Liste der eingesetzten Bilder mit allem, was Lora sich ansehen sollte (verdeckte Elemente, sichtbare Daten, unscharfe Schrift).

## Vor jedem Schreiben prüfen

Branches werden nach dem Merge gelöscht, und Lora merged oft zwischendurch. Bevor du auf einem bestehenden Branch weiterarbeitest: `git fetch --prune` und prüfen, ob der Branch noch existiert und ob sein PR schon gemergt ist (`git branch -r --contains <commit>` mit `origin/main`). Ist er gemergt, neuen Branch von `main` anlegen und Lora darauf hinweisen.
