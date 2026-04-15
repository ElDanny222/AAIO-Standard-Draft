# GEO-ohjeistus v0.1

**Status:** Luonnos  
**Versio:** 0.1.0  
**Päivämäärä:** 2026-04-09  
**Tekijät:** [Tekoäly-Dani](https://tekoalydani.com)  
**Lisenssi:** Apache 2.0  
**Yläspesifikaatio:** [AAIO-ydinspesifikaatio v0.1](aaio-core-v0.1.md)  

> 🇬🇧 [English version](../../specs/geo-guidelines-v0.1.md)

---

## Tiivistelmä

Generative Engine Optimization (GEO) on käytäntö, jolla optimoidaan verkkosisältöä niin, että se näkyy AI:n tuottamissa syntetisoiduissa vastauksissa. Kun AEO keskittyy siihen, että sisältöä *siteerataan* AI-vastausmoottoreissa, GEO keskittyy siihen, että sisältö *sisällytetään ja syntetisoidaan* AI-järjestelmien tuottamiin vastauksiin. GEO on AIO-pinon kolmas kerros, joka rakentuu SEO:n ja AEO:n perustan päälle.

---

## 1. Johdanto

### 1.1 Mitä GEO on?

GEO käsittelee perustavanlaatuista muutosta siinä, miten tieto tavoittaa käyttäjät. Perinteinen haku palauttaa linkkejä. Vastausmoottorit palauttavat viittauksia. Mutta **generatiiviset moottorit** syntetisoivat kokonaan uusia vastauksia yhdistämällä, parafrasoimalla ja päättelemällä useista lähteistä. GEO varmistaa, että sisältösi tulee osaksi tätä synteesiä.

### 1.2 GEO vs. AEO

| Näkökohta | AEO | GEO |
|-----------|-----|-----|
| **Tavoite** | Tule siteeratuksi lähteenä | Tule sisällytetyksi syntetisoiduihin vastauksiin |
| **Mekanismi** | Suora viittaus linkillä | Sisältö sulautettu osaksi generoitua tekstiä |
| **Attribuutio** | Yleensä eksplisiittinen (lähdelinkki) | Usein implisiittinen (sekoitettu synteesi) |
| **Mittaus** | Viittaustiheys | Sisällyttämisaste, käsiteattribuutio |

### 1.3 Miksi GEO on tärkeää

1. **AI Overviews / SGE**: Googlen AI Overviews syntetisoi vastauksia perinteisten tulosten yläpuolelle — jos sisältösi ei ole mukana synteesissä, menetät näkyvyyttä vaikka SEO olisi vahva
2. **Monilähteinen synteesi**: ChatGPT, Claude, Gemini ja Perplexity yhdistelevät useita lähteitä — GEO varmistaa, että datasi muovaa tuotosta
3. **Brändiauktoriteetti**: Kun AI käyttää johdonmukaisesti sisältöäsi vastauksiin, brändistäsi tulee implisiittinen auktoriteetti
4. **AAIO:n ennakkoedellytys**: AI-ostosaagentit käyttävät syntetisoitua tietoa toimittajien arviointiin

### 1.4 Paikka AIO-pinossa

```
┌─────────────────────────────────────────┐
│  AAIO  — Autonomiset agentit             │
├─────────────────────────────────────────┤
│  GEO   — Näky tuotetuissa vastauksissa  │  ◄── TÄMÄ KERROS
├─────────────────────────────────────────┤
│  AEO   — Tule siteeratuksi              │
├─────────────────────────────────────────┤
│  SEO   — Ole ryömittävissä              │
└─────────────────────────────────────────┘
```

---

## 2. Miten generatiiviset moottorit käyttävät sisältöä

### 2.1 Sisällön valinnan putkilinja

Generatiiviset moottorit valitsevat sisällön monivaiheisen putkilinjan kautta:

```
1. HAKU       →  Löydä ehdokaslähteet (SEO/AEO-kerros)
2. SIJOITUS   →  Pisteytä lähteet relevanssin, auktoriteetin ja tuoreuden mukaan
3. POIMINTA   →  Pura avaintosiasiat, väitteet ja data
4. SYNTEESI   →  Yhdistä poimittu tieto yhtenäiseksi vastaukseksi
5. ATTRIBUUTIO →  Viittaa valinnaista käytettyihin lähteisiin
```

GEO optimoi vaiheille 2–4: saa sisältösi sijoittumaan korkeammalle, poimittavaksi paremmin ja syntetisoitavaksi puhtaammin.

### 2.2 Mitä tekee sisällöstä "GEO-ystävällistä"

Generatiiviset moottorit suosivat sisältöä, joka on:

| Ominaisuus | Kuvaus | Esimerkki |
|------------|--------|---------|
| **Kattava** | Käsittelee aiheen perusteellisesti, ei pintapuolisesti | 2000+ sanan opas vs. 200 sanan blogikirjoitus |
| **Jäsennetty** | Selkeä hierarkia, otsikot, listat, taulukot | Hyvin organisoitu tekninen dokumentaatio |
| **Faktuaalinen** | Todennettavissa olevat väitteet näytöllä | "Markkinakoko: 7,3 miljardia (Gartner, 2026)" vs. "Markkina on valtava" |
| **Auktoritatiivinen** | Tunnustettujen asiantuntijoiden kirjoittama | Tekijä alan tunnistetiedoilla + viittaukset |
| **Ajankohtainen** | Äskettäin päivitetty tuoreella datalla | `dateModified` alle 90 päivää sitten |
| **Uniikki** | Alkuperäiset oivallukset, joita ei löydy muualta | Primaaritutkimus, omistusoikeudellinen data |
| **Yksiselitteinen** | Selkeät määritelmät, ei ristiriitaisia lausuntoja | "AAIO on [määritelmä]" vs. epämääräiset kuvaukset |

---

## 3. GEO-sisältöstrategia

### 3.1 Määräävä sisältö

Luo sisältöä, joka on paras yksittäinen lähde tietyllä aiheella. Generatiiviset moottorit painottavat kattavia, auktoritatiivisia sivuja enemmän synteesissä.

**Määräävän sisällön piirteet:**
1. **Syvyys**: Käsittelee kaikki relevantit osa-aiheet, reunatapaukset ja vivahteet
2. **Data**: Sisältää täsmälliset numerot, päivämäärät ja todennettavissa olevat faktat
3. **Rakenne**: Selkeä hierarkia, joka mahdollistaa täsmällisen poiminnan
4. **Omaperäisyys**: Sisältää oivalluksia, kehyksiä tai dataa, joita ei löydy muualta
5. **Täydellisyys**: Vastaa kysymykseen täysin — ei "klikkaa lisätietoja varten"

### 3.2 Käsiteomistajuus

GEO on **käsitteiden omistamista** AI-tietoavaruudessa. Kun AI tuottaa vastauksen AAIO:sta, sisältösi pitäisi olla ensisijainen tietolähde.

**Strategioita käsiteomistajuuteen:**

| Strategia | Toteutus |
|-----------|---------|
| **Määrittele termi** | Selkeät "X on Y" -määritelmät, joita LLM:t voivat käyttää suoraan |
| **Luo termistöä** | Luo ja käytä johdonmukaisesti täsmällisiä termejä (esim. "AAIO-valmiuspisteet") |
| **Luo kehyksiä** | Julkaise jäsennetyt kehykset, joihin muut viittaavat |
| **Julkaise dataa** | Alkuperäinen tutkimus, kyselyt, vertailut täsmällisillä numeroilla |
| **Rakenna vertailut** | Auktoritatiiviset vertailutaulukot (X vs. Y) |

### 3.3 Aiheauktoriteettiklusterit

Rakenna toisiinsa yhteydessä olevia sisältöjä ydinkonseptien ympärille:

```
               ┌──────────────────────┐
               │   Pilari-sivu (Napa) │
               │   "AI-optimointi"    │
               └──────────┬───────────┘
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
  ┌─────┴─────┐    ┌─────┴─────┐    ┌─────┴─────┐
  │  SEO AI-  │    │    AEO    │    │   AAIO    │
  │ aikakau-  │    │   Opas    │    │Viitekehys │
  │ della     │    │           │    │           │
  └───────────┘    └───────────┘    └───────────┘
```

**Miksi klusterit toimivat GEO:lle:**
- LLM:t yhdistävät aiheellisen syvyyden auktoriteettiin
- Toisiinsa linkitetty sisältö luo vahvistavia tietosignaaleja
- Aiheen monien puolien kattaminen lisää synteesin sisällyttämistä

### 3.4 Tuoreus ja päivitystahti

Generatiiviset moottorit painottavat tuoretta sisältöä enemmän:

| Sisältötyyppi | Suositeltu päivitystiheys |
|-------------|--------------------------|
| Ydinkäsitteiden määritelmät | Vuosittain (ellei toimiala muutu) |
| Tekniset spesifikaatiot | Neljännesvuosittain |
| Markkinadata ja tilastot | Kuukausittain |
| Uutiset ja kommentit | Viikoittain |
| Hinnoittelu ja saatavuus | Reaaliaikaisesti |

---

## 4. Tekniset GEO-vaatimukset

### 4.1 Rakenteinen data GEO:lle

#### ClaimReview

Sisällölle, joka esittää todennettavissa olevia väitteitä:

```json
{
  "@context": "https://schema.org",
  "@type": "ClaimReview",
  "claimReviewed": "AAIO voi lisätä agenttien ajamaa liikevaihtoa 40 %",
  "reviewBody": "Perustuu 12 suomalaisen yrityksen pilottitoteutuksiin...",
  "reviewRating": {
    "@type": "Rating",
    "ratingValue": 4,
    "bestRating": 5,
    "alternateName": "Enimmäkseen totta"
  },
  "author": {
    "@type": "Organization",
    "name": "Tekoäly-Dani"
  }
}
```

#### Dataset

Alkuperäistä dataa sisältävälle sisällölle:

```json
{
  "@context": "https://schema.org",
  "@type": "Dataset",
  "name": "AAIO-valmistusbenchmark 2026",
  "description": "AAIO-valmiuspisteet 500 suomalaisen verkkokaupan yli",
  "creator": {
    "@type": "Organization",
    "name": "Tekoäly-Dani"
  },
  "datePublished": "2026-04-01"
}
```

#### DefinedTerm

Termistön vahvistamiseen:

```json
{
  "@context": "https://schema.org",
  "@type": "DefinedTerm",
  "name": "AAIO",
  "description": "Agentic AI Optimization — optimointikerros, joka määrittelee miten verkkosivustot tulee rakentaa autonomisten AI-agenttien yhteentoimivuutta varten",
  "inDefinedTermSet": {
    "@type": "DefinedTermSet",
    "name": "AIO-termistö",
    "url": "https://tekoalydani.com/sanasto"
  }
}
```

### 4.2 Sisällön muotoilu poimintaa varten

| Muoto | Miksi se auttaa | Esimerkki |
|-------|----------------|---------|
| **Määritelmäkappaleet** | Suora poiminta "mikä on X?" -kyselyihin | Ensimmäinen kappale alkaa "AAIO on..." |
| **Vertailutaulukot** | Jäsennetty data helposti jäsennettäväksi vastauksiin | Markdown/HTML-taulukot selkeillä otsikoilla |
| **Numeroitulistat** | Vaiheittaiset menettelyt poimitaan sellaisenaan | "Miten toteuttaa AAIO: 1. ... 2. ..." |
| **Avain-arvo -parit** | Tosiasiat poimitaan yksitellen | "Markkinakoko: 7,3 miljardia", "CAGR: 40 %+" |
| **Lainaukset** | Asiantuntijausoittelut poimitaan auktoriteetiksi | Nimetty asiantuntija + tunnistetiedot + väite |

---

## 5. GEO-mittaus

### 5.1 Avainmittarit

| Mittari | Kuvaus | Miten mitata |
|---------|--------|-------------|
| **Sisällyttämisaste** | Kuinka usein sisältösi näkyy AI:n tuottamissa vastauksissa | Kysy AI-moottoreita ydinkonsepteistasi, seuraa läsnäoloa |
| **Käsiteattribuutio** | Yhdistääkö AI brändisi avain-käsitteisiin | Kysy AI:lta "Kuka on auktoriteetti X:ssä?" |
| **Sisällön synteesin tarkkuus** | Edustaaoko AI dataasi oikein | Tarkista AI:n tuottamat väitteet sisältöäsi vastaan |
| **Kilpailuasema** | Sisällyttämisasteesi vs. kilpailijoiden | Vertailuanalyysi useissa AI-moottoreissa |

### 5.2 GEO-auditointiprosessi

1. **Tunnista ydinkonseptit**: Listaa 10–20 konseptia, jotka brändisi pitäisi omistaa
2. **Kysy AI-moottoreita**: Kysy ChatGPT:ltä, Claudelta, Geminiltä ja Perplexityltä jokaisesta konseptista
3. **Analysoi vastaukset**: Seuraa, viitataanko sisältöäsi, sisällytetäänkö se vai puuttuuko se
4. **Kartoita aukot**: Tunnista aiheet, joilla kilpailijat näkyvät mutta sinä et
5. **Priorisoi**: Keskitä sisällönluominen suurimpiin vaikutusvaltaisiin aukkoihin
6. **Testaa uudelleen kuukausittain**: Seuraa parannuksia ajan myötä

---

## 6. GEO-tarkistuslista

### 6.1 Pikakäynnistys (1 viikko)

- [ ] Auditoi 10 parasta aihetta tärkeimmissä AI-moottoreissa (ChatGPT, Perplexity, Gemini)
- [ ] Lisää selkeät määritelmäkappaleet kaikille avain-käsitesivuille
- [ ] Varmista, että `dateModified` on tarkka kaikessa sisällössä
- [ ] Luo "Tärkeimmät havainnot" -tiivistelmä pilari-sisältöjen yläosaan
- [ ] Lisää `TechArticle` tai `Article` Schema.org kaikille sisältösivuille

### 6.2 Perusta (1 kuukausi)

- [ ] Rakenna tai vahvista 3–5 aiheauktoriteettiklusteria
- [ ] Luo määräävät sivut jokaiselle ydinkonseptille, jonka haluat omistaa
- [ ] Lisää vertailutaulukoita tärkeimmille "X vs. Y" -kyselyille
- [ ] Julkaise alkuperäistä dataa tai tutkimusta `Dataset` Schema.org -merkinnällä
- [ ] Lisää `DefinedTerm`-merkinnät omistusoikeudelliselle termistölle

### 6.3 Edistynyt (jatkuva)

- [ ] Kuukausittaiset GEO-auditoinnit kaikissa tärkeimmissä AI-moottoreissa
- [ ] Neljännesvuosittaiset sisällön tuoreus-päivitykset kaikilla pilari-sivuilla
- [ ] Luo asiantuntija-kirjoitettua sisältöä täydellisellä `Person`-merkinnällä
- [ ] Rakenna viittausverkosto: saa muiden auktoriteettilähteiden viittaukset
- [ ] Julkaise toimialavertailuja ja raportteja ladattavalla datalla

---

## 7. GEO ja AAIO

GEO ja AAIO ovat toisiaan täydentäviä mutta erillisiä:

- **GEO** varmistaa, että AI-järjestelmät *tietävät sinusta* ja sisällyttävät sisältösi syntetisoituun tietoon
- **AAIO** varmistaa, että AI-agentit voivat *toimia sen tiedon perusteella* — löytää, navigoida ja asioida

Kun GEO on vahva, AAIO hyötyy koska:
1. AI-ostosaagentit käyttävät GEO-lähtöistä tietoa toimittajien arviointiin
2. GEO:n kautta rakennettu brändiauktoriteetti lisää agenttien luottamusarvoja
3. Kattava GEO-sisältö tarjoaa rakenteisen datan, jota AAIO-agentit tarvitsevat

**Eteneminen:**
```
SEO  → "Agentit voivat löytää sinut"
AEO  → "Agentit siteeraavat sinua lähteenä"
GEO  → "Agentit tuntevat datasi hyvin"
AAIO → "Agentit voivat asioida kanssasi autonomisesti"
```

---

## Liite A: Viitteet

- [Schema.org](https://schema.org/) — Rakenteisen datan sanasto
- [E-E-A-T Guidelines](https://developers.google.com/search/docs/fundamentals/creating-helpful-content) — Sisällön laadun kehys
- [AEO Best Practices](aeo-guidelines-v0.1.md) — Vastausmoottorioptimointiopas (ennakkoedellytys)
- [AAIO Core Specification](aaio-core-v0.1.md) — AAIO:n ydinstandardi

---

*Tämä dokumentti on osa [AAIO Standard Draft](../../README.md) -projektia, jonka ylläpitäjä on [Tekoäly-Dani](https://tekoalydani.com).*
