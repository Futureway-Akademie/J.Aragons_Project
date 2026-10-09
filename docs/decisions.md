# Entscheidungen

## 2026-10-08 – Arbeitsbereich world-soul/

### Kontext

Der World-Soul-Code wurde in das Futureway-Workshop-Repository übernommen, dessen Struktur erhalten bleiben muss.

### Entscheidung

Projektarbeit findet ausschließlich unter `world-soul/` statt. Workshop-Dateien (`.agents/`, `.github/`, `AGENTS.md`, `CLAUDE.md`, `README.md`) werden nicht verändert; `.workshop/` und `docs/` nur zur Pflege von Projektzustand und Dokumentation.

### Begründung

Die Workshop-Struktur und das Dashboard sollen unverändert funktionieren; Änderungen werden später in das offizielle World-Soul-Repository übernommen.

## 2026-10-08 – Quelle und Bundle gemeinsam ändern

### Kontext

`index.html` ist ein generiertes Bundle, das die Quelle `World Soul.dc.html` eingebettet enthält. Im Repository gibt es kein Werkzeug, um das Bundle neu zu erzeugen.

### Entscheidung

Jede Änderung wird per Skript gleichzeitig in der Quelle und im eingebetteten Template von `index.html` und `world-soul-index.html` vorgenommen. Das Skript prüft die erwartete Trefferzahl jeder Ersetzung und schreibt erst, wenn alle Ersetzungen passen. Ersetzungen verankern sich nicht an camelCase-Attributen wie `onClick`, da diese im Bundle anders kodiert sind.

### Begründung

Eine Änderung nur an der Quelle würde die ausgelieferte Seite nicht verändern; die Trefferzahl-Prüfung verhindert, dass Quelle und Bundle auseinanderlaufen.

## 2026-10-08 – Eigene Tokens für Bedienelemente und Kacheln

### Kontext

Rahmen von Formularfeldern und Outline-Buttons lagen mit `--line` unter 3:1; bildlose Tour-Kacheln nutzten `--btn-bg` und wurden im Dunkelmodus grell hellblau.

### Entscheidung

Neue Tokens `--control-line` (nur für Bedienelemente) sowie `--tile-bg`/`--tile-fg` (im Dunkelmodus tiefes Markenblau). `--line` bleibt für Abschnittslinien unverändert.

### Begründung

Bedienelemente erreichen WCAG 3:1, ohne das Layout durch dunklere Abschnittslinien schwerer wirken zu lassen.

## 2026-10-09 – Kompakter Header auf Smartphones

### Kontext

Bei 375 px Breite war der Header 63 px zu breit: Der Menü-Button lag außerhalb des Bildschirms, die Seite scrollte seitlich, und die Bedienelemente waren nur 36 px hoch.

### Entscheidung

Bis 520 px Breite zeigt der Header nur Logo, Farbmodus-Schalter und Menü-Button (je 44×44 px). Die Sprachwahl wird dort ausgeblendet und erscheint stattdessen im mobilen Menü (Buttons 48×44 px). Die Beschriftung des Farbmodus-Schalters wird nur visuell ausgeblendet und bleibt für Screenreader erhalten.

### Begründung

Alle Bedienelemente bleiben sichtbar und mit dem Finger gut treffbar, ohne die Sprachwahl zu entfernen; ab 521 px bleibt der Header unverändert.

## 2026-10-09 – camelCase-Attribute und zugängliches Kontaktformular

### Kontext

Das Formular trug `novalidate="{{ true }}"`. Die Template-Engine verwirft kleingeschriebene React-Attribute, daher blieb die Browser-Validierung aktiv: Der Submit-Handler lief nie, die eigenen Fehlermeldungen in der Seitensprache erschienen nicht, stattdessen zeigte der Browser seine Meldung in der Browsersprache.

### Entscheidung

React-Attribute werden in der Quelle immer in camelCase geschrieben (`noValidate`, `onClick`, …); im Bundle erscheinen sie kodiert als `sc-camel-…`. Das Formular validiert selbst: Das fehlerhafte Feld erhält `aria-invalid="true"` und den Fokus, alle Felder verweisen per `aria-describedby` auf die Statusmeldung `#ws-form-status` (`role="status"`).

### Begründung

Fehlermeldungen erscheinen in der gewählten Seitensprache und werden von Screenreadern dem betroffenen Feld zugeordnet.

## 2026-10-09 – Fotos als Graustufen-WebP außerhalb des Bundles

### Kontext

`index.html` war 2,28 MB groß, davon ca. 1,83 MB eingebettete Fotos (Base64), die beim Öffnen immer vollständig geladen wurden – `loading="lazy"` war dadurch wirkungslos. Die Fotos lagen bereits nahe der benötigten Auflösung; eine erneute JPEG-Kodierung mit Windows-Bordmitteln sparte höchstens 15 %.

### Entscheidung

Die 13 Fotos werden als WebP in Graustufen (Qualität 0,8) unter `assets/` abgelegt und nicht mehr eingebettet; das Logo bleibt eingebettet und wurde auf 300 px Breite verkleinert. Der ungenutzte Ordner `uploads/` (Originale, 55 MB) und die alten JPEGs wurden entfernt.

### Begründung

Die Seite zeigt alle Fotos per CSS-Filter in Graustufen; Graustufen-WebP spart 39 % ohne sichtbaren Unterschied (PSNR 38,5–42 dB). Ausgelagerte Fotos werden erst beim Scrollen geladen, die initiale Datei schrumpft um 83 %. Farb-Originale bleiben über die Git-Historie wiederherstellbar.
