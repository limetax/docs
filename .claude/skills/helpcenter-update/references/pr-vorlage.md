# Commit und PR

## Commit-Nachricht

```
<Seite oder Thema>: <was sich ändert>

<1–3 Sätze, warum. Ticketnummer(n).>
```

Beispiel: `Arbeitsordner: DMS-Status ändern und Notiz ergänzen` mit dem Satz „Ava kann seit v2.0.48 den Status eines DMS-Dokuments ändern (TEC-3215).“

## PR-Titel

Wie die erste Zeile der Commit-Nachricht, dazu die Ticketnummer: `Arbeitsordner: DMS-Status ändern (TEC-3215)`.

## PR-Text

```markdown
## Was sich in der App geändert hat

<2–4 Sätze aus Sicht der Kanzlei. Release-Version und Ticket-Links.>

## Was im Helpcenter geändert wurde

- `<pfad/seite.mdx>`: <neu / ergänzt / umformuliert>, <was genau>
- `docs.json`: <Navigation / Redirect>, falls geändert

## Offene Screenshots

- [ ] `images/<gruppe>/<datei>.png`: <was zu sehen sein soll>

## Fragen an Lora

- <was aus Ticket und Code nicht sicher ablesbar war>

Quellen: <Linear-Ticket-Links>, <PR-Links in limetax/atlas>
```

Keine Kanzleinamen, auch wenn sie im Ticket stehen.
