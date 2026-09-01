# Mijn Reisalbum — interactieve 3D wereldkaart (Fase 1)

Een warme, persoonlijke 3D wereldkaart als ingang naar je reisherinneringen.

## Gebruiken
Zet alle bestanden en mappen hieronder samen in je repo (root of `/docs`
voor GitHub Pages):

```
index.html
bundle.js
countries.geojson
assets/
  earth-day.jpg
  earth-topology.png
```

Lokaal testen: `python3 -m http.server 8000` (niet als `file://` openen).

## Wat is er in Fase 1 gebouwd

**Nieuwe stijl** — warme cream/coral/gold travel-journal look in plaats van
het donkere sterrenveld. Geen glassmorphism, geen sci-fi sfeer.

**Navigatie** — bovenaan (desktop) / onderaan (mobiel): 🌍 Wereldkaart,
📖 Mijn reizen, ⭐ Bucketlist, 📸 Fotoalbum. De laatste twee tonen nu nog
een vriendelijke "komt eraan"-melding — dat is Fase 3/4 werk (foto's, IndexedDB).

**Drie landstatussen** — bezocht (koraal), bucketlist (goud) en niet bezocht
(neutrale zandtint), zichtbaar op de bol, in de zijlijst en in de legenda.

**Land selecteren zonder per ongeluk af te vinken** — een klik op een land
(of in de lijst) opent nu een landpaneel met vloeiende zoom-naar-land, in
plaats van het direct als bezocht te markeren. In het paneel kies je expliciet
"✓ Bezocht", "⭐ Bucketlist" of "○ Nog niet bezocht".

**Steden per land** — het landpaneel toont de steden uit `cities.js` met
aanvinkbare status. Een stad aanvinken zet het land automatisch op "bezocht"
als dat nog niet zo was.

**Stedentoggle nu goed vindbaar** — een ⚙-knop rechtsboven opent een
"Kaartweergave"-popover met duidelijke aan/uit-schakelaars voor Steden en
Auto-rotatie, plus een "Reset weergave"-knop (voorheen een verstopt setting).

**Bucketlist-pagina** — een echt overzicht van je bucketlist-landen als
kaartjes, met snelknoppen om te verplaatsen naar "bezocht" of te verwijderen.

**Wholesome details** — een subtiele toast ("Japan toegevoegd aan jouw
wereld ✈️") bij een nieuw bezocht land, en een voortgangsregel
("12 landen bezocht 🌍 · 6% van de wereld ontdekt").

## Bestanden aangepast in deze update
- **`index.html`** — volledig herschreven: nieuw kleurenpalet/typografie,
  navigatiebalk (top + bottom), kaartinstellingen-popover, landdetailpaneel
  (met statusknoppen + stedenchecklist), bucketlist/reizen/album-views.
- **`src/main.js`** (bron, wordt gebundeld tot `bundle.js`) — herschreven:
  datastructuur voor 3 statussen + stedenchecks in localStorage (met migratie
  vanaf de oude versie zodat niemand voortgang verliest), klik-op-land opent
  nu een paneel i.p.v. direct af te vinken, vlag-emoji per land, view-switching
  tussen de 4 hoofdsecties, warmere belichting en `earth-day.jpg` als
  globe-textuur i.p.v. de donkere nachtversie.
- **`bundle.js`** — opnieuw gegenereerd vanuit `src/main.js`.
- `cities.js` en `countries.geojson` — ongewijzigd, worden hergebruikt.

## Datastructuur (voorbereid op Fase 2-4)
```js
// localStorage: reisalbum_status_v1
{ [countryKey]: 'visited' | 'bucketlist' }

// localStorage: reisalbum_cities_v1
{ [countryKey]: { [cityName]: true } }
```
Voor Fase 2 (reizen/tijdlijn) en Fase 3 (foto's) volgt zoals afgesproken een
IndexedDB-laag voor trips/places/photos, met localStorage puur voor lichte
metadata (status, settings) — precies zoals in je opzet beschreven.

## Volgende fases (nog niet gebouwd)
- Fase 2: reizen aanmaken, reistijdlijn, locaties koppelen aan een reis
- Fase 3: foto's uploaden (IndexedDB), gallery, lightbox, captions
- Fase 4: memories-overzicht, routes op de globe, paspoortstempels, polish

Zeg het gerust als Fase 1 goed aanvoelt — dan bouw ik Fase 2 verder uit.
