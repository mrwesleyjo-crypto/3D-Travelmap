# Mijn Reisalbum — interactieve 3D wereldkaart (Fase 1 + 2 + 3)

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

Lokaal testen: `python3 -m http.server 8000` (niet als `file://` openen —
IndexedDB en de geojson-fetch werken dan niet).

## Fase 3 — Foto's

- **Foto's toevoegen per plek**: elke plaats in een reistijdlijn heeft nu een
  fotostrip met een "+"-tegel. Klik erop voor de bestandenkiezer, of sleep
  foto's er direct op (drag & drop).
- **IndexedDB, geen localStorage** — precies zoals gevraagd: foto's (die al
  snel groot worden) gaan naar IndexedDB; localStorage blijft voor lichte
  data (status, steden, reismetadata). Foto's worden bij het uploaden
  automatisch teruggeschaald naar max. 1600px zodat de opslag niet
  onnodig volloopt.
- **Lightbox**: klik op elke foto (in de tijdlijn, een landpaneel, de
  reisomslag, of het fotoalbum) voor een groot lichtbak-scherm met
  pijltjestoetsen/knoppen om te bladeren, een bewerkbare bijschrift-regel,
  en een verwijderknop.
- **Covers**: een reiskaart en de reisdetailpagina tonen automatisch de
  eerst-geüploade foto als omslagfoto (i.p.v. de vlag-placeholder) zodra
  die er is.
- **Landpagina als mini-fotoalbum**: zodra een land foto's heeft, krijgt het
  landpaneel een hero-afbeelding bovenaan en een "Memory gallery"
  thumbnail-grid onderaan. De statusregel toont nu ook
  "X reizen · Y steden bezocht · Z herinneringen".
- **Fotoalbum-pagina werkt nu echt**: alle foto's van al je reizen door
  elkaar, met simpele filterchips (Alles / per jaar / per land) en een
  luchtig masonry-grid.

## Fase 1 & 2 (ter herinnering)
Warme travel-journal stijl, navigatie, drie landstatussen (bezocht/
bucketlist/niet bezocht), land selecteren met adaptieve zoom, zichtbare
stedentoggle, reizen aanmaken met tijdlijn en route-op-de-globe. Zie de
eerdere versies van dit bestand voor details — die functionaliteit is
ongewijzigd gebleven.

## Wat nog niet is gebouwd (Fase 4)
- Algeheel "memories"-overzicht met extra statistieken
- Paspoortstempels (decoratief detail per land)
- Verdere polish/kleine animaties

## Bestanden aangepast in deze update
- **`src/main.js`** — volledige IndexedDB-laag (`reisalbum_db`, store
  `photos`, met indexes op plaats/reis/land), afbeelding-compressie via
  canvas, upload + drag&drop per plek, lightbox-component, fotoalbum-
  weergave met filters, cover-logica voor reiskaarten en -detail, hero +
  memory gallery in het landpaneel.
- **`index.html`** — lightbox-markup en -stijl, fotostrip-stijl in de
  tijdlijn, hero/memory-gallery-stijl, echt fotoalbum-grid i.p.v. de
  placeholder, trip-cover met afbeelding.
- `bundle.js` opnieuw gegenereerd.
- `cities.js`, `countries.geojson`, de textures — ongewijzigd.

## Datastructuur
```js
// IndexedDB: reisalbum_db → store "photos" (indexes: placeId, tripId, countryKey)
{ id, tripId, placeId, countryKey, countryName, city, blob, caption, date, createdAt }

// localStorage (ongewijzigd t.o.v. Fase 1/2)
reisalbum_status_v1   // { [countryKey]: 'visited' | 'bucketlist' }
reisalbum_cities_v1   // { [countryKey]: { [cityName]: true } }
reisalbum_trips_v1    // [{ id, countryKey, countryName, name, startDate, endDate, note, places[] }]
```

## Let op
Foto's zitten in de IndexedDB van de browser — die staat **lokaal op het
apparaat** en gaat niet automatisch mee als je GitHub Pages opnieuw
deployt of op een ander apparaat/browser inlogt. Een export/backup-functie
zou een mooie toevoeging zijn voor een latere fase, mocht je dat willen.

Zeg het gerust als dit goed werkt — dan pak ik Fase 4 op (memories-
overzicht, paspoortstempels, polish).
