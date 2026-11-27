# Screenshots aufnehmen

## Umgebung

- App: `https://app.limetax.de` (Production).
- **Nur Testmandant 45000 (Limetax GmbH).** Dort darf alles ausgelöst werden: Belege freigeben, aufteilen, archivieren, Stapel übertragen.
- Lora meldet sich selbst an, im eingebauten Browser der Claude-App oder in ihrem Chrome. Du gibst keine Zugangsdaten ein. Siehst du eine Anmeldeseite, sag Lora Bescheid und warte.

## Konventionen

| Punkt | Vorgabe |
| --- | --- |
| Modus | Heller Modus, Standard-Zoom |
| Fenster | Breite etwa 1280–1440 px, damit Schrift im Helpcenter lesbar bleibt |
| Ausschnitt | Nur der Bereich, um den es geht. Ganze Seiten nur, wenn die Orientierung wichtig ist |
| Ablage | `images/<gruppe>/<dateiname>.png`, Gruppe = Ordner der Seite (`rechnungen`, `belege`, `chat`, `export`, `stammdaten`, `skills`) |
| Dateiname | klein, Bindestriche, sprechend: `arbeitsordner-dms-status.png` |
| Pro Schritt | ein Bild, nicht mehr |

## Vor dem Speichern prüfen

Sieh dir jedes Bild an, bevor du es einsetzt:

- Zeigt es genau das, was der Platzhalter beschreibt?
- **Mauszeiger, Tooltips, Overlays:** Das runde Icon unten rechts in der App verdeckt oft Buttons. Ausblenden oder den Ausschnitt so wählen, dass nichts Wichtiges verdeckt ist.
- **Daten:** Nur Testmandant 45000. Keine anderen Mandantennamen, keine echten Personen in Chat-Verläufen, keine E-Mail-Adressen außer Test-Adressen.
- **Lesbarkeit:** Ist die Schrift bei 672 px Breite (Helpcenter-Spalte) noch lesbar? Sehr breite Aufnahmen zuschneiden.

## Aufnehmen

Je nach verfügbarem Browser-Werkzeug:

1. **Browser-Werkzeug mit Screenshot-Datei** (z. B. Claude in Chrome): Aufnahme machen, die gespeicherte Datei sofort aus dem Temp-Ordner ins Repo kopieren. Temp-Ordner werden aufgeräumt.
2. **Lora liefert die Bilder** (Einfügen in den Chat, Slack): Die eingefügten Dateien liegen im Temp-Ordner der Session. Sofort ins Repo kopieren, nach Inhalt zuordnen und die Zuordnung in der Antwort auflisten.

Bilder aus Slack-DMs sind schwer zu holen: Der Slack-Connector liefert sie nur als Base64. Lieber direkt einfügen lassen.

## Platzhalter ersetzen

```mdx
<Frame caption="<kurze Bildunterschrift, beschreibt den Zweck>">
  ![<Alt-Text: was zu sehen ist, mit den sichtbaren UI-Begriffen>](/images/<gruppe>/<datei>.png "<Alt-Text>")
</Frame>
```

Danach `git grep -n "TODO Screenshot"`, um sicherzugehen, dass keiner übrig ist, oder die übrigen in der Antwort nennen.
