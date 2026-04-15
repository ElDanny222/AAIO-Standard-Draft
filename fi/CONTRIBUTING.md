# Osallistuminen AAIO Standard Draft -projektiin

> 🇬🇧 [English version](../CONTRIBUTING.md)

Kiitos kiinnostuksestasi AAIO Standard Draft -projektia kohtaan. Tämä on avoin, yhteisölähtöinen spesifikaatio. Kaikki osallistumiset ovat tervetulleita — olipa kyseessä virheen korjaaminen, uuden osion ehdottaminen tai implementaatiokokemuksen jakaminen.

---

## Mitä tämä repositorio on

Tämä repositorio sisältää **luonnosspesifikaatiot** Agentic AI Optimization (AAIO) -standardille. Tavoitteena on tuottaa toimittajaneutraaleja, implementoitavia standardeja, jotka auttavat organisaatioita tulemaan agenttivalmiiksi.

Nämä ovat työstövaiheessa olevia dokumentteja. Kaikki on avoinna keskustelulle. Jos jokin on epäselvää, virheellistä tai puuttuu, se on hyvä syy avata issue tai pull request.

---

## Osallistumistapoja

### Ilmoita ongelmasta

Käytä GitHub Issues -toimintoa ilmoittaaksesi:
- Virheistä tai epäselvyyksistä olemassa olevissa spesifikaatioissa
- Puuttuvista määrittelyistä tai termistöstä
- Rikkinäisistä linkeistä tai muotoiluongelmista
- Vanhentuneista protokollatiedoista

Avaa issue ja kuvaile, mitä on vialla ja missä. Ehdotettua korjausta ei tarvita issuen avaamiseen.

### Ehdota muutosta

Käytä pull requestia ehdottaaksesi:
- Korjauksia olemassa oleviin spesifikaatioihin
- Uusia osioita olemassa olevaan dokumenttiin
- Uusia viiteimplementaatioita `examples/`-hakemistoon
- Skeemalisäyksiä tai -korjauksia

Merkittävien muutosten kohdalla (uudet protokollaprofiilit, suuret rakenteelliset revisiot) avaa ensin issue lähestymistavan keskustelemiseksi ennen PR:n kirjoittamista.

### Jaa implementaatiokokemus

Jos olet toteuttanut AAIO-vaatimuksia todellisessa järjestelmässä ja löytänyt aukkoja, reunatapauksia tai parempia lähestymistapoja — jaa ne. Implementaatiopalaute on tässä vaiheessa arvokkain panostus.

Avaa issue tunnisteella `implementation-feedback` tai lähetä sähköpostia osoitteeseen [dani@tekoalydani.com](mailto:dani@tekoalydani.com).

---

## Pull Request -prosessi

1. **Forkkaa repositorio** ja luo haara `main`-haarasta

   Haarojen nimeäminen:
   - `fix/kuvaus` korjauksille
   - `feat/kuvaus` uudelle sisällölle
   - `docs/kuvaus` dokumentaatioparannuksille

2. **Tee muutoksesi**

   Noudata alla olevaa tyyliopasta.

3. **Päivitä asianomaisen dokumentin tilaotsaketta**

   Jos muutos on oleellinen, päivitä versio tai lisää changelog-merkintä.

4. **Avaa pull request**

   PR-kuvauksessa tulee olla:
   - Mitä muuttui ja miksi
   - Mitkä osiot ovat vaikuttuneet
   - Mahdolliset avoimet kysymykset tai harkitut vaihtoehdot

5. **Arviointi**

   Kaikki PR:t arvioi repositorion ylläpitäjä ([Tekoäly-Dani](https://tekoalydani.com)). Arvioinnissa tarkistetaan:
   - Tekninen tarkkuus
   - Yhtenäisyys AAIO-viitekehyksen kanssa
   - Selkeys ja luettavuus
   - Yhteensopivuus olemassa olevan protokollalandscapen kanssa

6. **Yhdistäminen**

   Hyväksymisen jälkeen panostuksesi yhdistetään. Merkittävät osallistujat mainitaan dokumentissa, johon he ovat osallistuneet.

---

## Tyyliopas

### Dokumenttien muoto

Kaikki spesifikaatiodokumentit noudattavat tätä rakennetta:

```
# Dokumentin otsikko

> **Status:** Draft v0.X | Maintained by [Tekoäly-Dani](https://tekoalydani.com)

[Yksi lause siitä, mitä tämä dokumentti kattaa]

---

## [Osio]

[Sisältö]

---

## Suomeksi / In Finnish

[Dokumentin suomenkielinen tiivistelmä]
```

### Kieli

- **Englanti ensin.** Kaikki spesifikaatiosisältö kirjoitetaan englanniksi.
- **Suomenkielinen tiivistelmä lopussa.** Jokainen spesifikaatiodokumentti sisältää suomenkielisen tiivistelmäosion.
- Tekniset termit (MCP, ACP, UCP, A2A, AAIO) pysyvät englanninkielisinä molemmissa kielisissä osioissa.
- Suora ja täsmällinen kieli. Vältä markkinointikieltä, epävarmuuden ilmaisemista ja täytesanoja.

### Koodiesimerkit

Käytä aidattuja koodilohkoja kielitunnisteilla (json, http, markdown jne.).

### Taulukot

Käytä Markdown-taulukoita jäsennettyihin vertailuihin. Suosi taulukoita pitkien listojen sijaan, kun vertailtavia ominaisuuksia on useita.

### Tilaselitteet

Käytä näitä selitteitä johdonmukaisesti:

| Selite | Merkitys |
|--------|----------|
| `Draft` | Työstövaiheessa oleva dokumentti, voi muuttua |
| `RFC` | Request for Comments — yhteisöarviointi käynnissä |
| `Stable` | Valmistunut, muutokset vaativat uuden version |
| `Deprecated` | Korvattu uudemmalla versiolla |

---

## Laajuus

Tämä repositorio käsittelee nimenomaan **AAIO:ta optimointikehyksenä** — miten organisaatiot toteuttavat agenttiprotokollat tullakseen agenttivalmiiksi.

Repositorion ulkopuolella:
- MCP:n, ACP:n, UCP:n tai A2A:n ydinprotokollamäärittelyt (niillä on omat repositorionsa)
- Yleinen AI- tai LLM-kehitys
- SEO tai perinteinen verkkomarkkinointi

Jos olet epävarma, onko panostuksesi laajuuden puitteissa, avaa issue ja kysy.

---

## Käytösperiaatteet

Tämä on tekninen spesifikaatioprojekti. Panostuksia arvioidaan teknisen ansion ja selkeyden perusteella. Ole suora, ole täsmällinen ja ole rakentava.

---

## Yhteystiedot

[Tekoäly-Dani](https://tekoalydani.com)  
[dani@tekoalydani.com](mailto:dani@tekoalydani.com)
