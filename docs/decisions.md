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
