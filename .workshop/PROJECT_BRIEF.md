# Projektbrief

## Projektname

World Soul – Music Manager (Website)

## Idee / Problem

World Soul ist eine interkulturelle Musikplattform zwischen Guanajuato (Mexiko) und Leipzig (Deutschland). Sie braucht eine öffentliche Website, die ihre Leistungen, Touren, Historie, ihr Team und Kontaktmöglichkeiten zeigt.

## Zielgruppe

Unabhängige Bands und Künstler, Veranstaltungsorte, Festivals und Partner in Mexiko und Deutschland.

## Zielplattform

Statische Website auf GitHub Pages, nutzbar auf Desktop und Smartphone.

## Kernfunktionen

- Hero-Bereich mit Route Guanajuato ⇄ Leipzig und Kennzahlen
- „Qué hacemos“: fünf Leistungsbereiche
- Ausgewählte Touren und vollständige Tour-Historie
- Gründer und Team
- Kontaktdaten, Social-Links und Kontaktformular (Formspree)
- Impressum und Datenschutzerklärung
- Vier Sprachen (ES/EN/DE/FR) sowie Hell- und Dunkelmodus

## Nicht-Ziele

- Backend oder Datenbank
- CMS
- Ticketverkauf
- Analyse- oder Tracking-Dienste

## MVP

Die Website ist veröffentlicht, in beiden Farbmodi gut lesbar und auf Desktop und Smartphone bedienbar.

## Definition of Done

- Die Seite funktioniert in allen vier Sprachen und beiden Farbmodi.
- Kein Text unterschreitet WCAG-AA-Kontrast.
- Quelle (`World Soul.dc.html`) und Bundles (`index.html`, `world-soul-index.html`) sind synchron.
- Änderungen betreffen nur `world-soul/` sowie Projektzustand und Dokumentation.
- Durchgeführte Prüfungen sind im `verification`-Objekt des Tasks dokumentiert.

## Technische Rahmenbedingungen

- Quelle: `world-soul/World Soul.dc.html` mit `support.js`, Designsystem „Modernist“ unter `_ds/` und Bildern unter `assets/`.
- Auslieferung: `world-soul/index.html` und `world-soul-index.html` sind identische Single-File-Bundles mit eingebetteter Quelle; React 18.3.1 wird über unpkg geladen.
- Workshop-Dateien (`.agents/`, `.github/`, `AGENTS.md`, `CLAUDE.md`, `README.md`) bleiben unverändert.
