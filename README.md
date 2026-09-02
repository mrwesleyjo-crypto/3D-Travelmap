# Mijn Reisalbum — Redesign Fase 1 + 2

## Gebruiken
Zelfde bestandsstructuur als voorheen, alleen `index.html`, `bundle.js` en
`countries.geojson` zijn gewijzigd:

```
index.html
bundle.js
countries.geojson
assets/  (ongewijzigd — gizmo*.png + leaflet/)
```

Lokaal testen: `python3 -m http.server 8000`.

## Wat is er gebouwd (Fase 1 + 2 van je herontwerp-spec)

**Fase 1 — nieuwe navigatie + rustige kaart**
- Eén zwevende navigatiebalk onderaan, op zowel desktop als mobiel:
  🌍 Kaart · 📖 Paspoort · ✈️ Reizen · 📷 Herinneringen.
- De oude permanente zijbalk is weg. De kaart krijgt het hele scherm.
- Steden staan nu **standaard uit** (aanzetten kan via ⚙ Instellingen).
- De permanente legenda is verwijderd — kleurbetekenis staat nu in de
  landkaart bij een klik, en wordt één keer uitgelegd via Gizmo's intro.
- "Bucketlist" is geen aparte hoofdsectie meer. De status heet nu
  **Wishlist** en is gewoon een van de drie statussen van een land
  (Bezocht / Wishlist / Nog niet), zichtbaar en instelbaar via het
  landkaartje en het Paspoort.

**Fase 2 — land-interactie**
- Klik op een land: de kaart zoomt er vloeiend naartoe, het land krijgt
  een duidelijke donkere rand (highlight) die blijft staan tot je een
  ander land kiest of het kaartje sluit.
- Er verschijnt een **compacte zwevende landkaart** (geen paneel dat de
  kaart bedekt): vlag, naam, status, een korte statistiekregel
  (reizen · steden · herinneringen), drie statusknoppen, en twee
  snelkoppelingen: "📖 Paspoort" en "✈️ Reizen".

## Architectuurkeuze: hergebruik i.p.v. herbouw
Zoals gevraagd heb ik **geen rewrite** gedaan. De bestaande, werkende
onderdelen zijn hergebruikt:
- **Paspoort** = het bestaande uitgebreide land-paneel (zoeken, filteren,
  stedenchecklist, reizen-sectie, memory-gallery, stempel) — dat bestond
  al en werkte goed, het is nu alleen verplaatst van "permanente zijbalk
  over de kaart" naar "eigen sectie via de Paspoort-navigatie".
- **Reizen** = het bestaande, volledig werkende reizen/route-systeem
  (inclusief "klik op de kaart om een route te bouwen" en de
  voetstappenlijn) — ongewijzigd, alleen hernoemd van "Mijn reizen".
- **Herinneringen** = het bestaande fotoalbum (IndexedDB) — ongewijzigd,
  alleen hernoemd van "Fotoalbum".

Dit betekent: **geen enkele databasemigratie nodig**. Dezelfde
localStorage-sleutels (`reisalbum_status_v1`, `reisalbum_trips_v1`,
`reisalbum_cities_v1`) en dezelfde IndexedDB-foto's worden gewoon
hergebruikt. Al je bestaande bezochte landen, reizen en foto's blijven
intact.

## Wat ik heb laten staan (bewust niet verwijderd)
- De losstaande "Bucketlist"-weergave (`renderBucketlistView()` /
  `#viewBucketlist`) bestaat nog in de code, maar wordt nergens meer
  vanuit de navigatie aangeroepen — hij is "slapend", niet verwijderd,
  voor het geval je 'm later toch ergens voor wilt hergebruiken.

## Getest voor oplevering
- Syntax-check van de gebundelde JS
- Kruiscontrole: elk element dat de code opzoekt bestaat ook echt in de
  HTML
- Controle op dubbele functie/variabele-declaraties (kon zomaar gebeuren
  bij het knippen/verplaatsen van codeblokken)
- Bevestigd dat de opslagstructuur (localStorage-sleutels) niet is
  veranderd — dus geen migratie nodig, bestaande data blijft werken

## Nog niet gebouwd (bewust — volgende fases)
Zoals je zelf aangaf: pas doorbouwen na akkoord op wat er nu staat.
- **Fase 3**: Paspoort als een echt "boek" met open-animatie + bladzijden
- **Fase 4**: Artistieke, per-land unieke paspoortstempels met
  "stempel-inslag"-animatie (nu nog de eenvoudige stempel van hiervoor)
- **Fase 5-6**: Journey-object uitbreiden (vervoersmiddel, "Play Journey"
  met bewegend reisicoon over de route)
- **Fase 7**: Memories als scrapbook-album i.p.v. het huidige grid
- **Fase 8-10**: verdere mobiele optimalisatie, animatie-polish, opruimen

Laat weten of dit als basis goed aanvoelt — dan ga ik door met Fase 3
(het paspoort als boek).
