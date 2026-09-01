# Mijn Reisalbum — interactieve 3D wereldkaart (Fase 1 + 2 + 3 + Gizmo)

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
  gizmo.png
  gizmo-face.png
```

Lokaal testen: `python3 -m http.server 8000` (niet als `file://` openen).

## Wat is er deze keer aangepast

**Gizmo, je gids** — je eigen mascotte-afbeelding is nu daadwerkelijk in de
app verwerkt (`assets/gizmo.png` en een uitgesneden portret
`assets/gizmo-face.png`), met correct behouden transparantie — geen wit
vlak achter het figuurtje, gewoon los "zwevend" in de popup.

**Onboarding-tutorial bij eerste bezoek** — een zachte, ronde spreekbubbel-
popup (in het warme kleurenpalet van de app, geïnspireerd op je
concept-afbeelding maar passend bij de rest van de stijl) loodst je in 5
korte stapjes langs: land klikken & markeren, een reis aanmaken, foto's
toevoegen, en waar je Gizmo later terugvindt. Sla over kan altijd.
Verschijnt maar één keer per browser (opgeslagen in localStorage); daarna
alleen nog op verzoek.

**Gizmo-hulpknop** — een rond pootje-icoontje rechtsonder (boven de
bottom-nav op mobiel) opent de tutorial opnieuw, wanneer je maar wilt.

**Vriendelijkere lege overzichten** — de kale placeholder-kaarten in Mijn
Reizen, Bucketlist en Fotoalbum zijn vervangen door een Gizmo-tip: zijn
portret naast een korte, warme uitleg — overal in de app dezelfde
gidsende toon in plaats van droge systeemtekst.

**Duidelijker "van stad naar stad"** — de reistijdlijn toont nu genummerde
stops (1, 2, 3…) verbonden met een gestippelde pad-lijn, zodat de route
door een reis expliciet als een route voelt. De knop heet nu
"+ Volgende stop toevoegen" i.p.v. het generieke "+ Plaats toevoegen", en
een lege tijdlijn legt via Gizmo uit wat je moet doen.

## Waarom niet de exacte concept-afbeeldingen?
- Afbeelding 1 (voetstappen-pad) was een Dreamstime-stockfoto met
  watermerk — niet bruikbaar als asset, dus de route-op-de-kaart (al
  gebouwd in Fase 2) en de nieuwe genummerde tijdlijn geven hetzelfde
  "van A naar B"-gevoel zonder die afbeelding letterlijk over te nemen.
- Afbeelding 3 (donkere houten dialoogkaart) was een stijlconcept — de
  structuur (portret + spreekbubbel + knoppen) is overgenomen, maar dan in
  het lichte, warme kleurenpalet van de rest van de app, zodat het niet
  als een vreemde eend in de bijt aanvoelt.
- Afbeelding 2 (Gizmo zelf) had wél een echte transparante achtergrond en
  is 1-op-1 als asset gebruikt.

## Bestanden aangepast in deze update
- **`src/main.js`** — onboarding-stapmachine, Gizmo-hulpknop, gizmo-tip
  empty states, genummerde/gestippelde reistijdlijn.
- **`index.html`** — onboarding-overlay, spreekbubbel- en
  portret-styling, Gizmo-hulpknop, aangepaste tijdlijn-CSS.
- **`assets/gizmo.png`**, **`assets/gizmo-face.png`** — nieuw, uit je
  eigen aangeleverde afbeelding gesneden en geoptimaliseerd voor web.
- `bundle.js` opnieuw gegenereerd. Overige bestanden ongewijzigd.

## Nog openstaand (Fase 4)
- Algeheel "memories"-overzicht met extra statistieken
- Paspoortstempels
- Verdere polish

Laat weten hoe de tutorial en de tijdlijn nu aanvoelen — dan kan ik verder
verfijnen of doorpakken naar Fase 4.
