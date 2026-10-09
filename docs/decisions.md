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

## 2026-10-09 – Hosting auf Render statt GitHub Pages

### Kontext

GitHub Pages ließ sich für das Teilnehmerkonto im Repository `Futureway-Akademie/J.Aragons_Project` nicht aktivieren (Einstellungsseite 404). Die Futureway-Admins schlugen Render vor.

### Entscheidung

Die Website wird als Render Static Site aus Branch `main` mit Publish Directory `world-soul` und ohne Build-Schritt veröffentlicht: https://world-soul.onrender.com. Die Datenschutzerklärung (Punkt 2) nennt Render Services, Inc., 525 Brannan Street, Suite 300, San Francisco, CA 94107, USA (Adresse laut render.com/terms), Stand Oktober 2026.

### Begründung

Keine Codeänderung nötig, da die Seite statisch ist; nur `world-soul/` wird ausgeliefert, und jeder Merge nach `main` wird automatisch veröffentlicht.

## 2026-10-09 – Favicon aus den Logo-Buchstaben

### Kontext

Die Seite hatte kein Favicon; Browser erhielten für `/favicon.ico` einen 404. Zur Auswahl standen drei Entwürfe: A (Logo-Buchstaben „WS“ auf hellem Grund), B (weißes „WS“ auf Markenblau), C (Routen-Motiv mit „WS“).

### Entscheidung

Der Teilnehmer wählte Entwurf A, um der Marke treu zu bleiben. Die Buchstaben werden aus `assets/logo-ws-alpha.png` ausgeschnitten und auf einem hellen Quadrat (#f3f2f2) platziert; `favicon.ico` enthält 16/32/48 px mit abgerundeten Ecken, `apple-touch-icon.png` ist ein volles 180×180-Quadrat (Systeme runden selbst).

### Begründung

Der helle Grund hält die dunkelblauen Buchstaben auch in dunklen Browser-Tabs sichtbar; die Dateien liegen im Website-Stamm, sodass `/favicon.ico` direkt beantwortet wird.

## 2026-10-09 – Link-Vorschau für Crawler ohne JavaScript

### Kontext

Das og:image verwies relativ auf ein transparentes 1080×1080-PNG. Zudem sahen Link-Vorschau-Crawler im ausgelieferten Bundle nur den Titel „Bundled Page“ und keine Meta-Angaben, da alle Tags im JSON-Template stecken und erst per JavaScript eingefügt werden.

### Entscheidung

Neues Vorschaubild `assets/og-image.png` (1200×630, deckender heller Grund, Logo in Originalgröße, Text „PLATAFORMA INTERCULTURAL DE MÚSICA / GUANAJUATO ⇄ LEIPZIG“ in Markenblau #1b3a5c – Farbe und Text vom Teilnehmer gewählt). Vollständige Open-Graph-/Twitter-Angaben mit absoluten URLs auf https://world-soul.onrender.com in Quelle und Template; zusätzlich Titel, Beschreibung und dieselben Angaben im statischen Kopf beider Bundles.

### Begründung

Nur der statische Kopf ist für Crawler sichtbar; der deckende Hintergrund verhindert schwarze Flächen in dunklen App-Designs. Die Ortsangabe kann bei Wachstum der Plattform später angepasst werden.
