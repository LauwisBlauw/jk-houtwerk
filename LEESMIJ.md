# JK Houtwerk — voorbeeldwebsite

`index.html` is de hele website: één bestand, met alle stijl en scripts erin. Dubbelklik het
bestand om het in de browser te openen — er is geen server, build-stap of internetverbinding nodig.

## Wat er in zit

| Onderdeel | Bijzonderheden |
|---|---|
| Opening | "Welkom bij JK Houtwerk", met uw introductietekst en de slotregel "Kwaliteit is onze belofte" |
| Diensten | Vijf diensten als rijen: links de omschrijving, rechts de werkzaamheden |
| Galerij | Schuifgalerij: één foto in beeld, schuift elke 5 seconden door |
| Contact | Formulier waarin klanten hun gegevens en hun vraag of klus achterlaten, met e-mailadres en werkgebied ernaast |

## Kleuren

Het palet heet **gebrand hout & mos**:

| Rol | Kleur |
|---|---|
| Papier | `#F1F0EC` |
| Tekst | `#1A1917` |
| Links en accenten | `#4A5B41` (mosgroen) |
| Accentkleur | `#C9962B` (het goud uit uw logo) |
| Donkere balken en vlakken | `#14120F` / `#16150F` |

Het groen komt uit de luiken van het bijgebouw met de rieten kap op uw eigen foto. Alle kleuren
staan bovenaan in `index.html` bij elkaar onder `:root`; verandert u daar één waarde, dan gaat de
hele site mee. De donkere balk boven en onder gebruikt aparte `--balk-*`-kleuren, die bewust niet
met de lichte of donkere modus meewisselen.

## Het logo

De site gebruikt uw eigen logo, omgekleurd naar de kleuren van de site.

| Bestand in `logo` | Wat het is |
|---|---|
| `jk-houtwerk-logo-origineel.png` | zoals u het aanleverde, 1690 × 931 |
| `jk-houtwerk-logo-licht.png` | voor de lichte modus: inktkleurige letters, gouden nerf |
| `jk-houtwerk-logo-donker.png` | voor de donkere modus: cremewitte letters, gouden nerf |

De balken boven- en onderaan zijn in beide standen donker, zodat het logo er altijd hetzelfde in
staat: cremewitte letters met een gouden nerf. Hun kleuren staan als `--balk-*` in de tokens en
wisselen bewust niet mee met de lichte of donkere modus; de secties ertussen doen dat wel. Zo
krijgt de pagina in de lichte modus een donkere kop en voet, met krijtwit ertussen.

Het logo staat op beide plekken als data-URI in `index.html`, zodat de site één zelfstandig
bestand blijft en het logo ook meekomt in een gedeelde link. Liever een los bestand? Zoek op
`merk-beeld` en vervang de `src`-en door `logo/jk-houtwerk-logo-donker.png`.

`jk-houtwerk-logo-licht.png` gebruikt de site zelf niet meer, maar dat bestand is bewaard: die
heeft u nodig zodra het logo op een witte ondergrond moet, bijvoorbeeld op briefpapier of een
factuur.

Het omkleuren gebeurde per pixel op basis van uw origineel: wat verzadigd was (de nerf en de
ondertitel) kreeg de accentkleur, de rest de tekstkleur. De vorm zelf is onaangeroerd.

Eén ding blijft de moeite waard: vraag degene die het logo maakte om een **vectorversie**
(SVG, PDF of AI). Een PNG is een vast raster — prima voor het scherm, maar korrelig op groot
formaat zoals autobelettering of een bouwbord. Met een vectorbestand kan ik de kleuren bovendien
zonder kwaliteitsverlies aanpassen.

Er staat bewust geen telefoonnummer op de site: contact loopt via het formulier en e-mail.
Wilt u toch gebeld kunnen worden, dan is één regel in het contactblok genoeg —
`<div class="contact-rij"><dt>Telefoon</dt><dd><a href="tel:+31612345678">06 – 12 34 56 78</a></dd></div>`.

De site staat standaard in de lichte modus, ongeacht wat de bezoeker op zijn telefoon of computer
heeft ingesteld. Wie liever donker leest, klikt op het knopje in de balk. Wilt u dat omdraaien en
juist de instelling van de bezoeker volgen, zeg het dan — dat is een klein blokje CSS.

Verder: navigatie die op smalle schermen naar een tweede regel zakt, toetsenbordnavigatie, en
rustige animaties die uitgaan als iemand "minder beweging" heeft ingesteld.

De galerij schuift vanzelf door, maar stopt zodra iemand er met de muis op staat, erin veegt of
er met het toetsenbord in zit — en er is een pauzeknop. Wie "minder beweging" heeft ingesteld,
krijgt geen automatisch doorschuiven. Vegen op de telefoon werkt ook als het script niet laadt;
dan verdwijnen alleen de knoppen en de stippen.

Wilt u een andere beeldverhouding voor de foto's? Pas `--foto-verhouding` aan in de regel
`aspect-ratio: var(--foto-verhouding, 4 / 3)`. De tijd tussen twee foto's staat in het script bij
`const WACHTTIJD = 5000` (milliseconden).

## De foto's

In de map `fotos` staan uw originelen (`IMG_….jpg`, elk 2 tot 4 MB) én de versies die de site
gebruikt: bijgesneden op 4:3, 1300 px breed en teruggebracht tot 80 tot 300 KB per stuk. Zulke
telefoonfoto's van 4 MB rechtstreeks op een site zetten maakt hem traag op mobiel, vandaar.

De namen zeggen wat erop staat (`gevel-rieten-kap-kozijnen.jpg`, `inbouwkast-op-maat.jpg`) — dat
helpt bij Google.

De galerij is 4:3, net als een liggende telefoonfoto. **Liggende foto's** hoeven daarom alleen
verkleind te worden:

```
magick UWFOTO.jpg -auto-orient -resize 1300x -strip -quality 80 nieuwe-naam.jpg
```

**Staande foto's** passen niet in dat kader. Bijsnijden zou de bovenkant of onderkant afsnijden —
bij een inbouwkast of een gevel is dat precies het werk dat u wilt laten zien. Daarom staat de hele
foto in beeld en zijn de zijkanten opgevuld met een vervaagde uitvergroting van dezelfde foto:

```
magick UWFOTO.jpg -auto-orient \
  \( -clone 0 -resize 1300x975^ -gravity center -extent 1300x975 -blur 0x24 -modulate 88 \) \
  \( -clone 0 -resize x975 \) \
  -delete 0 -gravity center -composite -strip -quality 82 nieuwe-naam.jpg
```

Alleen de eerste foto wordt meteen geladen; de rest komt binnen zodra hij nodig is, en de site
haalt telkens de volgende alvast op. Zo begint de pagina snel en ziet u toch nooit een leeg vlak.

## Wat nog echt moet worden

Zoek in `index.html` op **`AANPASSEN`** — daar staat bij elk stuk wat er nog nodig is. In het kort:

1. **Contactgegevens** — e-mailadres (op twee plekken: het contactblok en de voet), KvK- en
   btw-nummer. Het werkgebied staat al goed: Utrecht, Gooi en Vechtstreek.
2. **Meer foto's in de galerij** — er staan er nu acht in. Een foto toevoegen is één regel in
   `index.html` (zoek op `dia-item`), en de stippen en de teller tellen vanzelf mee.
   Zet de `alt`-tekst goed: dat is wat blinde bezoekers en Google te zien krijgen.
3. **Dienstteksten** — deze staan er zoals u ze aanleverde. Wilt u een dienst toevoegen of een
   werkzaamheid schrappen, zoek dan op `class="dienst"`.
4. **Losse eindjes** — de opening staat in de ik-vorm, de diensten- en contactteksten nog in
   de wij-vorm. Zeg het als u dat gelijk wilt trekken.

## Het formulier laten werken

Het formulier controleert nu alleen de invoer en zegt dat het een voorbeeld is. Om het echt te
laten versturen zonder eigen server, bijvoorbeeld met Formspree:

1. Maak een gratis formulier aan en kopieer het endpoint.
2. Zet dat op het `<form>`-element:
   `<form class="formulier" id="contactformulier" action="https://formspree.io/f/UWCODE" method="post">`
3. Verwijder het script-blok `/* ---------- Voorbeeldformulier ---------- */` onderaan, zodat de
   browser het formulier gewoon verstuurt.

Netlify Forms werkt ook: dan volstaat `netlify` als attribuut op het formulier, mits u bij
Netlify host.

## Online zetten

De site is statisch — `index.html` plus de map `fotos` — dus vrijwel elke hostingpartij kan het aan:

- **Netlify of Cloudflare Pages** — de hele map naar de browser slepen, klaar.
  Gratis, inclusief https.
- **Eigen hosting via FTP** — `index.html` en de map `fotos` in de webmap zetten.
- **Domein** — `jkhoutwerk.nl` registreren bij een Nederlandse registrar en bij de host
  aanwijzen.

## Nog te doen voordat klanten u kunnen vinden

- **Google Bedrijfsprofiel** aanmaken — voor een lokaal timmerbedrijf levert dat meestal meer
  aanvragen op dan de website zelf.
- **`<meta name="description">`** in de `<head>` staat al op uw werkgebied; pas hem aan als uw
  diensten veranderen.
- **Privacyverklaring** toevoegen zodra het formulier echt gegevens ontvangt.
- **Favicon** toevoegen: een klein `favicon.png` en een regel
  `<link rel="icon" href="favicon.png">` in de `<head>`.

## Later uitbreiden

De galerij is de plek waar de site het meeste gaat opleveren: voor-en-na-paren van eigen klussen
overtuigen meer dan tekst. Vul die eerst.

Daarna kan er altijd meer bij — een werkwijze in stappen, referenties van klanten of richtprijzen.
Zeg het als u dat wilt.
