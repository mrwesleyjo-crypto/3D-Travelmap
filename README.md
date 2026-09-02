# Mijn Reisalbum — platte 2D wereldkaart

## Grote ombouw: van 3D bol naar platte kaart
Op je feedback dat de 3D-bol lelijk en onpraktisch aanvoelde, is de kaart nu
volledig herbouwd als een **platte, pannable/zoombare 2D-kaart** (met
[Leaflet](https://leafletjs.com), een lichte, veelgebruikte kaart-library —
géén 3D meer, geen zware textures, en de bundel is daardoor ook nog eens
9x kleiner geworden: 1,9MB → 222KB).

## Gebruiken
Zet alle bestanden en mappen hieronder samen in je repo:

```
index.html
bundle.js
countries.geojson
assets/
  gizmo.png
  gizmo-face.png
  gizmo-alt.png
  gizmo-alt-face.png
  leaflet/
    leaflet.css
    images/
      layers.png, layers-2x.png
      marker-icon.png, marker-icon-2x.png, marker-shadow.png
```

Lokaal testen: `python3 -m http.server 8000` (niet als `file://` openen).

## Wat is er veranderd

**Platte kaart** — landen worden getekend als gekleurde vlakken (bezocht /
bucketlist / niet bezocht) op een lichtblauwe "oceaan"-achtergrond, zonder
externe kaarttegels (dus geen CDN-afhankelijkheid, alles blijft lokaal en
snel laden). Slepen om te verschuiven, scrollen/knoppen om te zoomen — een
vertrouwde, praktische kaartervaring in plaats van een bol.

**Steden gewoon zichtbaar** — alle steden (net als voorheen) staan als
puntjes op de kaart, aan/uit te zetten via ⚙ Kaartweergave.

**Punt A naar punt B: een reis bouwen door te klikken** — dit was je
kernvraag. Open een reis en klik op **"📍 Voeg toe via de kaart"**: de app
schakelt naar een "route bouwen"-modus (met een bannertje bovenaan) waarin
je gewoon op steden op de kaart klikt, in de volgorde van je reis. Elke
klik voegt direct een genummerde stop toe. Klik "Klaar" als je route
compleet is. Typen via een formulier (de oude manier) kan nog steeds via
"+ Typ een plek", voor plekken die niet als puntje op de kaart staan.

**De voetstappenlijn** — tussen de stops van een reis wordt nu een
gestippelde koraalkleurige lijn getekend (dashArray-patroon dat als een
lichte voetstappen-route oogt), met genummerde pin-markers per stop.
Werkt nu altijd zodra er 2+ stops met bekende coördinaten zijn — en omdat
"Voeg toe via de kaart" alleen echte, bekende steden aanbiedt, weet je
zeker dat de lijn verschijnt.

**Overige aanpassingen**
- De instelling "Auto-rotatie" is verwijderd (was alleen relevant voor de
  bol).
- Landklikken opent nog steeds het landpaneel; tijdens het bouwen van een
  route via de kaart doet een landklik niets, zodat je stedenklikken niet
  per ongeluk een paneel openen.
- De "foto-indicator" op landen met herinneringen is nu een klein, statisch
  📸-icoontje op de kaart in plaats van een geanimeerde gloed op de bol.
- Alle overige functionaliteit (reizen, foto's/IndexedDB, bucketlist,
  fotoalbum, paspoortstempels, meertalige landnamen, Gizmo-onboarding)
  werkt ongewijzigd door — alleen de kaartweergave zelf is vervangen.

## Bestanden aangepast in deze update
- **`src/main.js`** — de hele "GLOBE"-sectie vervangen door een "KAART"-
  sectie op basis van Leaflet: landlagen, stedenmarkers, route-tekening,
  en de nieuwe klik-om-een-route-te-bouwen-functionaliteit. Verwijzingen
  naar three.js/globe.gl (`world.*`, `THREE.*`, camera/pointOfView-logica)
  zijn overal vervangen door Leaflet-equivalenten (`map.setView`,
  `map.fitBounds`, `L.polyline`, etc.).
- **`index.html`** — Leaflet's CSS gekoppeld, nieuwe stijlen voor de
  kaarttooltips, route-pins, foto-badges en de "route bouwen"-banner;
  de Auto-rotatie-instelling verwijderd.
- **`assets/leaflet/`** — nieuw: Leaflet's CSS + iconbestanden, lokaal
  meegeleverd (zelfde aanpak als steeds: geen externe CDN-afhankelijkheid
  tijdens het laden).
- **Verwijderd**: `earth-blue-marble-light.jpg`, `earth-topology.png` —
  niet meer nodig zonder 3D-bol.
- `bundle.js` opnieuw gegenereerd (nu 222KB i.p.v. 1,9MB, dankzij het
  verdwijnen van three.js/globe.gl).
- `cities.js`, `countries.geojson`, `src/translations.js` — ongewijzigd.

Laat weten of dit zo een stuk praktischer aanvoelt — en of de klik-op-de-
kaart-route precies is wat je voor ogen had.
