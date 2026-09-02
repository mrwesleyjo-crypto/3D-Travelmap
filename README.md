# Mijn Reisalbum — Redesign Fase 3: Paspoort als boek

## Gebruiken
Zelfde structuur als voorheen — alleen `index.html` en `bundle.js` zijn
gewijzigd (geen datawijzigingen, dus `countries.geojson` en `assets/`
hoef je niet opnieuw te vervangen, maar zitten voor het gemak toch in de
levering).

## Wat is er gebouwd (Fase 3)

**Gesloten omslag** — als je naar 📖 Paspoort navigeert, zie je eerst een
gesloten, koraalkleurig paspoortboekje met "PASSPORT" en je huidige
bezoek-telling ("12 landen bezocht"). Tikken erop opent het boek.

**Open-animatie** — de omslag klapt open met een subtiele 3D-achtige
rotatie (CSS `rotateY`, geen 3D-library nodig), waarna het boek soepel
invervaagt. Elke keer dat je opnieuw naar Paspoort navigeert, begint het
weer bij de gesloten omslag — een klein terugkerend ritueel, zoals
gevraagd.

**Twee pagina's naast elkaar (desktop/tablet)**
- **Linkerpagina**: "Mijn Paspoort" titel, je voortgang (X/aantal landen,
  percentage, voortgangsbalk), zoekbalk en filters (Alle / Bezocht /
  Wishlist / Nog niet).
- **Rechterpagina**: de landenlijst — tik een land voor de volledige
  detailpagina (stempel, steden, reizen, herinneringen — allemaal je
  bestaande functionaliteit, nu gepresenteerd als boekpagina). Een
  "Terug naar lijst"-pijl brengt je terug naar de landenlijst-pagina.
  Het wisselen tussen lijst en detail heeft nu een zachte
  overvloei-/schuifovergang, alsof je een bladzijde omslaat.

**Mobiel: swipebaar in plaats van naast elkaar** — op smalle schermen
staan de twee pagina's niet naast elkaar (past niet), maar swipe je er
native tussen (CSS scroll-snap, geen extra gebaar-JS nodig — dus licht
en soepel).

**Toegankelijkheid** — `prefers-reduced-motion` wordt gerespecteerd: de
boek-animaties vallen dan vrijwel weg i.p.v. gedwongen te spelen.

## Architectuurkeuze: opnieuw hergebruik, geen rewrite
- Alle bestaande elementen (`progressCount`, `searchInput`, `countryList`,
  `detailView`, `detailFlag`, `detailStamp`, enzovoort) zijn **letterlijk
  dezelfde DOM-elementen met dezelfde ID's** — alleen verplaatst naar de
  nieuwe boek-pagina's. Geen van de render-functies (`buildCountryList`,
  `renderDetail`, `renderCountryTripsSection`, etc.) hoefde te worden
  aangepast.
- De oude `#panel`-wrapper (met de open/dicht-schuifanimatie van een
  zijbalk) is vervangen door de boek-structuur; die specifieke
  schuif-CSS was toch niet meer nodig nu Paspoort een eigen volwaardige
  sectie is.
- De "Bucketlist"-status heet in de linkerpagina-filter nu ook overal
  "Wishlist", consistent met Fase 1-2.

## Getest voor oplevering
- Syntax-check van de gebundelde JS
- Kruiscontrole: elk element dat de code opzoekt bestaat ook in de HTML
- Controle op dubbele functie/variabele-declaraties
- Controle dat er geen restanten van de oude paneel-opmaak zijn
  achtergebleven

## Nog niet gebouwd (volgende fases)
- **Fase 4**: echte artistieke, per-land unieke paspoortstempels met een
  "stempel-inslag"-animatie wanneer een land voor het eerst op Bezocht
  wordt gezet (nu nog de eenvoudige stempel van hiervoor)
- **Fase 5-6**: Journey-object uitbreiden + "Play Journey"-animatie
- **Fase 7**: Memories als scrapbook-album
- **Fase 8-10**: mobiele optimalisatie, animatie-polish, opruimen

Laat weten hoe het boek aanvoelt — dan ga ik door met Fase 4 (de
artistieke stempels).
