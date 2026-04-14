# SEO-perusta AAIO:lle v0.1

**Status:** Luonnos  
**Versio:** 0.1.0  
**Päivämäärä:** 2026-04-09  
**Tekijät:** [Tekoäly-Dani](https://tekoalydani.com)  
**Lisenssi:** Apache 2.0  
**Yläspesifikaatio:** [AAIO-ydinspesifikaatio v0.1](aaio-core-v0.1.md)  

> 🇬🇧 [English version](../../specs/seo-foundations-v0.1.md)

---

## Tiivistelmä

Search Engine Optimization (SEO) on AIO-pinon perustavanlaatuinen kerros. Jokainen sitä seuraava optimointikerros — AEO, GEO, AAIO — riippuu vahvasta SEO-perustasta. Tämä dokumentti määrittelee SEO-vaatimukset, joiden täytyy olla paikallaan ennen kuin korkeamman tason AI-optimoinnit voivat onnistua, ja erittelee miten perinteiset SEO-käytännöt kehittyvät, kun kohdeyleisö siirtyy ihmisiltä AI-agenteille.

---

## 1. Johdanto

### 1.1 SEO AIO-pinossa

SEO on perustavanlaatuinen kerros (kerros 1 AIO-pinossa) — perusta, jolle kaikki AI-optimointi rakentuu. Ilman kunnollista SEO:ta:

- AI-ryömijät eivät löydä sisältöäsi (AEO epäonnistuu)
- LLM:t eivät voi indeksoida dataasi (GEO epäonnistuu)
- Autonomiset agentit eivät löydä yritystäsi (AAIO epäonnistuu)

```
┌─────────────────────────────────────────┐
│  AAIO  — Autonomiset agentit             │
├─────────────────────────────────────────┤
│  GEO   — Näky tuotetuissa vastauksissa  │
├─────────────────────────────────────────┤
│  AEO   — Tule siteeratuksi              │
├─────────────────────────────────────────┤
│  SEO   — Ole ryömittävissä ja indeksoitu │  ◄── TÄMÄ KERROS
└─────────────────────────────────────────┘
```

### 1.2 SEO vs. AEO vs. GEO vs. AAIO

| Näkökohta | SEO | AEO | GEO | AAIO |
|-----------|-----|-----|-----|------|
| **Ensisijainen yleisö** | Hakukoneiden ryömijät + ihmiset | AI-vastausmoottorit | LLM-tuotettu sisältö | Autonomiset AI-agentit |
| **Tavoite** | Sijoitu hakutuloksissa | Tule siteeratuksi lähteenä | Näky tuotetuissa vastauksissa | Mahdollista löytäminen + transaktio |
| **Keskeinen mittari** | Sijoitukset, orgaaninen liikenne | Viittaustiheys | Sisällyttämisaste | AAIO-valmiuspisteet |
| **Tekninen fokus** | Ryömittävyys, indeksoitavuus | Schema.org, llms.txt | Aiheautoriteetti, E-E-A-T | Agenttimanifesti, protokollapäätepisteet |

---

## 2. SEO:n ydinvaatimukset AAIO:lle

Nämä ovat SEO-perusvaaatimukset, joiden täytyy olla paikallaan ennen korkeampien AIO-kerrosten toteuttamista.

### 2.1 Ryömittävyys

Bottien — sekä perinteisten hakukoneiden että AI-ryömijöiden — kyky käyttää ja lukea sisältöäsi.

| Vaatimus | Prioriteetti | Kuvaus |
|----------|-------------|--------|
| `robots.txt` | PAKKO | Hyvin jäsennetty, sallii sekä hakukoneet että AI-ryömijät |
| Palvelinpuolen renderöinti | PAKKO | Kriittinen sisältö saatavilla ilman JavaScript-suoritusta |
| Vasteaika | PAKKO | TTFB < 500ms sisältösivuille |
| HTTP-statuskoodit | PAKKO | Oikeat 200/301/404/410 (ei pehmeitä 404-virheitä) |
| XML-sivukartta | PAKKO | Täydellinen, voimassa oleva, päivitetty automaattisesti |

#### robots.txt AI-valmiille sivustoille

```
# Perinteiset hakukoneet
User-agent: Googlebot
Allow: /

User-agent: Bingbot
Allow: /

# AI-vastausmoottorit (AEO-kerros)
User-agent: GPTBot
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: PerplexityBot
Allow: /

User-agent: Google-Extended
Allow: /

# AI-ostosaagentit (AAIO-kerros)
User-agent: AAIO-Agent
Allow: /

User-agent: MCP-Client
Allow: /

# Yhteiset esto-säännöt
User-agent: *
Disallow: /admin/
Disallow: /ostoskori/
Disallow: /kassa/
Disallow: /tili/

Sitemap: https://example.com/sitemap.xml
```

### 2.2 Indeksoitavuus

Sisällön täytyy olla indeksoitavissa — hakukoneiden ja AI-järjestelmien täytyy pystyä tallentamaan ja hakemaan se.

| Vaatimus | Prioriteetti | Kuvaus |
|----------|-------------|--------|
| Kanonistiset URL:t | PAKKO | `rel="canonical"` jokaisella sivulla |
| Meta-robots | PAKKO | Oikeat `index`/`noindex`-direktiivit |
| Hreflang | PITÄISI | Monikielisille sivustoille |
| Sivutus | PITÄISI | `rel="next"` / `rel="prev"` sivutetulle sisällölle |
| Duplikaattisisällön eliminointi | PAKKO | Yksi kanonistinen URL per sisältöentiteetti |

### 2.3 Sivustoarkkitehtuuri

| Vaatimus | Prioriteetti | Kuvaus |
|----------|-------------|--------|
| Looginen URL-hierarkia | PAKKO | Ennakoitavat polut (esim. `/tuotteet/kategoria/tuote`) |
| Matala arkkitehtuuri | PITÄISI | Tärkeät sivut enintään 3 klikkausta etusivulta |
| Sisäinen linkitys | PAKKO | Kontekstuaaliset linkit aiheeseen liittyvän sisällön välillä |
| Leivänmuru-navigointi | PITÄISI | `BreadcrumbList` Schema.org -merkinnät |
| URL-johdonmukaisuus | PAKKO | Ei kauttaviivan epäjohdonmukaisuuksia, pienaakkoset URL:t |

### 2.4 Sivukohtainen SEO

| Vaatimus | Prioriteetti | Kuvaus |
|----------|-------------|--------|
| Uniikit otsikkotunnisteet | PAKKO | Kuvaavat, alle 60 merkkiä |
| Metakuvaukset | PITÄISI | Houkuttelevat tiivistelmät, alle 160 merkkiä |
| Otsikkohierarkia | PAKKO | Yksi H1, looginen H2–H6-rakenne |
| Kuvan alt-teksti | PAKKO | Kuvaavat alt-attribuutit kaikissa kuvissa |
| Rakenteinen data | PAKKO | Schema.org JSON-LD (ks. luku 3) |
| Sisällön laatu | PAKKO | E-E-A-T-signaalit (Kokemus, Asiantuntemus, Auktoriteetti, Luotettavuus) |

---

## 3. Rakenteisen datan perusta

Rakenteinen data on kohta, jossa SEO siirtyy kohti AEO:ta ja AAIO:ta. Se on yhteinen vaatimus kaikilla AIO-kerroksilla.

### 3.1 Vaaditut Schema.org-tyypit

Jokaisen AAIO-tavoitteisen sivuston TÄYTYY toteuttaa nämä perus-Schema.org-tyypit:

#### Organization

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Yrityksen nimi",
  "url": "https://example.com",
  "logo": "https://example.com/logo.png",
  "description": "Selkeä, faktuaalinen yrityksen kuvaus",
  "contactPoint": {
    "@type": "ContactPoint",
    "telephone": "+358-XX-XXX-XXXX",
    "contactType": "asiakaspalvelu",
    "availableLanguage": ["Finnish", "English"]
  },
  "sameAs": [
    "https://linkedin.com/company/example",
    "https://twitter.com/example"
  ]
}
```

#### WebSite hakutoiminnolla

```json
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "name": "Esimerkkikauppa",
  "url": "https://example.com",
  "potentialAction": {
    "@type": "SearchAction",
    "target": "https://example.com/haku?q={search_term_string}",
    "query-input": "required name=search_term_string"
  }
}
```

### 3.2 Toimialakohtainen Schema.org

| Toimiala | Vaaditut tyypit |
|----------|----------------|
| Verkkokauppa | `Product`, `Offer`, `AggregateRating`, `Review` |
| SaaS | `SoftwareApplication`, `Offer`, `WebApplication` |
| Ammatilliset palvelut | `Service`, `ProfessionalService`, `Person` (asiantuntijat) |
| Paikallinen yritys | `LocalBusiness`, `PostalAddress`, `OpeningHoursSpecification` |
| Media / Kustannus | `Article`, `TechArticle`, `NewsArticle`, `Person` (tekijä) |

---

## 4. Tekninen SEO AI-valmiudelle

### 4.1 Suorituskyky

| Mittari | Tavoite | Miksi tärkeää AI:lle |
|---------|---------|---------------------|
| TTFB | < 500ms | AI-ryömijöillä on aikakatkaisu-raja |
| LCP | < 2,5s | Core Web Vital hakusijoitusten kannalta |
| CLS | < 0,1 | Asetteluvakaus sisällön poimintaan |

### 4.2 Renderöinti

| Lähestymistapa | SEO-vaikutus | AI-vaikutus | Suositus |
|----------------|-------------|-------------|---------|
| Palvelinpuolen renderöinti (SSR) | Paras | Paras | SUOSITELTU kaikille AAIO-sivustoille |
| Staattinen sivuston generointi (SSG) | Paras | Paras | SUOSITELTU sisältörikkaille sivustoille |
| Asiakaspuolen renderöinti (CSR) | Heikko | Heikoin | EI SUOSITELTU — AI-ryömijät harvoin suorittavat JS:ää |

### 4.3 Turvallisuus

| Vaatimus | Prioriteetti | Kuvaus |
|----------|-------------|--------|
| HTTPS | PAKKO | TLS 1.2+ kaikilla sivuilla |
| HSTS | PITÄISI | HTTP Strict Transport Security -otsake |
| Ei sekasisältöä | PAKKO | Kaikki resurssit ladataan HTTPS:n kautta |

---

## 5. Sisällön SEO-periaatteet

### 5.1 E-E-A-T AI:lle

Googlen E-E-A-T-kehys (Kokemus, Asiantuntemus, Auktoriteetti, Luotettavuus) on kriittinen sekä hakusijoituksille että AI-viittauksille.

| Signaali | SEO-vaikutus | AI-vaikutus | Miten toteuttaa |
|----------|-------------|-------------|----------------|
| **Kokemus** | Kohtalainen | Korkea | Omakohtaiset esimerkit, tapaustutkimukset, alkuperäinen data |
| **Asiantuntemus** | Korkea | Korkea | Tekijän tunnistetiedot, `Person` Schema.org, ammatillinen historia |
| **Auktoriteetti** | Korkea | Kriittinen | Toimialaviittaukset, backlinkit, tunnustettu brändi |
| **Luotettavuus** | Korkea | Kriittinen | Tarkka data, läpinäkyvä viittaus, HTTPS |

### 5.2 Sisältöarkkitehtuuri

| Käytäntö | Kuvaus | AI-hyöty |
|----------|--------|----------|
| Aiheklusterit | Napa-sivu + puhesivut ydinkonseptin ympärillä | Luo aiheautoriteetin LLM:ille |
| Pilari-sisältö | Kattavat, määräävät sivut keskeisistä aiheista | LLM:ien suosima viittausta varten |
| FAQ-integraatio | Kysymys-vastaus-muoto Schema.org FAQPage -merkinnällä | Suoraan vastausmoottoreiden poimittavissa |

### 5.3 Sisällön tuoreus

| Signaali | Toteutus |
|----------|---------|
| `datePublished` Schema.org:ssa | Aseta alkuperäisessä julkaisupäivässä |
| `dateModified` Schema.org:ssa | Päivitä sisällön muuttuessa |
| Sivukartan `<lastmod>` | Tarkat muutospäivämäärät |

---

## 6. SEO:n tarkistuslista AAIO-valmiudelle

### 6.1 Perusta (Vaaditaan ennen AIO-työtä)

- [ ] HTTPS kaikilla sivuilla voimassa olevalla TLS-sertifikaatilla
- [ ] `robots.txt` eksplisiittisillä AI-ryömijäohjeistuksilla
- [ ] XML-sivukartta `/sitemap.xml`-osoitteessa, automaattisesti generoitu
- [ ] Kanonistiset URL:t kaikilla sivuilla
- [ ] Palvelinpuolen renderöinti kaikelle kriittiselle sisällölle
- [ ] Schema.org `Organization` ja `WebSite` etusivulla
- [ ] Uniikit otsikkotunnisteet ja metakuvaukset kaikilla sivuilla
- [ ] Looginen otsikkohierarkia (H1–H6)
- [ ] Alt-teksti kaikissa kuvissa
- [ ] Core Web Vitals "Hyvä"-alueella

### 6.2 Parannus (Vaaditaan AEO/GEO-valmiudelle)

- [ ] Schema.org JSON-LD kaikilla tuote-/palvelusivuilla
- [ ] `BreadcrumbList`-merkinnät navigaatiosivuilla
- [ ] `FAQPage`-merkinnät FAQ/tietokanta-sivuilla
- [ ] `datePublished` ja `dateModified` kaikessa sisällössä
- [ ] `llms.txt` sivuston juuressa
- [ ] `ai.txt` AI-käytäntöilmoitus
- [ ] Tekijän `Person`-merkinnät tunnistetiedoilla

### 6.3 Edistynyt (Vaaditaan täydelle AAIO-pinolle)

- [ ] OpenAPI-spesifikaatio sivuston rajapinnoille
- [ ] `SearchAction` WebSite Schema.org:ssa
- [ ] Tuote-/palvelusyötteet koneluettavassa muodossa
- [ ] AAIO-agenttimanifesti `/.well-known/aaio-manifest.json`-osoitteessa
- [ ] A2A-agenttikortti `/.well-known/agent.json`-osoitteessa
- [ ] MCP-yhteensopivat työkalukuvaukset

---

## 7. Yleiset SEO-ongelmat, jotka rikkovat AI-optimoinnin

| Ongelma | AI-vaikutus | Ratkaisu |
|---------|------------|---------|
| Vain JavaScript-renderöinti | AI-ryömijät eivät voi lukea sisältöä | Palvelinpuolen renderöinti |
| CAPTCHA sisältösivuilla | Estää kaiken automatisoidun pääsyn | Agenttikohtainen tunnistautuminen (API-avaimet) |
| Ääretön vieritys ilman sivutusta | Ryömijät eivät löydä taitteen alapuolista sisältöä | Sivutetut URL:t `rel`-linkeillä |
| Dynaamiset URL:t istunto-ID:illä | Duplikaattisisältö, ryömimisen tuhlailu | Puhtaat kanonistiset URL:t |
| Vanhentunut sisältö | Vähentyneet tuoreussignaalit | Säännölliset sisältöpäivitykset `dateModified`-merkinnällä |

---

## 8. Suhde korkeampiin AIO-kerroksiin

### 8.1 SEO → AAIO -polku

```
SEO-perusta         →  Ryömittävissa, indeksoitavissa, rakenteinen
  + AEO-parannus    →  Siteerattavissa vastausmoottoreissa
    + GEO-autoriteetti → Sisällytetty tuotettuun sisältöön
      + AAIO-kaupankäynti → Agentit voivat löytää ja asioida
```

Jokainen kerros on kumulatiivinen. Kerrosten ohittaminen luo hauraita optimointeja, jotka epäonnistuvat AI-agenttien tarkastellessa digitaalista läsnäoloasi kokonaisvaltaisesti.

---

## Liite A: Viitteet

- [Google Search Central](https://developers.google.com/search) — Virallinen SEO-dokumentaatio
- [Schema.org](https://schema.org/) — Rakenteisen datan sanasto
- [Web Vitals](https://web.dev/vitals/) — Core Web Vitals -dokumentaatio
- [Google E-E-A-T Guidelines](https://developers.google.com/search/docs/fundamentals/creating-helpful-content) — Sisällön laadun kehys
- [llms.txt Specification](https://llmstxt.org/) — LLM-luettavat sivustoyhteenvedot
- [AAIO Core Specification](aaio-core-v0.1.md) — AAIO:n ydinstandardi

---

*Tämä dokumentti on osa [AAIO Standard Draft](../../README.md) -projektia, jonka ylläpitäjä on [Tekoäly-Dani](https://tekoalydani.com).*
