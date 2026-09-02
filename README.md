# Mijn Reisalbum — bugfixes, piratenkaart-stijl & veel meer steden

## Gebruiken
```
index.html
bundle.js
countries.geojson
assets/  (ongewijzigd — hoef je niet opnieuw te vervangen)
```
Alleen `index.html`, `bundle.js` en `countries.geojson` zijn deze ronde
gewijzigd.

## Je 7 punten — wat er is gebeurd

**1 & 4. Route bouwen via klikken werkte niet** — de stedenstippen waren
maar 4 pixels groot én niet gegarandeerd in beeld. Nu: tijdens "route
bouwen" tonen we alléén de steden van dát land, flink vergroot (10-13px
i.p.v. 4-5.5px), en de kaart zoomt automatisch zodat ze allemaal
zichtbaar en klikbaar zijn.

**Bonus-vondst**: tijdens het bouwen van deze fix ontdekte ik een echte
bug — een variabele werd te laat gedeclareerd, wat de hele kaart bij het
laden had kunnen laten crashen. Rechtgezet en getest.

**2. Play Journey "deed niks"** — ik kon dit niet 1-op-1 live reproduceren
(geen browsertoegang beschikbaar deze sessie), maar heb wel alle gebruikte
Leaflet-functies tegen de echte broncode geverifieerd (die kloppen), en de
hele functie waterdicht gemaakt met try/catch/finally: als er ergens iets
misgaat, valt de app netjes terug op de normale route in plaats van dat de
knop permanent "vastloopt". Mocht het nu nog steeds niets doen, dan helpt
een blik in de browserconsole (F12) enorm om de exacte oorzaak te vinden.

**3. Grenslijnen zagen er slecht uit + zwart vierkant bij klikken** — de
échte oorzaak gevonden en verholpen: **83 van de 219 landen hadden
ongeldige, zichzelf-overlappende geometrie** in de kaartdata (een
bijwerking van de eerdere resolutie-verbetering), plus 119 losse
rommelfragmentjes. Dat verklaarde zowel de rare vormpjes als het zwarte
vlak bij selectie (een dikke rand om kapotte geometrie valt extra op). Alle
219 landen zijn nu geometrisch gevalideerd en gerepareerd.

**5. Nederland toont ook de Caribische eilanden** — bevestigd: de brondata
had Aruba/Curaçao/Sint Maarten letterlijk onder "Netherlands" zitten,
waardoor de zoom over de hele Atlantische Oceaan spande. Nu zoomt een
klik altijd naar alleen het grootste (hoofd)landdeel — precies zoals
Google Maps dat ook doet.

**6. Te weinig steden per land** — flink uitgebreid, in twéé rondes deze
sessie: van 465 → 649 → **993 steden**. Gemiddeld nu bijna 5 steden per
land (was 2,3), en nog maar 31 landen onder de 3 (was 164 onder de 4).
Veel landen hebben nu 8-15+ steden om een echte, interessante route mee te
bouwen.

**7. Piratenkaart-stijl** — de kaart is nu een verouderde perkamentkaart
i.p.v. een blauwe wereldkaart: warme beige/zandkleurige ondergrond met
zachte, ongelijkmatige tinten, een subtiele papierkorrel-textuur (SVG-
ruisfilter), vier vage koffievlekken verspreid over het scherm, een lichte
vignet-schaduw naar de randen toe, en sepia-inktkleurige landgrenzen
i.p.v. felle kleuren. Puur decoratief, zit nooit in de weg van het klikken.

## Bestanden aangepast in deze update
- **`countries.geojson`** — alle 219 landen geometrisch gevalideerd en
  gerepareerd (geen self-intersections meer), artefact-fragmenten
  verwijderd.
- **`src/cities.js`** — uitgebreid van 649 naar 993 steden.
- **`src/main.js`** — `pickModeTrip`-declaratievolgorde gefixt (crash-
  risico), stedenmarkers tijdens routebouwen vergroot + auto-zoom naar
  alle beschikbare steden, `flyToFeature` gebruikt nu alleen het grootste
  landdeel voor de zoom, `playJourney` volledig met try/catch/finally
  omhuld, kleurenpalet aangepast naar de piratenkaart-stijl.
- **`index.html`** — nieuwe verouderd-papier-achtergrond, papierkorrel-
  SVG-filter, koffievlek-overlay, vignet.
- `bundle.js` opnieuw gegenereerd.

Laat weten of dit beter aanvoelt — vooral benieuwd naar Play Journey en of
de nieuwe piratenkaart-stijl bevalt.
