# Aktueller Projektstand

## Projekt

World Soul – Music Manager (Website): statische, viersprachige Website (ES/EN/DE/FR) mit Hell- und Dunkelmodus unter `world-soul/`. Status: aktiv, Roadmap v1. Fortschritt: 78,57 % (11 von 14 Gewichtspunkten, 5 von 6 Tasks).

## Aktive Phase

phase-2 – Qualität und Veröffentlichung.

## Aktive Aufgabe

task-2-1 – world-soul/ als statische Website auf Render veröffentlichen (seit 2026-10-09T13:58:39Z; zuvor blockiert, da GitHub Pages nicht aktivierbar). Vorgehen: Render Static Site mit Branch `main`, Publish Directory `world-soul`, ohne Build; Datenschutzerklärung auf den neuen Hosting-Anbieter anpassen.

## Zuletzt abgeschlossen

- task-2-4 – Performance: index.html 2.284.630 → 394.320 Bytes (−83 %); Fotos als Graustufen-WebP aus assets/ mit Lazy Loading, Logo verkleinert, ungenutzte Originale entfernt (2026-10-09).
- task-2-3 – Barrierefreiheit: Dokumenttitel, Fokus-Rückgabe nach Esc, sofort sichtbarer Fokus, zugängliche Formular-Fehler, Hinweis auf neuen Tab; axe-core 0 Verstöße, Narrator-Test bestanden (2026-10-09).
- task-2-2 – Responsive-Prüfung bei Smartphone-Breite: kompakter Mobil-Header, Sprachwahl im mobilen Menü, lesbare Routen-Beschriftungen; auf echtem Smartphone bestätigt (2026-10-09).
- task-1-2 – Kontrast und Hover-Zustände im Hell-/Dunkelmodus verbessert (Commit 9925dba, PR #1 in main gemergt, 2026-10-08).
- task-1-1 – World-Soul-Website nach `world-soul/` übernommen (Commit 57d4e72, 2026-10-08).

## Bereite nächste Aufgaben

Keine.

## Blockiert

Nichts.

## Wichtige Entscheidungen

- Arbeit am Projekt findet ausschließlich unter `world-soul/` statt; Workshop-Struktur bleibt erhalten.
- `World Soul.dc.html` ist die Quelle; jede Änderung wird zusätzlich in das eingebettete Template von `index.html` und `world-soul-index.html` übernommen (siehe `docs/decisions.md`).
- Fotos liegen als Graustufen-WebP in `assets/` und werden nicht mehr eingebettet; `index.html` benötigt `assets/` daneben. Farb-Originale nur noch in der Git-Historie (z. B. Commit 57d4e72).
- Boolesche/camelCase-Attribute (z. B. `noValidate`, `onClick`) in der Quelle immer camelCase schreiben; die Template-Engine verwirft kleingeschriebene Varianten.
- Bis 520 px Breite: Sprachwahl im mobilen Menü, Farbmodus-Schalter als Icon-Button (44×44).
- Neue Farb-Tokens `--control-line` und `--tile-bg`/`--tile-fg` für Bedienelement-Rahmen und bildlose Kacheln.

## Bekannte Probleme

- Veröffentlicht unter https://world-soul.onrender.com (Render). Die Datenschutzerklärung mit Render als Hosting-Anbieter ist lokal angepasst und erscheint dort erst nach dem Merge nach `main`. Die frühere Seite https://jegucab.github.io/WorldSoul/ (Repository jegucab/WorldSoul) bleibt unverändert.
- Kein Build-Werkzeug für das Bundle im Repository vorhanden.
- Die Seite hat kein Favicon (Browser fordern /favicon.ico an und erhalten 404).
- `og:image` verwendet einen relativen Pfad (`assets/logo-ws-alpha.png`); soziale Netzwerke erwarten meist eine absolute URL.

## Empfohlener nächster Schritt

Änderungen (Datenschutzerklärung, Dokumentation) committen, pushen und nach `main` mergen; nach dem automatischen Render-Deployment die Datenschutzerklärung auf https://world-soul.onrender.com prüfen und task-2-1 abschließen.
