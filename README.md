# Mijn Reisalbum — platte 2D wereldkaart

## Gebruiken
Zet alle bestanden en mappen hieronder samen in je repo:

```
index.html
bundle.js
countries.geojson
assets/
  gizmo.png, gizmo-face.png, gizmo-alt.png, gizmo-alt-face.png
  leaflet/
    leaflet.css
    images/ (5 bestandjes)
```

Lokaal testen: `python3 -m http.server 8000` (niet als `file://` openen).

## Deze update — je 2 punten

**1. "Punt A naar B lukt niet, er zijn niet genoeg steden"** — je had he-
lemaal gelijk: 166 van de 199 landen hadden maar 1 stad (alleen de hoofd-
stad). Een route van A naar B bouwen was voor 83% van de landen dus
letterlijk onmogelijk. Ik heb de stedenlijst flink uitgebreid: van 240 naar
**465 steden**, waarmee nu **117 landen 2 of meer steden** hebben
(gemiddeld 2,3 per land i.p.v. 1,2). Populaire reisbestemmingen (Thailand,
Marokko, Mexico, Griekenland, Vietnam, Italië, Peru, etc.) hebben nu vaak
4-8 steden, genoeg om een echte meerdaagse route mee te bouwen via
"📍 Voeg toe via de kaart".

**2. Slechte kwaliteit landgrenzen van dichtbij** — de oorzaak: de vorige
kaartdata was bedoeld voor overzicht op wereldschaal (1:110 miljoen), veel
te grof om op in te zoomen. Ik heb de hele landendataset vervangen door
een **10x preciezere bron** (10km-resolutie i.p.v. 110km), gebaseerd op
OpenStreetMap/Natural Earth. Grenzen en kustlijnen ogen nu echt vloeiend,
ook van dichtbij.

**Bijvangst van de datavervanging**: de nieuwe bron kent ook een paar
landen die de oude, grovere data helemaal miste (bijv. Moldavië, Syrië nu
met correcte volledige naam i.p.v. afkortingen als "UK"/"UAE" die de
brondata soms gaf — die heb ik met de hand gecorrigeerd naar volledige
namen).

**Eerlijke kanttekening**: 7 hele kleine landen (Monaco, San Marino,
Vaticaanstad, Malediven, Saint Kitts en Nevis, Nauru, Tuvalu) hebben in
deze precisere bron geen eigen landvlak — ze zijn te klein voor een
10km-resolutie dataset om als aparte polygon te tekenen. Hun hoofdsteden
staan wél gewoon als stedenmarker op de kaart en zijn bruikbaar voor
routes; alleen "klik het land aan om te markeren als bezocht" werkt voor
die 7 landen niet. Gezien het gaat om de kleinste micro-staten ter wereld
is dat een bewuste, verantwoorde afweging tegenover de veel betere
kwaliteit voor de overige 219 landen.

## Bestanden aangepast in deze update
- **`countries.geojson`** — volledig vervangen door een 10km-resolutie
  dataset (`@geo-maps/countries-land-10km`, OSM/Natural Earth-gebaseerd),
  met opnieuw gegenereerde `NAME`/`ISO_A2`-velden zodat de rest van de app
  ongewijzigd kan blijven werken.
- **`src/translations.js`** — opnieuw gegenereerd op basis van de nieuwe,
  completere landenset (219 landen i.p.v. 176), met handmatige correcties
  voor een paar landen waar de brondata een afkorting of omslachtige
  officiële naam gaf (bijv. "UK" → "United Kingdom", twee keer "Congo" →
  "Congo" / "Congo (DRC)").
- **`src/main.js`** — twee verouderde naam-aliassen gecorrigeerd
  (Tsjechië/Eswatini wezen naar niet meer bestaande sleutels).
- **`src/cities.js`** — uitgebreid van 240 naar 465 steden.
- `bundle.js` opnieuw gegenereerd.

Laat weten of de kaart nu scherp genoeg oogt en of je nu genoeg steden
hebt om routes mee te bouwen voor de landen die je in gedachten had.
