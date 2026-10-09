# Architektur

## Überblick

Die World-Soul-Website ist eine statische Single-Page-Website unter `world-soul/`. Es gibt kein Backend; das Kontaktformular sendet an Formspree.

## Dateien

| Pfad | Zweck |
| --- | --- |
| `world-soul/World Soul.dc.html` | Bearbeitbare Quelle: Markup, CSS-Tokens, Texte in vier Sprachen und Komponentenlogik |
| `world-soul/support.js` | Laufzeit für das `x-dc`-Format der Quelle |
| `world-soul/doc-page.js` | Hilfsskript der Quelle |
| `world-soul/_ds/modernist-…/` | Designsystem „Modernist“ (Tokens, Komponenten, Schrift Archivo) |
| `world-soul/assets/` | Logos und Fotos |
| `world-soul/index.html` | Ausgelieferte Seite: Single-File-Bundle |
| `world-soul/world-soul-index.html` | Byte-identische Kopie von `index.html` |

## Bundle-Aufbau

`index.html` enthält mehrere `<script type="__bundler/…">`-Blöcke:

- `manifest`: eingebettete Assets (Bilder, Schriften, Skripte) als Base64, über UUIDs referenziert
- `template`: die komplette Quelle als JSON-String; Asset-Pfade sind durch UUIDs ersetzt, camelCase-Attribute kodiert (z. B. `onClick` → `sc-camel-on-click`)
- `ext_resources`: externe Skripte (React/ReactDOM 18.3.1 von unpkg)

Das Template lässt sich byte-genau mit `json.dumps(…, ensure_ascii=False)` und anschließendem Ersetzen von `</` durch `</` wieder kodieren.

## Farbmodi

Farben sind als CSS-Custom-Properties auf `:root` definiert und unter `[data-theme="dark"]` überschrieben. Der Modus wird beim Start aus `localStorage` (`ws-theme`) oder `prefers-color-scheme` gewählt; `applyTheme` setzt `data-theme` und die `theme-color`.

Wichtige Tokens: `--bg`, `--surface`, `--text`, `--muted`, `--brand`, `--accent`, `--accent-text`, `--line` (Abschnittslinien), `--hair` (feine Trennlinien), `--control-line` (Rahmen von Bedienelementen), `--btn-bg`/`--btn-fg`, `--tile-bg`/`--tile-fg`.

Hover-Zustände sind als Klassen (`ws-nav-link`, `ws-btn`, `ws-ctl`, `ws-lang`, `ws-card`) mit `!important` umgesetzt, weil die Elemente Inline-Styles tragen.

## Responsives Verhalten

- Ab 960 px: Desktop-Navigation im Header, kein Menü-Button.
- 521–959 px: Menü-Button, Sprachwahl und Farbmodus-Schalter mit Beschriftung im Header.
- Bis 520 px: Header nur mit Logo, Farbmodus-Icon (`[data-theme-toggle]`) und Menü-Button; die Sprachwahl (`[data-header-langs]`) ist ausgeblendet und erscheint als `.ws-menu-langs` im mobilen Menü. Die Routen-Grafik (`.ws-route`) vergrößert ihre Beschriftungen und verschiebt die Städtenamen (`.ws-route-city`) unter die Linie.

## Barrierefreiheit

- `document.title` wird in `applyLang` aus `T[lang].docTitle` gesetzt; `lang` am `<html>` folgt der Sprache, der Rechtsbereich ist `lang="de"`.
- Skip-Link „Zum Inhalt“ als erstes fokussierbares Element; Fokusrahmen über `:focus-visible` in `--accent` (ohne Transition).
- Mobiles Menü: `aria-expanded`/`aria-controls` am Menü-Button; Esc schließt das Menü und setzt den Fokus zurück auf den Button.
- Kontaktformular mit `noValidate`, eigener Validierung, `aria-invalid` am fehlerhaften Feld und `aria-describedby="ws-form-status"`.
- Social-Links mit `target="_blank"` kündigen das Öffnen in neuem Tab im zugänglichen Namen an (`T[lang].a11y.newTab`).
- Prüfung: axe-core 4.10.2 in allen Sprachen und Farbmodi ohne Verstöße (Stand 2026-10-09).

