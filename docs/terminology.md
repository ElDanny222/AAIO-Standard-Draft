# Termistö / Terminology

**Status:** Draft  
**Version:** 0.1.0  
**Date:** 2026-04-09  
**Authors:** [Tekoäly-Dani](https://tekoalydani.com)  

Tämä sanasto määrittelee AAIO-standardissa ja sen tukidokumenteissa käytetyt keskeiset termit. Termit on esitetty sekä suomeksi että englanniksi.

This glossary defines key terms used in the AAIO Standard and its supporting documents. Terms are provided in both Finnish and English.

---

## Optimointitasot / Optimization Layers

### AIO — AI Optimization / Tekoälyoptimointi

**EN:** Umbrella term for all AI optimization practices. Includes AEO, GEO, and AAIO as sub-disciplines. Use as a general marketing term when referring to the full AI optimization stack.

**FI:** Sateenvarjotermi kaikelle tekoälyoptimoinnille. Sisältää AEO:n, GEO:n ja AAIO:n aladisipliineinä. Käytetään yleisenä markkinointiterminä viitattaessa koko AI-optimointipinoon.

### AEO — Answer Engine Optimization / Vastausmoottorioptimointi

**EN:** The practice of optimizing web content so that AI answer engines (ChatGPT, Perplexity, Gemini, Copilot) cite it as an authoritative source. AEO is the second layer of the AIO stack, building on SEO foundations.

**FI:** Käytäntö, jolla optimoidaan verkkosisältöä niin, että tekoälyvastausmoottorit (ChatGPT, Perplexity, Gemini, Copilot) viittaavat siihen auktoritatiivisena lähteenä. AEO on AIO-pinon toinen kerros, joka rakentuu SEO:n päälle.

**See also:** [AEO Best Practices](../specs/aeo-guidelines-v0.1.md)

### GEO — Generative Engine Optimization / Generatiivisten moottoreiden optimointi

**EN:** Optimizing content to appear in AI-generated synthesized answers. GEO focuses on being included in the generated text itself, not just cited as a source.

**FI:** Sisällön optimointi näkymään tekoälyn tuottamissa syntetisoiduissa vastauksissa. GEO keskittyy siihen, että sisältö sisällytetään itse generoituun tekstiin, ei vain lähteenä viittaamiseen.

### AAIO — Agentic AI Optimization / Autonomisten tekoälyagenttien optimointi

**EN:** The most advanced layer of the AIO stack. AAIO defines how websites and digital services should be structured so that autonomous AI agents can discover, understand, navigate, and transact with them. AAIO is an optimization layer, NOT a new protocol — it specifies how existing protocols and web standards should be implemented for optimal agent interoperability.

**FI:** AIO-pinon kehittynein kerros. AAIO määrittelee, miten verkkosivustot ja digitaaliset palvelut tulee rakentaa, jotta autonomiset tekoälyagentit voivat löytää, ymmärtää, navigoida ja asioida niiden kanssa. AAIO on optimointikerros, EI uusi protokolla — se määrittelee, miten olemassa olevia protokollia ja verkkostandardeja tulisi toteuttaa optimaalisen agentti-yhteentoimivuuden saavuttamiseksi.

**Key relationship / Keskeinen suhde:** AAIO does NOT replace SEO, AEO, or GEO — they stack cumulatively. / AAIO EI korvaa SEO:ta, AEO:ta tai GEO:ta — ne kasaantuvat kumulatiivisesti.

**See also:** [AAIO Core Specification](../specs/aaio-core-v0.1.md)

### AXO — Agent Experience Optimization / Agenttikokemusoptimointi

**EN:** The UX/CX perspective on AAIO. AXO frames agent optimization through the lens of how AI agents experience a website — designed for UX/CX decision-makers. AXO is the same underlying AAIO work, presented for a different audience.

**FI:** UX/CX-näkökulma AAIO:on. AXO kehystää agenttioptimoinnin sen kautta, miten tekoälyagentit kokevat verkkosivuston — suunniteltu UX/CX-päättäjille. AXO on sama AAIO-työ, esitettynä eri yleisölle.

**Usage / Käyttö:** Use AAIO for technical audiences, AXO for UX/CX audiences, AIO as the general marketing term. / Käytä AAIO:ta teknisille yleisöille, AXO:a UX/CX-yleisöille, AIO:ta yleisenä markkinointiterminä.

**See also:** [AXO Framework](../specs/axo-framework-v0.1.md)

---

## Protokollat / Protocols

### MCP — Model Context Protocol / Mallikontekstiprotokolla

**EN:** Protocol for sharing context between AI models and external tools/data sources. Developed by Anthropic. Enables AI agents to access and use external data through standardized tool interfaces.

**FI:** Protokolla kontekstin jakamiseen tekoälymallien ja ulkoisten työkalujen/datalähteiden välillä. Anthropicin kehittämä. Mahdollistaa tekoälyagenttien pääsyn ulkoiseen dataan standardoitujen työkalurajapintojen kautta.

**Reference:** [modelcontextprotocol.io](https://modelcontextprotocol.io/)

### ACP — Agent Commerce Protocol / Agenttikauppaprotokolla

**EN:** Protocol for secure machine-to-machine payment transactions between AI agents and e-commerce systems. Handles payment headers, transaction security, and confirmation signals.

**FI:** Protokolla turvallisille kone-koneiden välisille maksutransaktioille tekoälyagenttien ja verkkokauppajärjestelmien välillä. Käsittelee maksuotsikoita, transaktiourvaa ja vahvistussignaaleja.

### UCP — Universal Commerce Protocol / Universaali kauppaprotokolla

**EN:** Unified data standard for product and service information, designed to enable AI agents to compare offerings across different platforms using a consistent data format.

**FI:** Yhtenäinen datastandardi tuote- ja palvelutiedoille, suunniteltu mahdollistamaan tekoälyagenttien vertailut eri alustojen välillä käyttäen johdonmukaista dataformaattia.

### A2A — Agent-to-Agent Protocol / Agentti-agenttiprotokolla

**EN:** Protocol enabling direct communication between AI agents (e.g., buyer agent ↔ seller agent). Supports task-based interaction patterns including negotiation, delegation, and status tracking. Developed by Google.

**FI:** Protokolla, joka mahdollistaa suoran viestinnän tekoälyagenttien välillä (esim. ostajagentti ↔ myyjäagentti). Tukee tehtäväpohjaisia vuorovaikutusmalleja, kuten neuvottelu, delegointi ja tilanseuranta. Googlen kehittämä.

**Reference:** [github.com/google/A2A](https://github.com/google/A2A)

---

## AAIO-konseptit / AAIO Concepts

### AAIO Readiness Model / AAIO-valmiusmalli

**EN:** The four-pillar model that defines what capabilities a website must have for optimal agent interoperability: Discovery, Machine-Readability, Navigability, and Transactability.

**FI:** Neljän pilarin malli, joka määrittelee, mitkä kyvykkyydet verkkosivustolla tulee olla optimaalisen agentti-yhteentoimivuuden saavuttamiseksi: Löydettävyys, Koneluettavuus, Navigoitavuus ja Transaktiokyky.

### AAIO Readiness Score / AAIO-valmiuspisteet

**EN:** A quantitative measure (0–100) evaluating how well a website is optimized for autonomous AI agents. Composed of four category scores: Discovery (20%), Machine-Readability (35%), Navigability (20%), and Transactability (25%).

**FI:** Kvantitatiivinen mittari (0–100), joka arvioi, kuinka hyvin verkkosivusto on optimoitu autonomisille tekoälyagenteille. Koostuu neljästä kategoriasta: Löydettävyys (20 %), Koneluettavuus (35 %), Navigoitavuus (20 %) ja Transaktiokyky (25 %).

### Agent Manifest / Agenttimanifesti

**EN:** A machine-readable JSON file served at `/.well-known/aaio-manifest.json` that declares a website's agent capabilities, supported protocols, and available endpoints. The entry point for AI agents discovering a site's AAIO features.

**FI:** Koneluettava JSON-tiedosto, joka tarjoillaan osoitteessa `/.well-known/aaio-manifest.json` ja joka ilmoittaa verkkosivuston agenttikyvykkyydet, tuetut protokollat ja käytettävissä olevat päätepisteet. Sisääntulopiste tekoälyagenteille, jotka löytävät sivuston AAIO-ominaisuuksia.

### Transaction Maturity Levels / Transaktiokypsyystasot

**EN:** A four-level scale (L0–L3) classifying a website's ability to support agent-mediated transactions:

| Level | Name | Description |
|-------|------|-------------|
| L0 | Information Only | Agent can read data but cannot transact |
| L1 | Cart-Ready | Agent can add items via API |
| L2 | Checkout-Ready | Agent can checkout (payment requires human approval) |
| L3 | Fully Autonomous | Agent can complete entire transaction including payment |

**FI:** Neliportainen asteikko (L0–L3), joka luokittelee verkkosivuston kyvyn tukea agenttivälitteisiä transaktioita:

| Taso | Nimi | Kuvaus |
|------|------|--------|
| L0 | Vain tiedot | Agentti voi lukea dataa, mutta ei voi asioida |
| L1 | Ostoskorivalmis | Agentti voi lisätä tuotteita API:n kautta |
| L2 | Kassavalmis | Agentti voi suorittaa kassan (maksu vaatii ihmisen hyväksynnän) |
| L3 | Täysin autonominen | Agentti voi suorittaa koko transaktion mukaan lukien maksun |

---

## Tekniset termit / Technical Terms

### Schema.org

**EN:** A collaborative vocabulary for structured data on the web. Used in AAIO for marking up products, services, organizations, and other entities in a machine-readable format (typically JSON-LD).

**FI:** Yhteisöllinen sanasto rakenteelliselle datalle verkossa. Käytetään AAIO:ssa tuotteiden, palveluiden, organisaatioiden ja muiden entiteettien merkitsemiseen koneluettavassa muodossa (tyypillisesti JSON-LD).

### JSON-LD — JavaScript Object Notation for Linked Data

**EN:** The recommended format for embedding Schema.org structured data in web pages. Embedded in a `<script type="application/ld+json">` tag in the page HTML.

**FI:** Suositeltu formaatti Schema.org-rakenteellisen datan upottamiseen verkkosivuille. Upotetaan `<script type="application/ld+json">` -tagiin sivun HTML:ssä.

### OpenAPI

**EN:** A specification for documenting RESTful APIs. In AAIO context, used to describe a website's programmatic endpoints that agents can use for search, product data, and transactions.

**FI:** Spesifikaatio RESTful API:en dokumentointiin. AAIO-kontekstissa käytetään kuvaamaan verkkosivuston ohjelmallisia päätepisteitä, joita agentit voivat käyttää hakuun, tuotedataan ja transaktioihin.

### llms.txt

**EN:** A plaintext file served at the site root (`/llms.txt`) providing an LLM-readable summary of the website. Follows the [llmstxt.org](https://llmstxt.org/) specification.

**FI:** Tekstimuotoinen tiedosto sivuston juuressa (`/llms.txt`), joka tarjoaa LLM-luettavan yhteenvedon verkkosivustosta. Noudattaa [llmstxt.org](https://llmstxt.org/) -spesifikaatiota.

### ai.txt

**EN:** A plaintext file at the site root (`/ai.txt`) declaring the site's AI usage policy — what AI systems are permitted to do with the site's content.

**FI:** Tekstimuotoinen tiedosto sivuston juuressa (`/ai.txt`), joka ilmoittaa sivuston tekoälyn käyttöpolitiikan — mitä tekoälyjärjestelmät saavat tehdä sivuston sisällöllä.

### A2A Agent Card

**EN:** A JSON file served at `/.well-known/agent.json` that declares an A2A-compatible agent's capabilities, supported skills, and interaction endpoints. Part of the Google A2A protocol.

**FI:** JSON-tiedosto, joka tarjoillaan osoitteessa `/.well-known/agent.json` ja joka ilmoittaa A2A-yhteensopivan agentin kyvykkyydet, tuetut taidot ja vuorovaikutuspäätepisteet. Osa Googlen A2A-protokollaa.

---

## Liiketoimintakonteksti / Business Context

### AI Agent / Tekoälyagentti

**EN:** An autonomous software entity that acts on behalf of a user to accomplish a goal. In AAIO context, typically a purchase agent that researches, compares, and buys products/services.

**FI:** Autonominen ohjelmistoentiteetti, joka toimii käyttäjän puolesta tavoitteen saavuttamiseksi. AAIO-kontekstissa tyypillisesti ostoagentti, joka tutkii, vertailee ja ostaa tuotteita/palveluita.

### Purchase Agent / Ostoagentti

**EN:** An AI agent specifically tasked with finding, comparing, and purchasing products or services on behalf of a human user.

**FI:** Tekoälyagentti, jonka tehtävänä on löytää, vertailla ja ostaa tuotteita tai palveluita ihmiskäyttäjän puolesta.

### Agent-Mediated Commerce / Agenttivälitteinen kaupankäynti

**EN:** Commerce where the buyer's AI agent conducts some or all of the purchase process (research, comparison, negotiation, transaction) autonomously.

**FI:** Kaupankäynti, jossa ostajan tekoälyagentti suorittaa osan tai koko ostoprosessin (tutkimus, vertailu, neuvottelu, transaktio) autonomisesti.

### Agent Journey / Agenttipolku

**EN:** The sequence of steps an AI agent takes from initial discovery of a site to completed transaction — analogous to the human customer journey.

**FI:** Tekoälyagentin toimintojen sarja ensimmäisestä sivuston löytämisestä valmiin transaktion suorittamiseen — analoginen ihmisen asiakaspolulle.

---

## Lyhenneluettelo / Abbreviation Index

| Abbreviation | Full Name (EN) | Full Name (FI) |
|-------------|----------------|-----------------|
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

*This glossary is part of the [AAIO Standard Draft](../README.md) project by [Tekoäly-Dani](https://tekoalydani.com).*
