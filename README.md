# Limetax Helpcenter

Öffentliche Hilfe- und Anleitungssammlung zur Limetax App. Zielgruppe sind Steuerkanzleien: Steuerberater:innen und Steuerfachangestellte. Ansprache: Du.

Verbindliche Stilvorgaben stehen in [AGENTS.md](./AGENTS.md).

## Struktur

- `index.mdx` — Startseite
- `changelog.mdx` — Was neu in Limetax ist
- `erste-schritte/`, `belege/`, `kontierung/`, `bank/`, `bescheidpruefung/`, `chat/`, `agenten/`, `datev/`, `verwaltung/`, `sicherheit/`, `fehler/` — Themengruppen
- `docs.json` — Navigation, Farben, Logo, Theme, Redirects
- `limetax.css` — Feinschliff (wird von Mintlify automatisch geladen; muss separat ins Repo, siehe unten)
- `logo/`, `favicon.svg` — Assets (siehe unten)

## Live-Vorschau

- Editor: [app.mintlify.com/limetax/limetax](https://app.mintlify.com/limetax/limetax)
- Vorschau: [limetax.mintlify.app](https://limetax.mintlify.app)

## Arbeiten

1. Branch im Web-Editor anlegen.
2. Muster und Bausteine aus AGENTS.md verwenden.
3. Vorschau prüfen.
4. Pull Request, Review, Merge.
5. Bei Rename immer Redirect in `docs.json` ergänzen.

## Assets, die nicht über den Editor gepflegt werden

Der Mintlify-Editor kann keine Binär- und `.css`-Dateien anlegen. Folgende Dateien werden direkt per Git committet:

- `logo/light.svg`, `logo/dark.svg` — Limetax-Logo (aktuell noch Mintlify-Platzhalter)
- `favicon.svg` — Limetax-Favicon (aktuell noch Mintlify-Platzhalter)
- `limetax.css` — Feinschliff: keine abgerundeten Ecken, neutraler Hintergrund `#f7f7f7`, Blau nur als Akzent, Tabellen-Kopf, Codeblock-Styling

Die CSS-Datei wird von Mintlify automatisch auf allen Seiten geladen, sobald sie im Content-Verzeichnis liegt. Kein Import in `docs.json` oder MDX nötig.

## Support

Fragen und Feedback: [kontakt@limetax.de](mailto:kontakt@limetax.de)