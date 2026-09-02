# Mijn Reisalbum — Redesign compleet (Fase 1-10)

## Gebruiken
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

Alleen `index.html` en `bundle.js` zijn deze ronde gewijzigd — `assets/`
en `countries.geojson` zijn ongewijzigd t.o.v. de vorige levering.

## Fase 5 — Journey-object uitgebreid
Elke reis heeft nu ook een **vervoersmiddel** (✈️ vliegtuig, 🚗 auto,
🚆 trein, 🚌 bus, ⛴️ boot), instelbaar bij het aanmaken/bewerken van een
reis en zichtbaar als badge naast de reistitel.

## Fase 6 — Play Journey
Een nieuwe **"▶ Play Journey"**-knop in elke reis met 2+ herkende stops:
- de kaart zoomt naar het startpunt
- elke etappe wordt geanimeerd getekend, met het vervoersicoon dat
  meebeweegt (en meedraait in de reisrichting)
- bij aankomst verschijnt de volgende genummerde pin met een korte bounce
- aan het eind valt alles terug op de normale, statische route
- **`prefers-reduced-motion`**: de animatie wordt dan overgeslagen en je
  krijgt direct de statische route te zien

## Fase 7 — Herinneringen als scrapbook
Het fotoalbum is herbouwd tot een echt **digitaal scrapbook**:
- grote foto met locatie, datum en (indien aanwezig) een cursief
  bijschrift eronder
- filmstrip met kleine thumbnails, synchroon met welke foto in beeld is
- prev/next-pijlen op desktop; **swipebaar op mobiel** (dezelfde
  CSS-scroll-snap-aanpak als het paspoort — geen extra gebaar-code nodig)
- klik op de grote foto voor de volledige lightbox (ongewijzigd, inclusief
  bijschrift bewerken en verwijderen)

## Fase 8 — Mobiele optimalisatie
Gerichte controle en fixes:
- touch-targets vergroot naar ~44px op mobiel (sluitknoppen,
  icoon-knoppen, filters, statusknoppen)
- scrapbook-pijlen verborgen op mobiel (swipen werkt al native)
- gecontroleerd op horizontale overflow bij de nieuwe onderdelen

## Fase 9 — Animatie-polish
- `prefers-reduced-motion` nu consistent toegepast op alle nieuwe
  onderdelen (scrapbook, Play Journey, stempel-animatie)
- subtiele hover-lift op de statistiekkaartjes, consistent met de rest
  van de app (reiskaarten, bucketkaarten hadden dit al)

## Fase 10 — Bug fixing & opruimen
- **Bug gevonden en gefixt**: het bewerken van een foto-bijschrift in de
  lightbox verversten het scrapbook niet live — nu wordt na het opslaan
  automatisch de juiste weergave (reis, album, statistieken) bijgewerkt.
- Laatste restjes "Bucketlist" in gebruikersgerichte tekst vervangen door
  "Wishlist", consistent met Fase 1.
- Volledige testroutine opnieuw gedraaid vóór oplevering: syntax-check,
  kruiscontrole van alle DOM-verwijzingen, controle op dubbele
  functie/variabele-declaraties — allemaal schoon.

## Alle 10 fases nu compleet
1. Navigatie + rustige kaart
2. Land-interactie (zwevende landkaart)
3. Paspoort als boek (omslag + open-animatie + bladzijden)
4. Artistieke, per-land unieke paspoortstempels + stempel-inslag-animatie
5. Journey-object (incl. vervoersmiddel)
6. Play Journey-animatie
7. Herinneringen als scrapbook-album
8. Mobiele optimalisatie
9. Animatie-polish
10. Bug fixing + cleanup

## Wat bewust niet is gebouwd
Zoals afgesproken in de oorspronkelijke opdracht: geen accounts, geen
sociale features, geen achievements/gamification-laag, geen backend. Alles
blijft volledig client-side en werkt gewoon op GitHub Pages.

Laat weten hoe het geheel aanvoelt, of als je ergens nog een puntje wilt
bijschaven.
