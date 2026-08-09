# JK Houtwerk — website

`index.html` is de hele website: één bestand, met alle stijl en scripts erin. Dubbelklik het
bestand om het in de browser te openen — er is geen server, build-stap of internetverbinding nodig.

## Wat er in zit

| Onderdeel | Bijzonderheden |
|---|---|
| Opening | "Welkom bij JK Houtwerk", met uw introductietekst en de slotregel "Kwaliteit is onze belofte" |
| Diensten | Vijf diensten als rijen: links de omschrijving, rechts de werkzaamheden |
| Galerij | Schuifgalerij: één foto in beeld, schuift elke 5 seconden door |
| Contact | Formulier waarin klanten hun gegevens en hun vraag of klus achterlaten, met e-mailadres en werkgebied ernaast |

De privacyverklaring staat op een eigen pagina, `privacy.html`, bereikbaar via de voettekst. In de
adresbalk staat hij als **www.jkhoutwerk.nl/privacy** — GitHub Pages laat de `.html` vanzelf weg,
dus de links wijzen naar `/privacy` en niet naar het bestand. Ook
die pagina is zelfstandig: eigen stijl, geen gedeelde bestanden. Wijzigt u de kleuren in
`index.html`, pas ze dan ook bovenin `privacy.html` aan — daar staat dezelfde `:root` in het
klein.

Het tabbladicoon staat in `logo/favicon.svg`, met `favicon-32.png` en `apple-touch-icon.png` als
terugval. Het merk uit uw logo is daarvoor nagetekend: een verkleinde foto wordt op 16 pixels een
streperige brij. In `logo/deelvoorbeeld.jpg` staat het beeld dat WhatsApp en LinkedIn tonen bij een
gedeelde link.

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

De site volgt de instelling van het apparaat: staat de telefoon of computer op donker, dan opent de
site donker. Klikt de bezoeker op het knopje in de balk, dan wint die keuze zolang hij op de site
is. Zet hij zijn apparaat om terwijl de pagina openstaat, dan gaat de site mee — tenzij hij hier
zelf al geklikt had. Die keuze wordt niet onthouden tussen bezoeken; bij een nieuwe bezoek telt de
apparaatinstelling weer.

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

1. **Meer foto's in de galerij** — er staan er nu acht in. Een foto toevoegen is één regel in
   `index.html` (zoek op `dia-item`), en de stippen en de teller tellen vanzelf mee.
   Zet de `alt`-tekst goed: dat is wat blinde bezoekers en Google te zien krijgen.
2. **Dienstteksten** — deze staan er zoals u ze aanleverde. Wilt u een dienst toevoegen of een
   werkzaamheid schrappen, zoek dan op `class="dienst"`.
3. **Losse eindjes** — de opening staat in de ik-vorm, de diensten- en contactteksten nog in
   de wij-vorm. Zeg het als u dat gelijk wilt trekken.

## Het formulier

Het formulier verstuurt echt. Het gaat via **Web3Forms** naar `info@jkhoutwerk.nl`; het account
staat op datzelfde adres. De bezoeker blijft op de pagina: de knop gaat op slot tijdens het
versturen, daarna verschijnt een bevestiging die na drie seconden vervaagt. Gaat er iets mis, dan
komt het e-mailadres als terugvaloptie in beeld — die melding blijft wél staan.

De toegangssleutel staat gewoon zichtbaar in `index.html`. Dat hoort zo: hij kan alleen mail naar
uw eigen adres sturen, niets anders. Een verborgen veld (`botcheck`) vangt spambots af. Wordt het
ooit toch vervelend, vraag dan bij Web3Forms een nieuwe sleutel aan en vervang die ene regel.

## Waar de site staat

De site staat op GitHub en wordt daar gratis gepubliceerd:

| | |
|---|---|
| Code | https://github.com/LauwisBlauw/jk-houtwerk (openbaar) |
| Live | https://www.jkhoutwerk.nl |

De site mag sinds 9 augustus 2026 door zoekmachines gevonden worden; de `noindex`-regel is eruit.
Er staan nu ook een `robots.txt` en een `sitemap.xml` in de repo, en in de `<head>` staan de
bedrijfsgegevens als JSON-LD zodat Google ze direct begrijpt.

Let op: de repo is openbaar. De code én de foto's in `fotos/` zijn dus voor iedereen in te zien.
Wilt u dat later afschermen, dan kan de repo op privé — maar dan stopt de gratis publicatie via
GitHub Pages. Cloudflare Pages en Netlify publiceren wél gratis uit een privé-repo.

### Wijzigingen doorzetten

```
git add -A
git commit -m "korte omschrijving van de wijziging"
git push
```

Binnen een minuut staat de nieuwe versie live.

### Het domein

De site staat op **www.jkhoutwerk.nl**, met een geldig certificaat; `http` en het adres zonder
`www` sturen daar automatisch heen. Het domein staat bij TransIP: `www` wijst met een CNAME naar
`lauwisblauw.github.io`, en het domein zelf met A- en AAAA-records naar GitHub. De MX-, SPF-,
DKIM- en DMARC-records zijn van uw e-mail — daar moet u bij DNS-werk vanaf blijven.

Let op: verloopt de domeinnaam bij TransIP, dan valt de site om. Zorg dat de automatische
verlenging aanstaat.

## Nog te doen voordat klanten u kunnen vinden

- **Google Bedrijfsprofiel** aanmaken — voor een lokaal timmerbedrijf levert dat meestal meer
  aanvragen op dan de website zelf. Hiermee staat u in Google Maps en in het blok met bedrijven
  bovenaan de zoekresultaten.
- **Google Search Console** — daarmee weet Google dat de site bestaat, in plaats van te wachten
  tot hij hem toevallig tegenkomt. U meldt zich aan, krijgt een code, en die zetten we als
  TXT-record bij TransIP.
- **`<meta name="description">`** in de `<head>` staat al op uw werkgebied; pas hem aan als uw
  diensten veranderen.
- **Bewaartermijn in de privacyverklaring** — die staat nu op twee jaar na het laatste contact.
  Klopt dat niet met hoe u werkt, dan is het één zin aanpassen (zoek op `AANPASSEN` bij `privacy`).

## Later uitbreiden

De galerij is de plek waar de site het meeste gaat opleveren: voor-en-na-paren van eigen klussen
overtuigen meer dan tekst. Vul die eerst.

Daarna kan er altijd meer bij — een werkwijze in stappen, referenties van klanten of richtprijzen.
Zeg het als u dat wilt.
