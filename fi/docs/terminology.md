# Termistö

**Status:** Luonnos  
**Versio:** 0.1.0  
**Päivämäärä:** 2026-04-09  
**Tekijät:** [Tekoäly-Dani](https://tekoalydani.com)  

> 🇬🇧 [English version](../../docs/terminology.md)

Tämä sanasto määrittelee AAIO-standardissa ja sen tukidokumenteissa käytetyt keskeiset termit.

---

## Optimointitasot

### AIO — AI Optimization / Tekoälyoptimointi

Sateenvarjotermi kaikelle tekoälyoptimoinnille. Sisältää AEO:n, GEO:n ja AAIO:n aladisipliineinä. Käytetään yleisenä markkinointiterminä viitattaessa koko AI-optimointipinoon.

**Katso myös:** [AIO Framework](../../specs/aio-framework-v0.1.md)

### AEO — Answer Engine Optimization / Vastausmoottorioptimointi

Käytäntö, jolla optimoidaan verkkosisältöä niin, että tekoälyvastausmoottorit (ChatGPT, Perplexity, Gemini, Copilot) viittaavat siihen auktoritatiivisena lähteenä. AEO on AIO-pinon toinen kerros, joka rakentuu SEO:n päälle.

**Katso myös:** [AEO Best Practices](../../specs/aeo-guidelines-v0.1.md)

### GEO — Generative Engine Optimization / Generatiivisten moottoreiden optimointi

Sisällön optimointi näkymään tekoälyn tuottamissa syntetisoiduissa vastauksissa. GEO keskittyy siihen, että sisältö sisällytetään itse generoituun tekstiin, ei vain lähteenä viittaamiseen.

**Katso myös:** [GEO Guidelines](../../specs/geo-guidelines-v0.1.md)

### AAIO — Agentic AI Optimization / Autonomisten tekoälyagenttien optimointi

AIO-pinon kehittynein kerros. AAIO määrittelee, miten verkkosivustot ja digitaaliset palvelut tulee rakentaa, jotta autonomiset tekoälyagentit voivat löytää, ymmärtää, navigoida ja asioida niiden kanssa. AAIO on optimointikerros, **ei uusi protokolla** — se määrittelee, miten olemassa olevia protokollia ja verkkostandardeja tulisi toteuttaa optimaalisen agentti-yhteentoimivuuden saavuttamiseksi.

**Keskeinen suhde:** AAIO ei korvaa SEO:ta, AEO:ta tai GEO:ta — ne kasaantuvat kumulatiivisesti.

**Katso myös:** [AAIO Core Specification](../../specs/aaio-core-v0.1.md)

### AXO — Agent Experience Optimization / Agenttikokemusoptimointi

UX/CX-näkökulma AAIO:on. AXO kehystää agenttioptimoinnin sen kautta, miten tekoälyagentit kokevat verkkosivuston — suunniteltu UX/CX-päättäjille. AXO on sama AAIO-työ esitettynä eri yleisölle.

**Käyttö:** Käytä AAIO:ta teknisille yleisöille, AXO:a UX/CX-yleisöille, AIO:ta yleisenä markkinointiterminä.

**Katso myös:** [AXO Framework](../../specs/axo-framework-v0.1.md)

---

## Protokollat

### MCP — Model Context Protocol / Mallikontekstiprotokolla

Protokolla kontekstin jakamiseen tekoälymallien ja ulkoisten työkalujen/datalähteiden välillä. Anthropicin kehittämä. Mahdollistaa tekoälyagenttien pääsyn ulkoiseen dataan standardoitujen työkalurajapintojen kautta.

**Viite:** [modelcontextprotocol.io](https://modelcontextprotocol.io/)

### ACP — Agent Commerce Protocol / Agenttikauppaprotokolla

Protokolla turvallisille kone-koneiden välisille maksutransaktioille tekoälyagenttien ja verkkokauppajärjestelmien välillä. Käsittelee maksuotsikoita, transaktioturvallisuutta ja vahvistussignaaleja. Stripe & OpenAI (Apache 2.0).

**Katso myös:** [ACP Integration Guide](../../specs/acp-integration-v0.1.md)

### UCP — Universal Commerce Protocol / Universaali kauppaprotokolla

Yhtenäinen datastandardi tuote- ja palvelutiedoille, suunniteltu mahdollistamaan tekoälyagenttien vertailut eri alustojen välillä käyttäen johdonmukaista dataformaattia.

**Katso myös:** [UCP Integration Guide](../../specs/ucp-integration-v0.1.md)

### A2A — Agent-to-Agent Protocol / Agentti-agenttiprotokolla

Protokolla, joka mahdollistaa suoran viestinnän tekoälyagenttien välillä (esim. ostajagentti ↔ myyjäagentti). Tukee tehtäväpohjaisia vuorovaikutusmalleja, kuten neuvottelu, delegointi ja tilanseuranta. Googlen kehittämä, nyt Linux Foundationin alla.

**Viite:** [github.com/a2aproject/A2A](https://github.com/a2aproject/A2A)

**Katso myös:** [A2A Commerce Profile](../../specs/a2a-commerce-v0.1.md)

---

## AAIO-konseptit

### AAIO Readiness Model / AAIO-valmiusmalli

Neljän pilarin malli, joka määrittelee, mitkä kyvykkyydet verkkosivustolla tulee olla optimaalisen agentti-yhteentoimivuuden saavuttamiseksi:

1. **Löydettävyys** (Discovery) — voivatko agentit löytää sinut?
2. **Koneluettavuus** (Machine-Readability) — voivatko agentit ymmärtää datasi?
3. **Navigoitavuus** (Navigability) — voivatko agentit liikkua sivustollasi?
4. **Transaktiokyky** (Transactability) — voivatko agentit ostaa sinulta?

### AAIO Readiness Score / AAIO-valmiuspisteet

Kvantitatiivinen mittari (0–100), joka arvioi, kuinka hyvin verkkosivusto on optimoitu autonomisille tekoälyagenteille. Koostuu neljästä kategoriasta:
- Löydettävyys (20 %)
- Koneluettavuus (35 %)
- Navigoitavuus (20 %)
- Transaktiokyky (25 %)

### Agent Manifest / Agenttimanifesti

Koneluettava JSON-tiedosto, joka tarjoillaan osoitteessa `/.well-known/aaio-manifest.json` ja joka ilmoittaa verkkosivuston agenttikyvykkyydet, tuetut protokollat ja käytettävissä olevat päätepisteet. Sisääntulopiste tekoälyagenteille, jotka löytävät sivuston AAIO-ominaisuuksia.

### Transaction Maturity Levels / Transaktiokypsyystasot

Neliportainen asteikko (L0–L3), joka luokittelee verkkosivuston kyvyn tukea agenttivälitteisiä transaktioita:

| Taso | Nimi | Kuvaus |
|------|------|--------|
| L0 | Vain tiedot | Agentti voi lukea dataa, mutta ei voi asioida |
| L1 | Ostoskorivalmis | Agentti voi lisätä tuotteita API:n kautta |
| L2 | Kassavalmis | Agentti voi suorittaa kassan (maksu vaatii ihmisen hyväksynnän) |
| L3 | Täysin autonominen | Agentti voi suorittaa koko transaktion mukaan lukien maksun |

---

## Tekniset termit

### Schema.org

Yhteisöllinen sanasto rakenteelliselle datalle verkossa. Käytetään AAIO:ssa tuotteiden, palveluiden, organisaatioiden ja muiden entiteettien merkitsemiseen koneluettavassa muodossa (tyypillisesti JSON-LD).

**Viite:** [schema.org](https://schema.org/)

### JSON-LD — JavaScript Object Notation for Linked Data

Suositeltu formaatti Schema.org-rakenteellisen datan upottamiseen verkkosivuille. Upotetaan `<script type="application/ld+json">` -tagiin sivun HTML:ssä.

### OpenAPI

Spesifikaatio RESTful API:en dokumentointiin. AAIO-kontekstissa käytetään kuvaamaan verkkosivuston ohjelmallisia päätepisteitä, joita agentit voivat käyttää hakuun, tuotedataan ja transaktioihin.

**Viite:** [spec.openapis.org](https://spec.openapis.org/oas/latest.html)

### llms.txt

Tekstimuotoinen tiedosto sivuston juuressa (`/llms.txt`), joka tarjoaa LLM-luettavan yhteenvedon verkkosivustosta. Noudattaa [llmstxt.org](https://llmstxt.org/) -spesifikaatiota.

### ai.txt

Tekstimuotoinen tiedosto sivuston juuressa (`/ai.txt`), joka ilmoittaa sivuston tekoälyn käyttöpolitiikan — mitä tekoälyjärjestelmät saavat tehdä sivuston sisällöllä.

### A2A Agent Card

JSON-tiedosto, joka tarjoillaan osoitteessa `/.well-known/agent.json` ja joka ilmoittaa A2A-yhteensopivan agentin kyvykkyydet, tuetut taidot ja vuorovaikutuspäätepisteet. Osa A2A-protokollaa.

---

## Liiketoimintakonteksti

### AI Agent / Tekoälyagentti

Autonominen ohjelmistoentiteetti, joka toimii käyttäjän puolesta tavoitteen saavuttamiseksi. AAIO-kontekstissa tyypillisesti ostoagentti, joka tutkii, vertailee ja ostaa tuotteita tai palveluita.

### Purchase Agent / Ostoagentti

Tekoälyagentti, jonka tehtävänä on löytää, vertailla ja ostaa tuotteita tai palveluita ihmiskäyttäjän puolesta.

### Agent-Mediated Commerce / Agenttivälitteinen kaupankäynti

Kaupankäynti, jossa ostajan tekoälyagentti suorittaa osan tai koko ostoprosessin (tutkimus, vertailu, neuvottelu, transaktio) autonomisesti.

### Agent Journey / Agenttipolku

Tekoälyagentin toimintojen sarja ensimmäisestä sivuston löytämisestä valmiin transaktion suorittamiseen — analoginen ihmisen asiakaspolulle.

---

## Lyhenneluettelo

| Lyhenne | Koko nimi (EN) | Koko nimi (FI) |
|---------|----------------|-----------------|
| A2A | Agent-to-Agent | Agentti-agentti |
| AAIO | Agentic AI Optimization | Autonomisten tekoälyagenttien optimointi |
| ACP | Agent Commerce Protocol | Agenttikauppaprotokolla |
| AEO | Answer Engine Optimization | Vastausmoottorioptimointi |
| AIO | AI Optimization | Tekoälyoptimointi |
| AXO | Agent Experience Optimization | Agenttikokemusoptimointi |
| CX | Customer Experience | Asiakaskokemus |
| GEO | Generative Engine Optimization | Generatiivisten moottoreiden optimointi |
| JSON-LD | JavaScript Object Notation for Linked Data | — |
| MCP | Model Context Protocol | Mallikontekstiprotokolla |
| SEO | Search Engine Optimization | Hakukoneoptimointi |
| UCP | Universal Commerce Protocol | Universaali kauppaprotokolla |
| UX | User Experience | Käyttäjäkokemus |

---

*Tämä sanasto on osa [AAIO Standard Draft](../../README.md) -projektia, jonka ylläpitäjä on [Tekoäly-Dani](https://tekoalydani.com).*
