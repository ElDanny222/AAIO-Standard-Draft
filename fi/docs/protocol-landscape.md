# Protokollakartta

> **Status:** Draft v0.1 | Ylläpitäjä: [Tekoäly-Dani](https://tekoalydani.com)

> 🇬🇧 [English version](../../docs/protocol-landscape.md)

Tämä dokumentti kartoittaa agenttien protokollaekosysteemin ja selittää, miten kukin protokolla suhteutuu AAIO:on (Agentic AI Optimization).

---

## Keskeinen oivallus

Yhtä ainoaa "agenttisen webin protokollaa" ei ole. Sen sijaan on syntymässä toisiaan täydentävien protokollien pino — kukin ratkaisee erillisen osan agentin vuorovaikutusongelmasta. AAIO ei ole uusi protokolla tässä pinossa. Se on **implementointikehys**, joka kertoo organisaatioille, miten nämä protokollat otetaan käyttöön ja yhdistetään oikein.

---

## Protokollojen yleiskatsaus

### MCP — Model Context Protocol

| Ominaisuus | Tiedot |
|------------|--------|
| **Alkuperä** | Anthropic (avoin standardi) |
| **Tarkoitus** | Yhdistää AI-mallit ulkoisiin työkaluihin, tietolähteisiin ja rajapintoihin |
| **Kerros** | Konteksti / työkalujen käyttö |
| **Tila** | Aktiivinen, laajasti omaksuttu |

MCP määrittelee, miten AI-mallit (LLM:t) löytävät ulkoiset työkalut ja kutsuvat niitä. Yritys, joka tarjoaa MCP-palvelimen, antaa AI-agenteille jäsennetyn tavan hakea varastotietoja, tarkistaa saatavuutta, hakea dokumentteja tai laukaista toimintoja — ilman, että agentin tarvitsee kaapata HTML-sivuja.

**Suhde AAIO:on:** MCP-palvelimen tarjoaminen on AAIO:n ydinvaatimus. Ilman MCP-yhteensopivaa rajapintaa AI-agentit turvautuvat jäsentymättömään web-kaappaukseen, joka on hidasta, hauraata ja monille agenttijakille saavuttamatonta.

---

### ACP — Agent Commerce Protocol

| Ominaisuus | Tiedot |
|------------|--------|
| **Alkuperä** | Stripe & OpenAI (avoin standardi, Apache 2.0) |
| **Tarkoitus** | Määrittelee HTTP-otsakkeet ja allekirjoitukset kone-koneiden välisiin transaktioihin |
| **Kerros** | Maksu / transaktioiden valtuutus |
| **Tila** | Aktiivinen |

ACP määrittelee, miten AI-agentit tunnistautuvat, valtuuttavat ja toteuttavat rahalliset transaktiot ilman ihmisen hyväksyntää joka vaiheessa. Se kattaa agentti-identiteetin otsakkeet, transaktioiden allekirjoittamisen ja maksun vahvistuskoukut.

**Suhde AAIO:on:** ACP vaaditaan kaikissa AAIO-implementaatioissa, jotka tukevat autonomista ostamista (taso 3+ AAIO-valmiuspisteissä). Organisaatiot, jotka tarvitsevat vain agenttien löytämistä ja tarjousten tekemistä, voivat lykätä ACP-implementaatiota.

---

### UCP — Universal Commerce Protocol

| Ominaisuus | Tiedot |
|------------|--------|
| **Alkuperä** | Kehittyvä avoin standardi |
| **Tarkoitus** | Yhtenäinen skeema palvelu- ja tuotadatalle AI-agenteille |
| **Kerros** | Data / jäsennetty sisältö |
| **Tila** | Luonnos |

UCP määrittelee, mitä kenttiä tuote- tai palvelulistauksen täytyy sisältää ollakseen täysin koneluettava agenteille. Se laajentaa ja muodollistaa sen, mitä Schema.org aloitti — mutta lisää agenttikohtaisia kenttiä kuten neuvoteltavuusliput, agenttiluettavat SLA:t ja koneyhteensopivat hinnoittelurakenteet.

**Suhde AAIO:on:** UCP-vaatimustenmukaisuus vaaditaan AAIO-taso 2+:lle. Se varmistaa, että kun agentti hakee tuotetta, se saa täydellisen, yksiselitteisen, jäsennetyn vastauksen ihmisluettavan verkkosivun sijaan.

---

### A2A — Agent-to-Agent Protocol

| Ominaisuus | Tiedot |
|------------|--------|
| **Alkuperä** | Google (nyt Linux Foundation, avoin standardi) |
| **Tarkoitus** | Kommunikaatio- ja neuvotteluprotokolla autonomisten agenttien välillä |
| **Kerros** | Agenttien koordinointi / moniagenttiorkestrointi |
| **Tila** | Aktiivinen |

A2A määrittelee, miten yksi agentti puhuu toiselle — mukaan lukien kyvykkyyksien löytäminen, tehtävien delegointi ja tulosten välittäminen. Kaupankäyntikontekstissa A2A mahdollistaa ostaja-agenttien suoran hakeutumisen myyjä-agentteihin, ehtojen neuvottelun ja transaktioiden vahvistamisen jäsennetyn viestinvaihdon kautta.

**Suhde AAIO:on:** A2A on relevantti AAIO-taso 4:lle (täysi agenttinen kaupankäynti). Organisaatiot, jotka tarjoavat A2A-yhteensopivan agenttipäätepisteen, mahdollistavat ostaja-agenttien vuorovaikutuksen ilman minkäänlaista ihmisille suunnattua rajapintaa.

---

### AGENTS.md

| Ominaisuus | Tiedot |
|------------|--------|
| **Alkuperä** | Yhteisön käytäntö (ei virallista standardointielintä) |
| **Tarkoitus** | Ohjaustiedosto, joka kertoo AI-agenteille, miten navigoida ja käyttää koodikantaa tai palvelua |
| **Kerros** | Löydettävyys / konteksti |
| **Tila** | Käytäntö |

`AGENTS.md` on pelkkä tekstitiedosto, joka sijoitetaan repositorion tai verkkosivuston juureen. Se kertoo AI-agenteille, mitä järjestelmä tekee, miten se on rakennettu ja mitä agentti saa tehdä. Se on agenttien vastine `robots.txt`:lle — mutta kuvaileva eikä rajoittava.

**Suhde AAIO:on:** `AGENTS.md`-tiedosto (tai vastaava `ai-instructions.txt` verkkosivuston juuressa) suositellaan kaikille AAIO-taso 1+ -implementaatioille. Se on nopein ja halvimman tapa tehdä järjestelmästä agenttien luettava.

---

## Miten protokollat pinoutuvat

```
┌─────────────────────────────────────────────────────────┐
│                        AAIO                              │
│         (Optimointikehys — ei protokolla)                │
│                                                          │
│  Määrittelee MILLOIN ja MITEN toteuttaa alla olevat      │
└─────────────────────────────────────────────────────────┘
         │              │              │              │
         ▼              ▼              ▼              ▼
   ┌──────────┐   ┌──────────┐  ┌──────────┐  ┌──────────┐
   │  MCP     │   │   UCP    │  │   ACP    │  │   A2A    │
   │          │   │          │  │          │  │          │
   │ Työkalu- │   │  Data-   │  │ Maksu-   │  │ Agentti- │
   │ käyttö   │   │ skeema   │  │ otsakkeet│  │ viestintä│
   └──────────┘   └──────────┘  └──────────┘  └──────────┘
         │              │              │              │
         └──────────────┴──────────────┴──────────────┘
                                │
                         ┌──────────────┐
                         │  AGENTS.md   │
                         │ (löydettävyys)│
                         └──────────────┘
```

---

## AAIO-valmiustasot

| Taso | Nimi | Vaaditut protokollat |
|------|------|----------------------|
| **0** | Ei agenttivalmis | Ei mitään |
| **1** | Löydettävä | AGENTS.md (tai vastaava) |
| **2** | Luettava | MCP-palvelin + UCP-yhteensopiva data |
| **3** | Transaktiokykyinen | + ACP-otsakkeet + hinnoittelurajapinta |
| **4** | Täysin autonominen | + A2A-päätepiste |

Organisaatioiden ei tarvitse saavuttaa tasoa 4 hyötyäkseen AAIO:sta. Jokainen taso tuottaa itsenäistä arvoa. Pelkästään taso 1 voi merkittävästi lisätä AI-viittausten tiheyttä vastausmoottoreissa.

---

## Mitä AAIO EI määrittele

AAIO ei kilpaile eikä korvaa:

- **SEO** — edelleen välttämätön ihmisten hakuliikenteelle
- **AEO/GEO** — edelleen välttämätön AI-vastausmoottoriviittauksille
- **MCP, ACP, UCP, A2A** — AAIO toteuttaa ne, ei korvaa niitä
- **Schema.org-rakenteinen data** — pysyy perustavanlaatuisena riippuvuutena

AAIO istuu kaikkien näiden yläpuolella. Se vastaa kysymykseen: *"Koska kaikki nämä protokollat ovat olemassa, miten organisaatio ottaa ne käyttöön oikeassa järjestyksessä, oikealla syvyydellä, omaan käyttötapaukseensa?"*

---

## Katso myös

- [Käyttöönotto-opas](implementation-roadmap.md) — vaiheittainen käytännön opas
- [AAIO-ydinspesifikaatio](../specs/aaio-core-v0.1.md) — täydelliset tekniset vaatimukset
