# Limetax Helpcenter — Projektanweisungen

Diese Datei ist die verbindliche Stilvorgabe für alle, die am Limetax Helpcenter schreiben — Menschen wie KI-Assistenten. Der Mintlify-Editor und angebundene Agenten lesen sie automatisch.

## Über dieses Projekt

- Dokumentationsseite auf Basis von [Mintlify](https://mintlify.com)
- Seiten sind MDX-Dateien mit YAML-Frontmatter
- Konfiguration liegt in `docs.json`
- Zusätzliches Styling liegt in `limetax.css` (wird automatisch auf allen Seiten geladen)
- Sprache: **Deutsch**. Keine englischen Seiten, keine Übersetzungen.

## Zielgruppe

Ausschließlich **Kanzleien**: Steuerberater:innen, Steuerfachangestellte und Kanzleimitarbeitende, die mit der Limetax App arbeiten. **Keine Mandanten, keine Endverbraucher.**

Konsequenz: Fachsprache wird vorausgesetzt. Begriffe wie Kontierung, Festschreibung, Buchungsstapel, Sachkonto, SKR03/SKR04, UStVA oder Buchungsdatenservice werden **nicht erklärt und nicht umschrieben** — die Zielgruppe kennt sie, Vereinfachung wirkt herablassend.

## Ansprache und Ton

- **Du-Ansprache**, durchgehend. „Klicke auf **Speichern**." Nie „Sie", nie unpersönliche Passivkonstruktionen.
- **Locker in der Anrede, exakt beim Fachbegriff.** Richtig: „Du findest den Buchungsstapel unter…". Falsch: „Du findest deine Buchungen unter…".
- **Direkt und substanziell.** Kein Marketing-Ton, keine Füllwörter, keine Einleitungen über die Wichtigkeit von Buchhaltung.
- **Der erste Satz beantwortet die Frage.** Kein Aufwärmen.
- Aktiv statt passiv. Ein Gedanke pro Satz.

## Terminologie

Verbindliche Schreibweisen:

| Richtig | Nicht |
| --- | --- |
| Mandant / Mandantin | Kunde, Klient |
| Kanzlei | Firma, Unternehmen (wenn die Kanzlei gemeint ist) |
| Kontierung, kontieren | Verbuchung im Sinne von Kontenzuordnung |
| Buchungsstapel | Stapel, Batch |
| Festschreibung, festschreiben | Sperren, finalisieren |
| Sachkonto | Konto (wenn das Sachkonto gemeint ist) |
| Beleg | Dokument (wenn ein Buchungsbeleg gemeint ist) |
| DATEV Unternehmen online | DUO (nicht als Erstnennung) |
| Buchungsdatenservice | BDS (nicht als Erstnennung) |
| Limetax App | die App, das Tool, die Plattform |
| KI-Assistent | Bot, AI, die KI |

Abkürzungen bei der ersten Nennung pro Artikel ausschreiben, danach zulässig.

## Titel

Der Titel ist das, was jemand ins Suchfeld tippen würde — nicht der Name eines Features.

- Handlungsorientiert: „Duplikate erkennen und auflösen", nicht „Duplikatserkennung"
- Fehlermeldungen **wörtlich** in den Titel: „Microsoft-Login: Administratorgenehmigung erforderlich"
- Konkrete Sonderfälle benennen: „Falscher deutscher USt-Ausweis bei Auslandseinkäufen (EU & Drittland)"
- Keine Präfixe wie „Export – …". Die Gruppierung übernimmt die Navigation.
- Sentence case, keine durchgängige Großschreibung

## Aufbau eines Artikels

Ein Artikel behandelt **eine** Aufgabe. Zielgröße 300–600 Wörter. Lieber drei kurze Seiten als eine Sammelseite.

Es gibt genau vier Muster:

**A – Übersichtsseite:** Kurzer Absatz „Was du hier findest" → `<Columns>` mit `<Card>` → optional `<Note>` mit Support-Verweis.

**B – Anleitung (Regelfall):** Ein Satz Zweck → Voraussetzungen → `<Steps>` mit Screenshots → `<Check>` als Erfolgskriterium → verwandte Artikel als Cards.

**C – Konzept:** Was es ist → warum es relevant ist → wie es funktioniert → Grenzen und Sonderfälle in `<AccordionGroup>`.

**D – Troubleshooting:** Symptom als Überschrift → `<AccordionGroup>` mit „Ursache / Lösung" → Eskalationspfad zum Support.

## Komponenten

- **Jede Anleitung gehört in `<Steps>`.** Nummerierte Listen sind für Klickwege verboten.
- **Maximal zwei Callouts pro Seite.** Wenn alles hervorgehoben ist, ist nichts hervorgehoben.
- `<Danger>` **ausschließlich** bei irreversiblen Vorgängen oder echten steuerlichen bzw. fristlichen Risiken (z. B. Festschreibung, Fristversäumnis). Nie als Aufmerksamkeitsmittel.
- `<Card>` ist ein Navigationselement. Eine Card ohne `href` ist ein Fehler.
- `<Tabs>` nur bei echten Varianten (Web-App vs. Mobile App), nicht als Gliederungsersatz.
- **Jeder Screenshot steht in einem `<Frame>`** mit `caption` und `alt`.
- Wiederkehrende Textbausteine (Support-Kontakt, Hinweise zu DATEV-Voraussetzungen) als Snippet unter `/snippets/`, nicht kopieren.

## Frontmatter

Jede Seite braucht `title` und `description`. Die `description` ist ein vollständiger Satz mit Punkt — sie erscheint in der Suche, bei Google und auf Kacheln.

```mdx
---
title: "Duplikate erkennen und auflösen"
description: "So findest du doppelt erfasste Belege in Limetax und entscheidest, welcher gebucht wird."
icon: "copy"
---
```

`icon` nur setzen, wenn alle Seiten einer Gruppe eins bekommen.

## Formatierung

- UI-Elemente fett: „Klicke auf **Speichern**."
- Menüpfade mit Pfeil: **Einstellungen → Kanzlei → Nutzer**
- Code-Formatierung für Dateinamen, Pfade, Befehle, Feldnamen
- Überschriften in Sentence case

## Screenshots

- Heller Modus, Standard-Zoom
- **Niemals echte Mandantendaten.** Testmandanten oder anonymisierte Daten.
- Ein Screenshot pro Step, nicht drei. Bilder ersetzen keinen Text, sie bestätigen ihn.
- Ablage unter `/images/<gruppe>/<dateiname>.png`

## Design

Die visuelle Identität kommt aus `docs.json` und `limetax.css` — nicht aus einzelnen Seiten.

- **Keine Inline-Styles, keine `style`-Props.** Anpassungen gehören in `limetax.css`.
- Tailwind-Arbitrary-Values werden von Mintlify nicht unterstützt.
- Limetax-Blau `#436fff` ist **Akzentfarbe**, nie Fläche. Keine bunten Boxen als Gestaltungselement.
- Keine abgerundeten Ecken — das ist eine harte Markenregel und in `limetax.css` global gesetzt.
- Weißraum vor Dekoration.

## Inhaltliche Grenzen

- **Keine internen Prozesse** dokumentieren (Limetax-interne Abläufe, Team-Onboarding, Roadmap).
- **Keine steuerliche Beratung.** Das Helpcenter erklärt die Bedienung der Limetax App, nicht die Rechtslage. Wo eine steuerliche Bewertung nötig ist, auf die Verantwortung der Kanzlei verweisen.
- **Keine Preise, Vertragsdetails oder Rabatte** — die ändern sich und gehören auf limetax.de.
- **Keine unveröffentlichten Features.** Nur dokumentieren, was live ist.
- Bei Aussagen zur KI-Verarbeitung: keine Versprechen zu Genauigkeit oder Trefferquoten. Beschreiben, was das System tut und wo die Kanzlei prüfen muss.

## Beim Umbenennen oder Verschieben von Seiten

Immer einen Redirect in `docs.json` ergänzen. Support-Mitarbeitende und Kanzleien verlinken Artikel direkt — tote Links kosten Vertrauen.