# Mijn Reisalbum — interactieve 3D wereldkaart (Fase 1 + Fase 2)

## Gebruiken
Zet alle bestanden en mappen hieronder samen in je repo (root of `/docs`
voor GitHub Pages):

```
index.html
bundle.js
countries.geojson
assets/
  earth-blue-marble.jpg
  earth-topology.png
```

Lokaal testen: `python3 -m http.server 8000` (niet als `file://` openen).

## Fixes n.a.v. je feedback op Fase 1
- **Auto-rotatie staat nu standaard uit** (toggle in ⚙ Kaartweergave staat
  standaard uit; je kunt 'm zelf aanzetten).
- **Klikken op een land zoomt nu automatisch en vloeiend in** — de
  zoomafstand past zich aan de grootte van het land aan (dichterbij voor
  Nederland, verder weg voor Rusland), dus je hoeft niet meer zelf handmatig
  bij te zoomen.
- **De wazige kaart bij inzoomen is verholpen.** De oorzaak: de gebruikte
  globe-textuur was maar 1600×800 pixels — veel te laag voor dichtbij. Ik
  gebruik nu een 4096×2048 textuur (`earth-blue-marble.jpg`, standaard
  meegeleverd in de three-globe-library) plus anisotropic filtering en een
  fijnere bol-curvatuur, wat er samen voor zorgt dat de kaart scherp blijft
  tot vlak boven het landoppervlak.

## Fase 2 — Reizen & tijdlijn
- **Nieuw navigatie-item werkt nu echt**: "📖 Mijn reizen" toont al je
  reizen als kaartjes (bestemming, data, aantal plekken).
- **Reis aanmaken**: via "+ Nieuwe reis" (in Mijn Reizen, of direct vanuit
  een landpaneel als "+ Nieuwe reis naar [land]") vul je naam, start-/
  einddatum en een notitie in.
- **Reistijdlijn**: binnen een reis zie je een verticale tijdlijn van
  plaatsen — elk met datum en notitie, en een kruisje om te verwijderen.
  "+ Plaats toevoegen" laat je een stad kiezen (met suggesties uit de
  bekende steden van dat land) plus datum en notitie.
- **Route op de globe**: zodra een reis met 2+ plaatsen (met bekende
  coördinaten) geopend is, tekent de bol een zachte koraalkleurige,
  geanimeerde route-lijn tussen de plekken, en zoomt de camera automatisch
  naar het gebied van de reis.
- **Landpaneel toont nu ook "Mijn reizen"** voor dat land, met snelkoppeling
  naar elke reis.
- Reis bewerken/verwijderen kan via de potlood-/prullenbak-iconen in de
  reisdetailweergave (met bevestiging bij verwijderen).

## Wat nog niet is gebouwd (Fase 3 & 4)
- Foto's uploaden, IndexedDB, gallery, lightbox, captions
- Memories-overzicht, paspoortstempels, extra polish/animaties

## Bestanden aangepast in deze update
- **`src/main.js`** — auto-rotate default uit, adaptieve zoom-naar-land
  met scherpere randafhandeling, hogere-resolutie textuur + anisotropic
  filtering, volledig nieuw datamodel + UI voor reizen (`reisalbum_trips_v1`
  in localStorage), generiek formulier-modal-systeem, reistijdlijn, route-
  op-de-globe via een arcs-laag, en integratie in het landdetailpaneel.
- **`index.html`** — nieuwe modal-opmaak, tripkaarten, tijdlijn-styling,
  "Mijn reizen"-overzicht en -detailweergave, kleine bugfix (stedensectie
  in het landpaneel werd soms afgebroken vóór de nieuwe reizen-sectie kon
  renderen — nu opgelost).
- **`assets/earth-blue-marble.jpg`** vervangt `earth-day.jpg` (4096×2048 i.p.v.
  1600×800).
- `bundle.js` opnieuw gegenereerd vanuit `src/main.js`.
- `cities.js`, `countries.geojson` — ongewijzigd.

## Datastructuur
```js
// localStorage: reisalbum_status_v1
{ [countryKey]: 'visited' | 'bucketlist' }

// localStorage: reisalbum_cities_v1
{ [countryKey]: { [cityName]: true } }

// localStorage: reisalbum_trips_v1
[{
  id, countryKey, countryName, name, startDate, endDate, note,
  places: [{ id, city, date, note, lat, lng }]
}]
```
Voor Fase 3 (foto's) komt hier een `photos`-laag in IndexedDB bij, gekoppeld
aan `placeId`, zoals afgesproken in je oorspronkelijke opzet.

Zeg het gerust als dit goed aanvoelt — dan ga ik door met Fase 3 (foto's).
