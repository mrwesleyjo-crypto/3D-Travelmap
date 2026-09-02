# Mijn Reisalbum — interactieve 3D wereldkaart

## Gebruiken
Zet alle bestanden en mappen hieronder samen in je repo (root of `/docs`
voor GitHub Pages):

```
index.html
bundle.js
countries.geojson
assets/
  earth-blue-marble-light.jpg
  earth-topology.png
  gizmo.png
  gizmo-face.png
  gizmo-alt.png
  gizmo-alt-face.png
```

Lokaal testen: `python3 -m http.server 8000` (niet als `file://` openen).

## Deze update — je 5 punten

**1. Meertalige landnamen** — Gizmo vraagt nu als allereerste stap "In welke
taal wil je landnamen zien?" (Nederlands 🇳🇱 / English 🇬🇧 / Deutsch 🇩🇪 /
Français 🇫🇷 / Español 🇪🇸). De vertaaltabel voor alle 176 landen komt uit
de officiële ISO-landendatabase, niet uit losse aannames. Overal waar een
landnaam wordt getoond (landpaneel, lijst, bucketlist, reizen, stempel,
toasts) verschijnt nu de vertaalde naam. Je kunt de taal altijd wijzigen
via ⚙ Kaartweergave → 🌐 Taal. Het "Nieuwe reis"-formulier gebruikt nu
bovendien een echte dropdown voor het land — geen typefouten meer mogelijk,
en dat lost meteen een deel van punt 3 en 4 op (zie hieronder).

**2. Lichter water op de globe** — de oceaan was bijna zwart-navy. Ik heb de
textuur zelf bewerkt: alleen de blauwe (oceaan-)pixels zijn lichter en
zachter gemaakt, de landkleuren zijn ongemoeid gelaten.

**3 & 4. "Mijn reizen" duidelijker + de stippellijn (route) uitgelegd** —
De kans is groot dat de route niet verscheen omdat een vrij getypte
plaatsnaam niet overeenkwam met een bekende stad (alleen dán kan ik 'm op
de kaart tekenen). Dat werd nergens uitgelegd. Nu:
- **Land kiezen** gaat via een dropdown i.p.v. vrij typen — geen mismatches
  meer.
- Bij **"Stad" invullen** staat direct een uitleg: kies een suggestie voor
  een plek op de kaart, of typ zelf iets — dat komt dan wél in je tijdlijn
  maar (nog) niet op de kaart.
- Elke stop in de tijdlijn toont nu een klein 🗺️ (staat op de kaart) of 📍
  (nog niet herkend) icoontje.
- Boven de tijdlijn staat een statusregel: "🗺️ Zichtbaar op de kaart" zodra
  er 2+ herkende stops zijn, of een tip als dat nog niet zo is.
- Na het toevoegen van een plek zegt de melding nu expliciet of hij wel of
  niet op de kaart verscheen.

**5. Gizmo's nieuwe uiterlijk** — je twee nieuwe afbeeldingen zijn verwerkt:
de zwaaiende pose is nu overal Gizmo's gezicht/figuur (dezelfde bestands-
namen, dus automatisch overal bijgewerkt), en de nadenkende pose gebruik ik
specifiek bij de taalkeuzestap in de intro.

## Bestanden aangepast in deze update
- **`src/translations.js`** — nieuw: vertaaltabel voor 176 landen in 5 talen.
- **`src/main.js`** — taallogica (`displayName`, `matchCountryByAnyName`,
  taalkeuze in onboarding + instellingen), dropdown voor land bij een
  nieuwe reis, uitleg + status-iconen rond de route/kaart-koppeling,
  nieuwe Gizmo-afbeeldingen.
- **`index.html`** — CSS voor de taalkeuze-knoppen, dropdown-veld,
  route-status-chip en kaart-badges.
- **`assets/earth-blue-marble-light.jpg`** — nieuw, vervangt de te donkere
  textuur.
- **`assets/gizmo*.png`** — nieuwe afbeeldingen van je mascotte.
- `bundle.js` opnieuw gegenereerd. `cities.js`, `countries.geojson`
  ongewijzigd.

## Scope-keuze die ik bewust heb gemaakt
De rest van de interface (knoppen, uitleg, Gizmo's teksten) blijft
Nederlands — alleen landnamen worden vertaald. De hele interface naar 5
talen vertalen is een veel groter project; zeg het als je dat ook wilt, dan
pak ik dat apart op.

Laat weten of dit nu lekker werkt, vooral punt 3/4 ben ik benieuwd of de
uitleg nu duidelijk genoeg is.
