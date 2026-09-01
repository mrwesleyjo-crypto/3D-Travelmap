# Reisjournaal — interactieve 3D wereldkaart

Een 3D draaibare wereldbol waarop je landen kunt afvinken als bezocht, met
optionele markers voor hoofdsteden en grote steden.

## Gebruiken
Open gewoon `index.html` in een browser, of zet de map op GitHub Pages
(root of `/docs`) — geen build-stap nodig, puur vanilla JS/HTML/CSS met
ES-module imports via CDN (three.js + three-globe).

## Bestanden
- `index.html` — de hele app: markup, styling en logica
- `cities.js` — hoofdsteden + belangrijke steden (naam, land, lat/lng, continent)

## Features
- Klik op een land op de bol om het te markeren als bezocht (goud) — met
  smooth camera fly-to en polygon-transities
- Zijpaneel met zoekbare, per continent gegroepeerde landenlijst,
  filter (alle / bezocht / nog niet) en voortgangsbalk
- Toggle om hoofdstad- en grote-stad-markers te tonen/verbergen
- Bezochte landen worden opgeslagen in localStorage (blijft bewaard na herladen)
- Sterrenveld, atmosfeer-glow, damped orbit-controls, subtiele auto-rotatie
- Volledig responsive: bottom-sheet paneel op mobiel

## Personaliseren
- Kleuren/typografie staan bovenin de `<style>` als CSS-variabelen
  (`--gold`, `--ink-*`, `--serif`, `--sans`)
- Landdata komt live van een Natural Earth GeoJSON via unpkg — dus geen
  eigen land-bestand nodig
- `cities.js` uitbreiden met extra steden kan gewoon door een object toe
  te voegen aan de `CITIES`-array
