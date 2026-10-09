# Aktueller Projektstand

## Projekt

World Soul – Music Manager (Website): statische, viersprachige Website (ES/EN/DE/FR) mit Hell- und Dunkelmodus unter `world-soul/`. Status: aktiv, Roadmap v2. Veröffentlicht unter https://world-soul.onrender.com. Fortschritt: 87,5 % (14 von 16 Gewichtspunkten, 6 von 8 Tasks).

## Aktive Phase

phase-3 – Feinschliff (phase-1 und phase-2 abgeschlossen).

## Aktive Aufgabe

task-3-1 – Favicon für die World-Soul-Website ergänzen (seit 2026-10-09T14:25:45Z). Vorgehen: Entwürfe A/B/C zur Auswahl durch den Teilnehmer, danach favicon.ico (16/32/48) und apple-touch-icon (180×180) unter world-soul/, Einbindung in Quelle und Bundles, lokale und Live-Prüfung.

## Zuletzt abgeschlossen

- task-2-1 – Website als Render Static Site veröffentlicht: https://world-soul.onrender.com; Datenschutzerklärung nennt Render (2026-10-09).
- task-2-4 – Performance: index.html 2.284.630 → 394.320 Bytes (−83 %); Fotos als Graustufen-WebP aus assets/ mit Lazy Loading, Logo verkleinert, ungenutzte Originale entfernt (2026-10-09).
- task-2-3 – Barrierefreiheit: Dokumenttitel, Fokus-Rückgabe nach Esc, sofort sichtbarer Fokus, zugängliche Formular-Fehler, Hinweis auf neuen Tab; axe-core 0 Verstöße, Narrator-Test bestanden (2026-10-09).
- task-2-2 – Responsive-Prüfung bei Smartphone-Breite: kompakter Mobil-Header, Sprachwahl im mobilen Menü, lesbare Routen-Beschriftungen; auf echtem Smartphone bestätigt (2026-10-09).
- task-1-2 – Kontrast und Hover-Zustände im Hell-/Dunkelmodus verbessert (Commit 9925dba, PR #1 in main gemergt, 2026-10-08).
- task-1-1 – World-Soul-Website nach `world-soul/` übernommen (Commit 57d4e72, 2026-10-08).

## Bereite nächste Aufgaben

- task-3-2 – Vorschaubild für soziale Netzwerke (og:image) mit absoluter URL

## Blockiert

Nichts.

## Wichtige Entscheidungen

- Hosting: Render Static Site (Branch `main`, Publish Directory `world-soul`); jeder Merge nach `main` wird automatisch veröffentlicht.
- Arbeit am Projekt findet ausschließlich unter `world-soul/` statt; Workshop-Struktur bleibt erhalten.
- `World Soul.dc.html` ist die Quelle; jede Änderung wird zusätzlich in das eingebettete Template von `index.html` und `world-soul-index.html` übernommen (siehe `docs/decisions.md`).
- Fotos liegen als Graustufen-WebP in `assets/` und werden nicht mehr eingebettet; `index.html` benötigt `assets/` daneben. Farb-Originale nur noch in der Git-Historie (z. B. Commit 57d4e72).
- Boolesche/camelCase-Attribute (z. B. `noValidate`, `onClick`) in der Quelle immer camelCase schreiben; die Template-Engine verwirft kleingeschriebene Varianten.
- Bis 520 px Breite: Sprachwahl im mobilen Menü, Farbmodus-Schalter als Icon-Button (44×44).
- Neue Farb-Tokens `--control-line` und `--tile-bg`/`--tile-fg` für Bedienelement-Rahmen und bildlose Kacheln.

## Bekannte Probleme

- Die frühere Seite https://jegucab.github.io/WorldSoul/ (Repository jegucab/WorldSoul) bleibt unverändert.
- Kein Build-Werkzeug für das Bundle im Repository vorhanden.
- Die Seite hat kein Favicon (Browser fordern /favicon.ico an und erhalten 404; geplant: task-3-1).
- `og:image` verwendet einen relativen Pfad (`assets/logo-ws-alpha.png`); soziale Netzwerke erwarten meist eine absolute URL (geplant: task-3-2).

## Empfohlener nächster Schritt

Änderungen synchronisieren; danach task-3-1 (Favicon).
