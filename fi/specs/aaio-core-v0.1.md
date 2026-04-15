# AAIO-ydinspesifikaatio v0.1

**Status:** Luonnos  
**Versio:** 0.1.0  
**Päivämäärä:** 2026-04-09  
**Tekijät:** [Tekoäly-Dani](https://tekoalydani.com)  
**Lisenssi:** Apache 2.0  

> 🇬🇧 [English version](../../specs/aaio-core-v0.1.md)

---

## Tiivistelmä

Agentic AI Optimization (AAIO) on optimointikerros, joka määrittelee miten verkkosivustot ja digitaaliset palvelut tulee rakentaa, jotta autonomiset AI-agentit voivat **löytää**, **ymmärtää**, **navigoida** ja **asioida** niiden kanssa. AAIO ei tuo uutta protokollaa — se määrittelee, miten olemassa olevia protokollia (MCP, ACP, UCP, A2A) ja webstandardeja (Schema.org, OpenAPI, robots.txt) tulisi toteuttaa optimaalisen agentin yhteentoimivuuden saavuttamiseksi.

---

## 1. Johdanto

### 1.1 Tausta

Web siirtyy uuteen aikakauteen, jossa autonomiset AI-agentit toimivat käyttäjien puolesta — tutkivat tuotteita, vertailevat palveluita, neuvottelevat hinnoista ja suorittavat ostoja. Perinteinen SEO optimoi hakukoneiden ryömijöitä ja ihmislukijoita varten. AAIO optimoi pohjimmiltaan erilaista kuluttajaa varten: **AI-ostoagenttia**.

### 1.2 Laajuus

Tämä spesifikaatio määrittelee:

- **AAIO-valmiusmallin**: kyvykkyydet, joita verkkosivustolla täytyy olla agentin yhteentoimivuutta varten
- **AAIO-valmiuspisteet**: kvantitatiivisen kehyksen (0–100) agenttivalmiuden mittaamiseen
- Vaatimukset **koneluettavuudelle**, **navigoitavuudelle** ja **transaktiokykyisyydelle**
- Integroinnit olemassa oleviin protokolliin (MCP, ACP, UCP, A2A)

### 1.3 Suhde SEO:hon, AEO:hon ja GEO:hon

AAIO on edistynein kerros **AIO (AI Optimization)** -pinossa. Kerrokset ovat kumulatiivisia:

| Kerros | Koko nimi | Kohde | Optimoi |
|--------|-----------|-------|---------|
| **SEO** | Search Engine Optimization | Hakukoneiden ryömijät | Sijoitukset, orgaaninen liikenne |
| **AEO** | Answer Engine Optimization | AI-vastausmoottorit (ChatGPT, Perplexity, Gemini) | Viittausten saaminen auktoritatiivisena lähteenä |
| **GEO** | Generative Engine Optimization | AI-tuotetut syntetisoidut vastaukset | Näkyminen LLM-tuotetuissa vastauksissa |
| **AAIO** | Agentic AI Optimization | Autonomiset AI-ostosaagentit | Löytäminen + viittaus + navigointi + transaktio |

**Keskeinen periaate:** AAIO ei korvaa SEO:ta, AEO:ta tai GEO:ta. Ne pinoutuvat kumulatiivisesti.

---

## 2. AAIO-valmistusmalli

AAIO-valmistusmalli määrittelee neljä pilaria, joita verkkosivuston täytyy käsitellä ollakseen täysin optimoitu autonomisille AI-agenteille.

### 2.1 Neljä pilaria

```
┌─────────────────────────────────────────────────────┐
│                  AAIO-VALMIUS                        │
├──────────────┬──────────────┬────────────┬───────────┤
│ LÖYDETTÄVYYS │ LUETTAVUUS   │ NAVIGOINTI │ TRANSAKTIO│
│              │              │            │           │
│  Voivatko    │  Voivatko    │ Voivatko   │ Voivatko  │
│  agentit     │  agentit     │ agentit    │ agentit   │
│  löytää      │  ymmärtää    │ liikkua    │ ostaa/    │
│  sinut?      │  datasi?     │ sivustolla?│ varata?   │
└──────────────┴──────────────┴────────────┴───────────┘
```

### 2.2 Pilari 1: Löydettävyys

Löydettävyys on AI-agenttien kyky löytää verkkosivusto ja tunnistaa se tehtävälleen relevanttina.

| Vaatimus | Prioriteetti | Kuvaus |
|----------|-------------|--------|
| `robots.txt` agenttiohjeistukset | PAKKO | Eksplisiittiset salli/estä-säännöt AI-agenttien user-agenteille |
| `llms.txt` | PITÄISI | LLM-luettava sivustoyhteenveto `/llms.txt`-osoitteessa |
| `ai.txt` | PITÄISI | AI-käytäntöilmoitus `/ai.txt`-osoitteessa |
| `AGENTS.md` | PITÄISI | Agentin ohjaustiedosto repositorion tai sivuston juuressa |
| AAIO-agenttimanifesti | PITÄISI | Koneluettava kyvykkyysilmoitus (ks. luku 5) |
| Jäsennetty sivukartta | PAKKO | XML-sivukartta `<lastmod>`-tiedolla |
| Schema.org `WebSite` | PAKKO | JSON-LD `WebSite`-merkintä `potentialAction`-hakutoiminnolla |

### 2.3 Pilari 2: Koneluettavuus

Koneluettavuus varmistaa, että AI-agentit voivat poimia jäsennettyä, yksiselitteistä tietoa verkkosivustolta.

| Vaatimus | Prioriteetti | Kuvaus |
|----------|-------------|--------|
| Schema.org JSON-LD | PAKKO | Product, Service, Organization, Offer -merkinnät |
| Hinnoittelu rakenteisessa datassa | PAKKO | `price`, `priceCurrency`, `availability` Schema.org-merkinnöissä |
| OpenAPI-spesifikaatio | PITÄISI | Rajapintapäätepisteet dokumentoitu OpenAPI 3.x -muodossa |
| Tuotesyötteet | PITÄISI | Koneluettava tuoteluettelo (JSON, XML tai CSV) |
| Johdonmukainen datamuoto | PAKKO | Sama entiteetti = sama data kaikkialla (ei ristiriitaisia hintoja) |
| Kanonistinen URL | PAKKO | `rel="canonical"` estämään duplikaattientiteettien sekaannukset |

#### Vähimmäis-Schema.org verkkokaupalle

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Tuotteen nimi",
  "description": "Selkeä, faktuaalinen tuotekuvaus",
  "sku": "UNIIKKI-SKU-123",
  "brand": {
    "@type": "Brand",
    "name": "Brändin nimi"
  },
  "offers": {
    "@type": "Offer",
    "price": 99.99,
    "priceCurrency": "EUR",
    "availability": "https://schema.org/InStock",
    "url": "https://example.com/tuote/uniikki-sku-123",
    "priceValidUntil": "2026-12-31"
  }
}
```

#### Datalaadun periaatteet

1. **Yksi totuuden lähde**: Jokaisella entiteetillä (tuote, palvelu, hinta) täytyy olla yksi kanoninen esitys
2. **Ajallinen tarkkuus**: Hintojen, saatavuuden ja varaston täytyy heijastaa reaaliaikaista tilaa
3. **Yksiselitteisyys**: Jokaisella entiteetillä täytyy olla uniikki, vakaa tunniste (SKU, GTIN tai URI)
4. **Täydellisyys**: Puuttuva data on pahempaa kuin likimääräinen data — agentit eivät voi päätellä, mitä ei ole ilmoitettu

### 2.4 Pilari 3: Navigoitavuus

Navigoitavuus määrittelee, kuinka hyvin AI-agentit voivat liikkua verkkosivustolla tietyn tiedon löytämiseksi.

| Vaatimus | Prioriteetti | Kuvaus |
|----------|-------------|--------|
| Looginen URL-rakenne | PAKKO | Ennakoitavat, hierarkkiset URL-polut |
| XML-sivukartta | PAKKO | Täydellinen, ajantasainen sivukartta `/sitemap.xml`-osoitteessa |
| Leivänmuru-merkinnät | PITÄISI | `BreadcrumbList` Schema.org -merkinnät kaikilla sivuilla |
| Sisäinen hakurajapinta | PITÄISI | Ohjelmoitava hakupäätepiste (JSON-vastaukset) |
| Sivutus `rel`-linkeillä | PITÄISI | `rel="next"` / `rel="prev"` sivutetulle sisällölle |
| Kategoriataksonomia | PITÄISI | Koneluettava kategoriahierarkia |
| HTTP-statuskoodit | PAKKO | Oikeat 200/301/404/410 -vastaukset (ei pehmeitä 404-virheitä) |

### 2.5 Pilari 4: Transaktiokykyisyys

Transaktiokykyisyys on AI-agenttien kyky suorittaa kaupallisia toimintoja (osto, varaus, tilaus) verkkosivustolla.

| Vaatimus | Prioriteetti | Kuvaus |
|----------|-------------|--------|
| Koneluettava kassaprosessi | PAKKO | Kassavirta käytettävissä ilman JavaScript-renderöintiä |
| API-pohjainen tilaus | PITÄISI | REST/GraphQL-rajapinta tilauksen luomiseen |
| Selkeät käyttöehdot | PAKKO | Koneella jäsennettävissä olevat ehdot (tai jäsennetty tiivistelmä) |
| Maksuprotokollen tuki | PITÄISI | ACP-yhteensopiva maksuvirta |
| Tilausvahvistus | PAKKO | Jäsennetty tilausvahvistus (JSON tai sähköposti) |
| Palautuskäytäntö | PITÄISI | Koneluettava palautuskäytäntö Schema.org-muodossa |
| Tunnistautuminen | VOI | OAuth 2.0 tai API-avain agenttiistunnoille |

#### Transaktiokypsyystasot

> **Huomio:** Nämä transaktiotasot (L0–L3) mittaavat vain *transaktiokykyisyyttä*. Ne eroavat laajemmasta AIO-kypsyysmallista (L0–L4), joka mittaa yleistä AI-optimointivalmiutta kaikilla neljällä pilarilla.

| Taso | Nimi | Kuvaus |
|------|------|--------|
| L0 | **Vain tiedot** | Agentti voi lukea tuotetietoja, mutta ei voi asioida |
| L1 | **Ostoskorivalmis** | Agentti voi lisätä tuotteita ostoskoriin API:n kautta |
| L2 | **Kassavalmis** | Agentti voi suorittaa kassan (maksu vaatii ihmisen hyväksynnän) |
| L3 | **Täysin autonominen** | Agentti voi suorittaa koko transaktion mukaan lukien maksun (ACP:n kautta) |

---

## 3. AAIO-valmiuspisteet

### 3.1 Yleiskatsaus

AAIO-valmiuspisteet on kvantitatiivinen mittari (0–100), joka arvioi, kuinka hyvin verkkosivusto on optimoitu autonomisille AI-agenteille. Pisteet koostuvat neljästä kategoriapisteestä, jotka vastaavat neljää pilaria.

### 3.2 Pisteytyskehys

| Kategoria | Paino | Enimmäispisteet | Kuvaus |
|-----------|-------|-----------------|--------|
| Löydettävyys | 20 % | 20 | Voivatko agentit löytää ja tunnistaa sivuston? |
| Koneluettavuus | 35 % | 35 | Voivatko agentit poimia rakenteista dataa? |
| Navigoitavuus | 20 % | 20 | Voivatko agentit liikkua sivustolla tehokkaasti? |
| Transaktiokykyisyys | 25 % | 25 | Voivatko agentit suorittaa kaupallisia toimintoja? |
| **Yhteensä** | **100 %** | **100** | |

### 3.3 Pisteytyshierarkia

#### Löydettävyyspisteet (0–20)

| Tarkistus | Pisteet | Kriteerit |
|-----------|---------|-----------|
| robots.txt agenttiohjeistuksineen | 4 | AI-agenttien user-agentit eksplisiittisesti käsitelty |
| llms.txt olemassa | 3 | Voimassa oleva llms.txt sivuston juuressa |
| XML-sivukartta | 4 | Täydellinen, voimassa oleva, äskettäin päivitetty |
| Schema.org WebSite | 3 | JSON-LD WebSite SearchAction-toiminnolla |
| AAIO-agenttimanifesti | 4 | Voimassa oleva manifesti (ks. luku 5) |
| ai.txt olemassa | 2 | AI-käytäntöilmoitus |

#### Koneluettavuuspisteet (0–35)

| Tarkistus | Pisteet | Kriteerit |
|-----------|---------|-----------|
| Schema.org Product/Service | 8 | Täydellinen JSON-LD kaikille tuotteille/palveluille |
| Hinnoittelu rakenteisessa datassa | 6 | Hinta, valuutta, saatavuus merkinnöissä |
| Datan johdonmukaisuus | 5 | Ei ristiriitoja rakenteisen datan ja sivun sisällön välillä |
| OpenAPI-spesifikaatio | 5 | Dokumentoidut rajapintapäätepisteet |
| Uniikit tunnisteet | 4 | SKU/GTIN/URI kaikille entiteeteille |
| Tuotesyötteet | 4 | Koneluettava luettelo saatavilla |
| Ajallinen tarkkuus | 3 | Hinnat/saatavuus heijastaa nykytilaa |

#### Navigoitavuuspisteet (0–20)

| Tarkistus | Pisteet | Kriteerit |
|-----------|---------|-----------|
| Looginen URL-rakenne | 4 | Ennakoitavat, hierarkkiset polut |
| Leivänmuru-merkinnät | 3 | BreadcrumbList relevanteilla sivuilla |
| Sisäinen hakurajapinta | 4 | Ohjelmoitava haku palauttaa jäsennetyt tulokset |
| Sivutus | 3 | Oikea rel=next/prev -toteutus |
| HTTP-statuskoodit | 3 | Ei pehmeitä 404-virheitä, oikeat uudelleenohjaukset |
| Kategoriataksonomia | 3 | Koneluettava kategoriahierarkia |

#### Transaktiokykyisyyspisteet (0–25)

| Tarkistus | Pisteet | Kriteerit |
|-----------|---------|-----------|
| Koneluettava kassaprosessi | 6 | Kassa käytettävissä ilman JS-renderöintiä |
| API-pohjainen tilaus | 5 | REST/GraphQL-tilauspäätepiste |
| Jäsennetyt käyttöehdot | 3 | Koneella jäsennettävissä olevat ehdot |
| Maksuprotokolla (ACP) | 4 | ACP-yhteensopiva maksuvirta |
| Tilausvahvistus | 3 | Jäsennetty vahvistusvastaus |
| Palautuskäytäntömerkinnät | 2 | Schema.org MerchantReturnPolicy |
| A2A-integraatio | 2 | A2A-protokollatuki agentin neuvottelulle |

### 3.4 Pistetasot

| Pisteet | Taso | Selite | Kuvaus |
|---------|------|--------|--------|
| 0–19 | F | **Ei valmis** | Ei agenttioptimointia; näkymätön AI-agenteille |
| 20–39 | D | **Perus** | Minimaalinen rakenteinen data; agentit löytävät, mutta eivät voi asioida |
| 40–59 | C | **Kehittyvä** | Hyvä löydettävyys ja luettavuus; rajoitettu transaktiokyky |
| 60–79 | B | **Agenttivalmis** | Vahva kaikissa pilareissa; agentit voivat navigoida ja asioida |
| 80–100 | A | **Agenttioptimioitu** | Parhaan luokan toteutus; täysin autonominen agenttikaupankäynti |

---

## 4. Protokollaintegraatio

### 4.1 Protokollalandscape

AAIO toimii optimointikerroksena olemassa olevien protokollien päällä:

```
┌─────────────────────────────────────────────┐
│        AAIO (Optimointikerros)               │
│   "Miten toteuttaa protokollat agenteille"   │
├─────────────┬──────────┬──────────┬──────────┤
│    MCP      │   ACP    │   UCP    │   A2A    │
│  (Konteksti)│(Kauppa)  │(Yhtenäin.)│(Agentti) │
├─────────────┴──────────┴──────────┴──────────┤
│     Webstandardit (HTTP, JSON-LD,             │
│     Schema.org, OpenAPI, OAuth)               │
└───────────────────────────────────────────────┘
```

### 4.2 Model Context Protocol (MCP)

**Rooli AAIO:ssa:** MCP tarjoaa kontekstin jakamisen AI-mallien ja ulkoisten työkalujen/tietolähteiden välillä.

**AAIO-vaatimukset:**
- Sivustojen PITÄISI tarjota MCP-yhteensopivat työkalukuvaukset rajapinnoilleen
- Tuote-/palveludata PITÄISI olla saatavilla MCP-resurssipisteissä
- MCP-palvelintoteutukset PITÄISI noudattaa agenttimanifesti-ilmoitusta

### 4.3 Agent Commerce Protocol (ACP)

**Rooli AAIO:ssa:** ACP käsittelee turvalliset kone-koneiden väliset maksutransaktiot.

**AAIO-vaatimukset:**
- Taso 2+ transaktiokykyä tavoittelevien sivustojen PITÄISI tukea ACP-maksuotsikoita
- Maksuvirtojen TÄYTYY sisältää selkeät vahvistus-/hylkäyssignaalit
- Transaktiokirjanpitoa TÄYTYY ylläpitää auditointitarkoituksiin

### 4.4 Universal Commerce Protocol (UCP)

**Rooli AAIO:ssa:** UCP tarjoaa yhtenäisen datastandardin palvelu- ja tuotetiedoille.

**AAIO-vaatimukset:**
- Tuote-/palveludatan PITÄISI noudattaa UCP-skeemamäärittelyjä soveltuvin osin
- UCP-yhteensopivat syötteet mahdollistavat alustojen välisen agenttivertailun

### 4.5 Agent-to-Agent Protocol (A2A)

**Rooli AAIO:ssa:** A2A mahdollistaa suoran kommunikaation ostaja- ja myyjäagenttien välillä.

**AAIO-vaatimukset:**
- Taso 3 transaktiokykyä tarjoavien sivustojen PITÄISI toteuttaa A2A-yhteensopiva agenttipäätepiste
- A2A-agenttikortteja PITÄISI julkaista osoitteessa `/.well-known/agent.json`

---

## 5. AAIO-agenttimanifesti

### 5.1 Tarkoitus

AAIO-agenttimanifesti on koneluettava JSON-tiedosto, joka ilmoittaa verkkosivuston agenttikyvykkyydet, tuetut protokollat ja käytettävissä olevat päätepisteet. Se toimii sisääntulopisteenä AI-agenteille, jotka löytävät sivuston AAIO-ominaisuuksia.

### 5.2 Sijainti

Manifesti PITÄISI tarjoilla osoitteessa:

```
/.well-known/aaio-manifest.json
```

### 5.3 Esimerkki

```json
{
  "$schema": "https://aaio-standard.org/schemas/aaio-manifest.schema.json",
  "version": "0.1",
  "name": "Esimerkkikauppa",
  "description": "Suomalainen verkkokauppa optimoitu AI-agenteille",
  "url": "https://kauppa.example.fi",
  "contact": "ai-tuki@example.fi",
  "aaioVersion": "0.1",
  "capabilities": {
    "discovery": {
      "robotsTxt": true,
      "llmsTxt": true,
      "aiTxt": true,
      "sitemap": "https://kauppa.example.fi/sitemap.xml",
      "agentManifest": true
    },
    "readability": {
      "schemaOrg": ["Product", "Offer", "Organization", "BreadcrumbList"],
      "openApi": "https://kauppa.example.fi/api/v1/openapi.json",
      "productFeed": "https://kauppa.example.fi/feeds/products.json",
      "dataFormats": ["json-ld", "microdata"]
    },
    "navigation": {
      "searchEndpoint": "https://kauppa.example.fi/api/v1/haku",
      "categoryEndpoint": "https://kauppa.example.fi/api/v1/kategoriat",
      "breadcrumbs": true,
      "pagination": true
    },
    "transaction": {
      "level": "L2",
      "checkoutApi": "https://kauppa.example.fi/api/v1/kassa",
      "cartApi": "https://kauppa.example.fi/api/v1/ostoskori",
      "paymentProtocols": ["acp-v1"],
      "authentication": ["oauth2", "api-key"],
      "tosUrl": "https://kauppa.example.fi/ehdot",
      "returnPolicyUrl": "https://kauppa.example.fi/palautukset"
    }
  },
  "protocols": {
    "mcp": {
      "supported": true,
      "serverUrl": "https://kauppa.example.fi/mcp"
    },
    "a2a": {
      "supported": true,
      "agentCard": "https://kauppa.example.fi/.well-known/agent.json"
    },
    "acp": {
      "supported": true,
      "version": "1.0"
    }
  },
  "rateLimit": {
    "requestsPerMinute": 60,
    "burstLimit": 10
  },
  "lastUpdated": "2026-04-09T00:00:00Z"
}
```

---

## 6. Implementointiopas

### 6.1 Pikakäynnistystarkistuslista

**Vaihe 1: Perusta (Pistetavoite: 20–40)**
- [ ] Lisää Schema.org JSON-LD kaikille tuotteille/palveluille
- [ ] Luo/päivitä `robots.txt` AI-agenttiohjeistuksilla
- [ ] Varmista, että XML-sivukartta on täydellinen ja ajantasainen
- [ ] Validoi, että kaikki hinnoittelu on rakenteisessa datassa

**Vaihe 2: Parannus (Pistetavoite: 40–60)**
- [ ] Luo `llms.txt` sivustoyhteenvedolla
- [ ] Toteuta leivänmuru-merkinnät
- [ ] Lisää sisäinen hakurajapinta (JSON-vastaukset)
- [ ] Julkaise OpenAPI-spesifikaatio
- [ ] Luo AAIO-agenttimanifesti

**Vaihe 3: Kaupankäynti (Pistetavoite: 60–80)**
- [ ] Toteuta API-pohjainen ostoskori/kassaprosessi
- [ ] Lisää koneluettavat käyttöehdot ja palautuskäytäntö
- [ ] Varmista, että kassaprosessi toimii ilman JavaScript-renderöintiä
- [ ] Toteuta tuotesyötteet

**Vaihe 4: Autonomia (Pistetavoite: 80–100)**
- [ ] Toteuta ACP-maksuprotokolla
- [ ] Ota käyttöön A2A-agenttipäätepiste
- [ ] Julkaise MCP-työkalukuvaukset
- [ ] Mahdollista täysin autonomiset transaktiot

### 6.2 Yleisimmät ongelmat

| Ongelma | Vaikutus | Ratkaisu |
|---------|---------|---------|
| Vain JavaScript-renderöinti | Agentit eivät voi lukea sisältöä | Palvelinpuolen renderöinti tai staattinen HTML-varasuunnitelma |
| Ristiriitainen hinnoittelu | Agentin sekaannus, luottamuksen menetys | Yksi totuuden lähde kaikille hinnoille |
| Puuttuva `rel=canonical` | Duplikaattientiteettien sekaannus | Kanonistiset URL:t kaikilla sivuilla |
| CAPTCHA estää agentit | Täydellinen agenttipoissulkeminen | Agenttikohtainen tunnistautuminen (API-avaimet, OAuth) |
| Vanhentuneet sivukartat | Agentit navigoivat 404-virheisiin | Automatisoitu sivukartan generointi |

---

## 7. Turvallisuusnäkökohdat

### 7.1 Agentin tunnistautuminen

Sivustojen PITÄISI toteuttaa porrastettu pääsy:

1. **Julkinen taso**: Tunnistautumaton lukupääsy tuote-/palvelutietoihin
2. **Rekisteröity taso**: API-avainpohjainen pääsy hakuun, syötteisiin ja yksityiskohtaiseen dataan
3. **Transaktionaalinen taso**: OAuth 2.0 tai vastaava kassalle ja maksuille

### 7.2 Nopeusrajoitukset

Sivustojen TÄYTYY toteuttaa nopeusrajoitukset agentiliikenteelle:

- Ilmoita nopeusrajoitukset AAIO-agenttimanifestissa
- Palauta `429 Too Many Requests` `Retry-After`-otsikolla rajojen ylittyessä

### 7.3 Tietosuoja

- Agentin pääsyn TÄYTYY noudattaa GDPR:ää ja soveltuvia tietosuojamääräyksiä
- Henkilökohtaisia tietoja EI SALLITA paljastaa rakenteisen datan tai rajapintojen kautta ilman suostumusta
- Transaktiodatan TÄYTYY olla salattua siirrossa (TLS 1.2+)

---

## 8. Vaatimustenmukaisuus

### 8.1 Vaatimustenmukaisuustasot

| Taso | Nimi | Vaatimukset |
|------|------|-------------|
| **AAIO Basic** | Löydettävyys + Luettavuus | Kaikki PAKKO-vaatimukset pilareista 1–2 |
| **AAIO Standard** | + Navigoitavuus | Kaikki PAKKO-vaatimukset pilareista 1–3 |
| **AAIO Commerce** | + Transaktiokykyisyys L1–L2 | Kaikki PAKKO-vaatimukset kaikista pilareista, L2-transaktio |
| **AAIO Full** | + Autonominen kaupankäynti | Kaikki vaatimukset mukaan lukien L3-transaktio ja protokollaintegraatio |

---

## 9. Tuleva kehitys

- **v0.2**: Muodolliset ACP-integrointivaatimukset
- **v0.3**: Moniagentti-transaktiomallit (agenttiparvit)
- **v0.4**: Rajat ylittävän kaupankäynnin näkökohdat (monivaluutta, monijurisdiktio)
- **v1.0**: Vakaa spesifikaatio toimiala-arvioinnilla

---

## Liite A: Viitteet

- [Schema.org](https://schema.org/) — Rakenteisen datan sanasto
- [OpenAPI Specification](https://spec.openapis.org/oas/latest.html) — Rajapinnan dokumentointistandardi
- [Model Context Protocol](https://modelcontextprotocol.io/) — AI-mallin kontekstin jakaminen
- [A2A Protocol (Linux Foundation)](https://github.com/a2aproject/A2A) — Agenttien välinen kommunikaatio
- [llms.txt Specification](https://llmstxt.org/) — LLM-luettavat sivustoyhteenvedot
- [GDPR](https://gdpr-info.eu/) — EU:n yleinen tietosuoja-asetus

---

*Tämä spesifikaatio on osa [AAIO Standard Draft](../../README.md) -projektia, jonka ylläpitäjä on [Tekoäly-Dani](https://tekoalydani.com).*
