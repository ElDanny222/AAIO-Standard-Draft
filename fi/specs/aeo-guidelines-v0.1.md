# AEO-parhaat käytännöt v0.1

**Status:** Luonnos  
**Versio:** 0.1.0  
**Päivämäärä:** 2026-04-09  
**Tekijät:** [Tekoäly-Dani](https://tekoalydani.com)  
**Lisenssi:** Apache 2.0  
**Yläspesifikaatio:** [AAIO-ydinspesifikaatio v0.1](aaio-core-v0.1.md)  

> 🇬🇧 [English version](../../specs/aeo-guidelines-v0.1.md)

---

## Tiivistelmä

Answer Engine Optimization (AEO) on käytäntö, jolla optimoidaan verkkosisältöä niin, että tekoälyvastausmoottorit (ChatGPT, Perplexity, Gemini, Copilot) viittaavat siihen auktoritatiivisena lähteenä. AEO on AIO-pinon toinen kerros, joka rakentuu SEO-perustan päälle ja mahdollistaa GEO:n ja AAIO:n korkeammat kerrokset.

---

## 1. Johdanto

### 1.1 Mitä AEO on?

AEO optimoi sisällön uudelle hakuluokalle: **AI-vastausmoottoreille**, jotka syntetisoivat vastauksia useista lähteistä. Toisin kuin perinteiset hakukoneet, jotka palauttavat linkkejä, vastausmoottorit palauttavat suoria vastauksia — ja viittaavat lähteisiinsä. Viitattuna oleminen tarkoittaa liikennettä, auktoriteettia ja luottamusta.

### 1.2 Miksi AEO on tärkeää

- **AI-vastausmoottorit kasvavat**: ChatGPT, Perplexity, Gemini ja Copilot palvelevat satoja miljoonia kyselyitä kuukausittain
- **Viittaus = auktoriteetti**: Viitattuna oleminen asemoi brändin tietyn aihealueen määräävänä lähteenä
- **AAIO:n perusta**: AI-ostosaagentit käyttävät samoja tietolähteistä — AEO-näkyvyys ruokkii suoraan agenttien löydettävyyttä

### 1.3 AEO vs. SEO vs. GEO

| Näkökohta | SEO | AEO | GEO |
|-----------|-----|-----|-----|
| **Kohde** | Hakukoneiden ryömijät | AI-vastausmoottorit | AI:n tuottamat syntetisoidut vastaukset |
| **Tavoite** | Sijoitu hakutuloksissa | Tule siteeratuksi lähteenä | Näky tuotetuissa vastauksissa |
| **Sisältömuoto** | Avainsanat, linkit, metatagit | Jäsennetty, faktuaalinen, auktoritatiivinen | Kattava, hyvin jäsennetty |
| **Mittaus** | Sijoitukset, CTR | Viittaustiheys | Sisällyttämisaste generoituun sisältöön |

---

## 2. Sisältöstrategia LLM-näkyvyyteen

### 2.1 Ydinperiaatteet

1. **Ole määräävä lähde**: LLM:t suosivat kattavaa, täsmällistä ja auktoritatiivista sisältöä
2. **Vastaa kysymyksiin suoraan**: Jäsennä sisältö yleisösi kysymysten ympärille
3. **Ilmoita faktat, ei mielipiteet**: LLM:t viittaavat faktuaalisiin, todennettaviin väitteisiin subjektiivisen sisällön sijaan
4. **Ole ajantasainen**: Tuoreussignaalit ovat tärkeitä — päivitä sisältöä säännöllisesti ajankohtaisella datalla
5. **Ole täsmällinen**: Konkreettiset numerot, päivämäärät ja esimerkit ovat enemmän viitattavissa kuin epämääräiset lausunnot

### 2.2 Sisältömuodot, joita LLM:t suosivat

| Muoto | Miksi LLM:t suosivat sitä | Esimerkki |
|-------|--------------------------|---------|
| **Määritelmäkappaleet** | Selkeä, viitattavissa oleva vastaus "mikä on X?" -kysymykseen | "AAIO (Agentic AI Optimization) on optimointikerros, joka..." |
| **Vertailutaulukot** | Jäsennetty, helposti poimittava | Ominaisuusvertailutaulukot selkeillä otsikoilla |
| **Vaiheittaiset listat** | Proseduraalinen tieto arvostetaan korkealle | "Miten toteuttaa Schema.org: 1. Valitse merkintätyyppi..." |
| **FAQ-osiot** | Suora kysymys-vastaus -kartoitus | Kysymys-vastaus -parit Schema.org FAQPage -merkinnällä |
| **Tilastot lähteillä** | Todennettavissa olevat datapisteet | "AI-optimointimarkkina on 7,3 miljardia euroa (2026, Gartner)" |

### 2.3 Sisällön ongelmat

Vältä näitä malleja, jotka vähentävät LLM-siteerattavuutta:

- **Klikkiotsikot**: "Et usko..." — LLM:t eivät klikkaa
- **Ohut sisältö**: Sivut, joilla on alle 300 sanaa oleellista sisältöä
- **Duplikaattisisältö**: Sama tieto useilla sivuilla
- **Portin takainen sisältö**: LLM-ryömijät eivät pysty kirjautumaan sisään
- **Vain kuvateksti**: Kuvien teksti ei ole useimpien LLM-ryömijöiden poimittavissa
- **Vain dynaamisesti generoitu sisältö**: JavaScript-renderöity sisältö ei välttämättä ryömi

---

## 3. Rakenteinen data AEO:lle

### 3.1 Tärkeimmät Schema.org-tyypit

#### FAQPage

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "Mitä AAIO on?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "AAIO (Agentic AI Optimization) on optimointikerros, joka määrittelee miten verkkosivustot tulee rakentaa, jotta autonomiset AI-agentit voivat löytää, ymmärtää, navigoida ja asioida niiden kanssa."
      }
    }
  ]
}
```

#### Article / TechArticle

```json
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "headline": "AAIO-ydinspesifikaatio v0.1",
  "author": {
    "@type": "Organization",
    "name": "Tekoäly-Dani"
  },
  "datePublished": "2026-04-09",
  "dateModified": "2026-04-09",
  "description": "Tekninen spesifikaatio Agentic AI Optimization -standardille",
  "proficiencyLevel": "Expert"
}
```

#### HowTo

```json
{
  "@context": "https://schema.org",
  "@type": "HowTo",
  "name": "Miten toteuttaa AAIO verkkokaupallesi",
  "step": [
    {
      "@type": "HowToStep",
      "name": "Lisää Schema.org-merkinnät",
      "text": "Lisää JSON-LD Product ja Offer -merkinnät kaikille tuotesivuille"
    },
    {
      "@type": "HowToStep",
      "name": "Luo llms.txt",
      "text": "Luo LLM-luettava sivustoyhteenveto /llms.txt-osoitteeseen"
    }
  ]
}
```

### 3.2 Schema.org-validointi

- Validoi kaikki merkinnät [Google Rich Results Test](https://search.google.com/test/rich-results) -työkalulla
- Varmista, ettei rakenteisessa datassa ole virheitä tai varoituksia
- Tarkista, että kaikki vaaditut kentät on täytetty
- Varmista, että JSON-LD on läsnä sivun lähdekoodissa (ei vain dynaamisesti renderöitynä)

---

## 4. Tekniset AEO-vaatimukset

### 4.1 Ryömittävyys AI-agenteille

| Vaatimus | Toteutus |
|----------|---------|
| Salli AI-ryömijät `robots.txt`:ssä | `User-agent: GPTBot`, `User-agent: ClaudeBot` jne. `Allow`-säännöillä |
| Tarjoile staattinen HTML | Palvelinpuolen renderöinti tai esirenderöinti kriittiselle sisällölle |
| Nopeat vasteajat | Tavoite < 500ms TTFB sisältösivuille |
| `llms.txt` | LLM-luettava sivustoyhteenveto [llmstxt.org](https://llmstxt.org/) -spesifikaation mukaan |
| `ai.txt` | AI-käytäntöilmoitus, jossa kerrotaan sallittu AI-käyttö |

### 4.2 llms.txt-rakenne

`llms.txt`-tiedoston PITÄISI sisältää:

```markdown
# Sivuston nimi

> Lyhyt sivuston kuvaus (1-2 lausetta)

## Avainaiheet
- Aihe 1: Lyhyt kuvaus
- Aihe 2: Lyhyt kuvaus

## Tärkeimmät sivut
- [Sivun otsikko](URL): Kuvaus
- [Sivun otsikko](URL): Kuvaus

## Yhteystiedot
- Nimi, rooli, sähköposti
```

### 4.3 Sisällön tuoreussignaalit

LLM:t huomioivat tuoreuden lähteitä valittaessa:

1. **`dateModified` Schema.org:ssa**: Päivitä kun sisältö muuttuu
2. **Last-Modified HTTP -otsake**: Aseta oikein kaikille sisältösivuille
3. **Sivukartan `<lastmod>`**: Tarkat muutospäivämäärät sivukartassa
4. **Näkyvät päivämäärät sivulla**: "Päivitetty viimeksi: VVVV-KK-PP" näkyvässä sisällössä

---

## 5. AEO-mittaus

### 5.1 Avainmittarit

| Mittari | Kuvaus | Miten mitata |
|---------|--------|-------------|
| **Viittaustiheys** | Kuinka usein sisältöäsi siteerataan AI-moottoreissa | Seuraa brändin mainintoja ChatGPT:n, Perplexityn, Geminin vastauksissa |
| **Viittaustarkkuus** | Onko siteerattu tieto oikein | Tarkista AI:n tuottamat viittaukset sisältöäsi vastaan |
| **Ryömijöiden käyntitiheys** | Kuinka usein AI-ryömijät vierailevat | Analysoi palvelinlokeja AI-agenttien user-agenteista |
| **Rakenteisen datan kattavuus** | Sivujen prosenttiosuus voimassa olevalla Schema.org:lla | Automaattinen validointi |

---

## 6. AEO-tarkistuslista

### 6.1 Pikakäynnistys (1 viikko)

- [ ] Tarkista ja päivitä `robots.txt` AI-ryömijöille
- [ ] Lisää Schema.org `Organization` ja `WebSite` JSON-LD etusivulle
- [ ] Luo `llms.txt` sivustoyhteenvedolla
- [ ] Varmista, että kaikilla avain-sivuilla on `dateModified` Schema.org:ssa
- [ ] Lisää `FAQPage`-merkinnät FAQ/tietokantasivuille

### 6.2 Perusta (1 kuukausi)

- [ ] Lisää Schema.org-merkinnät kaikille tuote-/palvelusivuille
- [ ] Luo kattava FAQ-sisältö 20 tärkeimmälle toimialasi kysymykselle
- [ ] Toteuta palvelinpuolen renderöinti kriittisille sisältösivuille
- [ ] Aseta AI-ryömijöiden seuranta palvelinlokeissa
- [ ] Luo `ai.txt` AI-käyttökäytännöllä

### 6.3 Edistynyt (jatkuva)

- [ ] Luo sisällönpäivitystahti (kuukausittain minimissään avain-sivuille)
- [ ] Rakenna aiheautoriteetti: luo kattavia sisältöklustereita
- [ ] Seuraa viittaustiheyttä tärkeimmissä AI-vastausmoottoreissa
- [ ] Testaa sisältömuotoja viitattavuutta varten

---

## 7. Toimialakohtaiset ohjeet

### 7.1 Verkkokauppa

- Lisää `Product`, `Offer` ja `AggregateRating` kaikille tuotesivuille
- Lisää vertailutaulukoita tuotekategorioihin
- Julkaise ostooppaita rakenteisella datalla
- Varmista, että hinnoittelu on aina ajantasaista rakenteisessa datassa

### 7.2 SaaS / Teknologia

- Lisää `SoftwareApplication` Schema.org -tuotesivuille
- Luo yksityiskohtaisia ominaisuusvertailusivuja
- Dokumentoi rajapintapäätepisteet OpenAPI-spesifikaatiolla
- Julkaise teknistä dokumentaatiota `TechArticle`-merkinnällä

### 7.3 Ammatilliset palvelut

- Lisää `Service` ja `ProfessionalService` -merkinnät
- Luo tapaustutkimuksia mitattavilla tuloksilla
- Julkaise asiantuntijasisältöä `Person`-tekijämerkinnällä
- Sisällytä hinnoittelu-/tuntiveloitustiedot rakenteisessa datassa

### 7.4 Paikallinen yritys

- Lisää `LocalBusiness`-merkintä tarkoilla NAP-tiedoilla (nimi, osoite, puhelin)
- Julkaise palvelualuetiedot rakenteisessa datassa
- Sisällytä aukioloajat Schema.org:ssa
- Luo sijaintikohtaisia sisältösivuja

---

## Liite A: AI-vastausmoottoreiden ryömijäviite

| Moottori | User-Agent | Dokumentaatio |
|---------|------------|---------------|
| OpenAI / ChatGPT | `GPTBot` | [OpenAI GPTBot](https://platform.openai.com/docs/gptbot) |
| Anthropic / Claude | `ClaudeBot` | [Anthropic ClaudeBot](https://docs.anthropic.com/en/docs/claude-bot) |
| Google / Gemini | `Google-Extended` | [Google AI Crawler](https://developers.google.com/search/docs/crawling-indexing/overview-google-crawlers) |
| Perplexity | `PerplexityBot` | [Perplexity Bot](https://docs.perplexity.ai/guides/perplexity-bot) |
| Apple | `Applebot-Extended` | [Apple Bot](https://support.apple.com/en-us/111867) |

---

*Tämä dokumentti on osa [AAIO Standard Draft](../../README.md) -projektia, jonka ylläpitäjä on [Tekoäly-Dani](https://tekoalydani.com).*
