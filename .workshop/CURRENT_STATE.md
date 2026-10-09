# Aktueller Projektstand

## Projekt

World Soul – Music Manager (Website): statische, viersprachige Website (ES/EN/DE/FR) mit Hell- und Dunkelmodus unter `world-soul/`. Status: aktiv, Roadmap v1. Fortschritt: 78,57 % (11 von 14 Gewichtspunkten, 5 von 6 Tasks).

## Aktive Phase

phase-2 – Qualität und Veröffentlichung (alle Tasks bis auf das blockierte task-2-1 abgeschlossen).

## Aktive Aufgabe

Keine.

## Zuletzt abgeschlossen

- task-2-4 – Performance: index.html 2.284.630 → 394.320 Bytes (−83 %); Fotos als Graustufen-WebP aus assets/ mit Lazy Loading, Logo verkleinert, ungenutzte Originale entfernt (2026-10-09).
- task-2-3 – Barrierefreiheit: Dokumenttitel, Fokus-Rückgabe nach Esc, sofort sichtbarer Fokus, zugängliche Formular-Fehler, Hinweis auf neuen Tab; axe-core 0 Verstöße, Narrator-Test bestanden (2026-10-09).
- task-2-2 – Responsive-Prüfung bei Smartphone-Breite: kompakter Mobil-Header, Sprachwahl im mobilen Menü, lesbare Routen-Beschriftungen; auf echtem Smartphone bestätigt (2026-10-09).
- task-1-2 – Kontrast und Hover-Zustände im Hell-/Dunkelmodus verbessert (Commit 9925dba, PR #1 in main gemergt, 2026-10-08).
- task-1-1 – World-Soul-Website nach `world-soul/` übernommen (Commit 57d4e72, 2026-10-08).

## Bereite nächste Aufgaben

Keine.

## Blockiert

- task-2-1 – world-soul/ über GitHub Pages veröffentlichen: GitHub Pages lässt sich nicht aktivieren: github.com/Futureway-Akademie/J.Aragons_Project/settings/pages liefert 404 für das Teilnehmerkonto (fehlende Admin-Rechte am Repository oder Pages in der Organisation Futureway-Akademie deaktiviert). Benötigt Freigabe durch einen Organisations-Owner. Nach Freigabe: Settings → Pages → Deploy from a branch → main, / (root); erwartete URL https://futureway-akademie.github.io/J.Aragons_Project/world-soul/.

## Wichtige Entscheidungen

- Arbeit am Projekt findet ausschließlich unter `world-soul/` statt; Workshop-Struktur bleibt erhalten.
- `World Soul.dc.html` ist die Quelle; jede Änderung wird zusätzlich in das eingebettete Template von `index.html` und `world-soul-index.html` übernommen (siehe `docs/decisions.md`).
- Fotos liegen als Graustufen-WebP in `assets/` und werden nicht mehr eingebettet; `index.html` benötigt `assets/` daneben. Farb-Originale nur noch in der Git-Historie (z. B. Commit 57d4e72).
- Boolesche/camelCase-Attribute (z. B. `noValidate`, `onClick`) in der Quelle immer camelCase schreiben; die Template-Engine verwirft kleingeschriebene Varianten.
- Bis 520 px Breite: Sprachwahl im mobilen Menü, Farbmodus-Schalter als Icon-Button (44×44).
- Neue Farb-Tokens `--control-line` und `--tile-bg`/`--tile-fg` für Bedienelement-Rahmen und bildlose Kacheln.

## Bekannte Probleme

- Die Website ist aus diesem Repository noch nicht veröffentlicht; die bisherige Live-Seite liegt unter https://jegucab.github.io/WorldSoul/ und enthält die Verbesserungen aus task-1-2 noch nicht.
- Kein Build-Werkzeug für das Bundle im Repository vorhanden.
- Die Seite hat kein Favicon (Browser fordern /favicon.ico an und erhalten 404).

## Empfohlener nächster Schritt

Änderungen mit dem Repository synchronisieren. Einziger offener Task ist task-2-1 (blockiert): Freigabe für GitHub Pages bei Futureway-Akademie anfragen. Danach ggf. Roadmap um weitere Aufgaben ergänzen (z. B. Favicon).
