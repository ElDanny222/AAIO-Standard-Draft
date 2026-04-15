# AAIO Standard Draft

![Tila](https://img.shields.io/badge/tila-luonnos-yellow)
![Versio](https://img.shields.io/badge/versio-0.1-blue)
![Lisenssi](https://img.shields.io/badge/lisenssi-Apache%202.0-green)

**Agentic AI Optimization (AAIO)** — avoimet tekniset spesifikaatiot, jotka tekevät verkkosivustoista löydettäviä, luettavia ja asioitavia autonomisille AI-agenteille.

Ylläpitäjä: [Tekoäly-Dani](https://tekoalydani.com)

> 🇬🇧 [English version](../README.md)

---

## Mitä AAIO on?

AAIO ei ole uusi protokolla. Se on **optimointikerros**, joka määrittelee miten organisaatiot toteuttavat olemassa olevat agenttiprotokollat — MCP, ACP, UCP, A2A — niin, että autonomiset AI-agentit voivat:

1. **Löytää** yrityksen ja sen palvelut
2. **Ymmärtää** jäsennellyn tuote- ja palveludatan
3. **Asioida** ilman ihmisvälikättä

AAIO sijoittuu SEO:n, AEO:n ja GEO:n yläpuolelle. Se vastaa nousevaan todellisuuteen, jossa AI-agentit — ei ihmiset — ovat ensisijaisia ostajia, tutkijoita ja päätöksentekijöitä.

```
Ihmisten haku (SEO) → AI-vastausmoottorit (AEO/GEO) → Autonomiset agentit (AAIO)
```

---

## Repositorion rakenne

```
AAIO-Standard-Draft/
├── README.md                        # Tämä tiedosto (englanti)
├── fi/                              # Suomenkieliset käännökset
│   ├── README.md                    # Tämä tiedosto
│   ├── CONTRIBUTING.md
│   ├── ROADMAP.md
│   ├── CHANGELOG.md
│   ├── specs/                       # Tekniset spesifikaatiot (FI)
│   ├── docs/                        # Tukidokumentaatio (FI)
│   └── examples/                   # Esimerkit (FI)
├── CONTRIBUTING.md                  # Osallistumisohjeet
├── LICENSE                          # Apache 2.0
│
├── specs/                           # Tekniset spesifikaatiot (EN)
│   ├── aio-framework-v0.1.md        # AIO-viitekehys
│   ├── seo-foundations-v0.1.md      # SEO-perusta AAIO:lle
│   ├── aeo-guidelines-v0.1.md       # AEO-parhaat käytännöt
│   ├── geo-guidelines-v0.1.md       # GEO-ohjeistus
│   ├── aaio-core-v0.1.md            # AAIO-ydinspesifikaatio
│   ├── axo-framework-v0.1.md        # AXO-viitekehys (UX-näkökulma)
│   ├── acp-integration-v0.1.md      # ACP-integrointiopas
│   ├── ucp-integration-v0.1.md      # UCP-integrointiopas
│   └── a2a-commerce-v0.1.md         # A2A Commerce Protocol -profiili
│
├── schemas/                         # Koneluettavat skeemamäärittelyt
│   ├── aaio-manifest.schema.json    # Sivustotason AAIO-manifesti
│   ├── aaio-product.schema.json     # Agenttioptimoitu tuotedata
│   ├── aaio-service.schema.json     # Agenttioptimoitu palveludata
│   └── aaio-scoring.schema.json     # AAIO-valmiuspisteet
│
├── examples/                        # Viiteimplementaatiot
│   ├── ecommerce/
│   ├── service-provider/
│   └── saas-platform/
│
└── docs/                            # Tukidokumentaatio (EN)
    ├── protocol-landscape.md        # Miten MCP, ACP, UCP, A2A suhteutuvat AAIO:on
    ├── implementation-roadmap.md    # Vaiheittainen käyttöönotto-opas
    └── terminology.md               # Sanasto
```

---

## Spesifikaatiot

### AIO-pino (kumulatiiviset kerrokset)

| Kerros | Dokumentti | Tila | Kuvaus |
|--------|------------|------|--------|
| Viitekehys | [AIO Framework v0.1](../specs/aio-framework-v0.1.md) | Luonnos | Sateenvarjoviitekehys, joka yhdistää kaikki AI-optimointikerrokset |
| L1 | [SEO Foundations v0.1](../specs/seo-foundations-v0.1.md) | Luonnos | SEO-vaatimukset, jotka ovat kaiken AI-optimoinnin perusta |
| L2 | [AEO Guidelines v0.1](../specs/aeo-guidelines-v0.1.md) | Luonnos | Vastausmoottorioptimoinnin parhaat käytännöt |
| L3 | [GEO Guidelines v0.1](../specs/geo-guidelines-v0.1.md) | Luonnos | Generatiivisten moottoreiden optimointiohjeistus |
| L4 | [AAIO Core v0.1](../specs/aaio-core-v0.1.md) | Luonnos | Ydinoptimointivaatimukset ja agenttivalmiuskriteerit |
| L4 (UX) | [AXO Framework v0.1](../specs/axo-framework-v0.1.md) | Luonnos | Agenttikokemusoptimointiviitekehys |

### Protokollaintegrointispesifikaatiot

| Dokumentti | Tila | Kuvaus |
|------------|------|--------|
| [ACP Integration v0.1](../specs/acp-integration-v0.1.md) | Luonnos | Agent Commerce Protocol -integrointiopas |
| [UCP Integration v0.1](../specs/ucp-integration-v0.1.md) | Luonnos | Universal Commerce Protocol -integrointiopas |
| [A2A Commerce v0.1](../specs/a2a-commerce-v0.1.md) | Luonnos | Agentti-agentti-neuvotteluprotokollan profiili |

---

## Pikaopas

**Oletko johtaja tai strategi?**

Aloita [AIO-viitekehyksestä](../specs/aio-framework-v0.1.md) kokonaiskuvan saamiseksi — se selittää kumulatiivisen kerrosmallin ja kypsyyspolun SEO:sta täyteen AAIO:on.

**Haluatko tehdä organisaatiostasi agenttivalmiin?**

Aloita [SEO-perustan](../specs/seo-foundations-v0.1.md) tarkistuslistasta, sitten seuraa [käyttöönotto-opasta](docs/implementation-roadmap.md) vaiheittaiseksi poluksi täyteen AAIO-vaatimustenmukaisuuteen.

**Oletko kehittäjä, joka rakentaa agentteja palvelevaa infrastruktuuria?**

Lue ensin [AAIO-ydinspesifikaatio](../specs/aaio-core-v0.1.md) ja [protokollakartta](docs/protocol-landscape.md).

**Oletko sisältöstrategi tai markkinoija?**

[AEO-ohjeistus](../specs/aeo-guidelines-v0.1.md) ja [GEO-ohjeistus](../specs/geo-guidelines-v0.1.md) kattavat, miten optimoida sisältöä AI-vastausmoottoreita ja generatiivista AI:ta varten.

**Oletko AI-tutkija tai toimittaja?**

[Sanasto](docs/terminology.md) määrittelee kaikki termit täsmällisesti. [Protokollakartta](docs/protocol-landscape.md) sijoittaa AAIO:n suhteessa MCP:hen, ACP:hen, UCP:hen ja A2A:han.

---

## Termistö

| Termi | Koko nimi | Rooli AAIO:ssa |
|-------|-----------|---------------|
| **AIO** | AI Optimization | Sateenvarjotermi kaikelle AI-optimoinnille |
| **AEO** | Answer Engine Optimization | Viittausten saaminen AI-vastausmoottoreista (ChatGPT, Perplexity) |
| **GEO** | Generative Engine Optimization | Näkyminen AI:n tuottamissa syntetisoiduissa vastauksissa |
| **AAIO** | Agentic AI Optimization | Autonomisten agenttien mahdollistaminen löytämään, ymmärtämään ja asioimaan |
| **AXO** | Agent Experience Optimization | UX/CX-näkökulma AAIO:on — miten agentit kokevat sivuston |
| **MCP** | Model Context Protocol | Anthropicin protokolla AI-mallien yhdistämiseen työkaluihin ja dataan |
| **ACP** | Agent Commerce Protocol | Kone-kone-maksutransaktiot (Stripe & OpenAI, Apache 2.0) |
| **UCP** | Universal Commerce Protocol | Yhtenäinen palveludatastandardi AI-agenteille |
| **A2A** | Agent-to-Agent | Agenttien välinen neuvotteluprotokolla (Google, nyt Linux Foundation) |

---

## Tila

Tämä repositorio on **aktiivisessa luonnosvaiheessa**. Kaikki spesifikaatiot ovat v0.1 ja voivat muuttua. Palaute ja osallistuminen ovat tervetulleita — katso [CONTRIBUTING.md](CONTRIBUTING.md).

Nämä spesifikaatiot on kehitetty todellisen AAIO-implementaatiotyön pohjalta [tekoalydani.com](https://tekoalydani.com)-sivustolla ja on suunniteltu toimittajanetriaaliksi ja avoimesti laajennettaviksi.

---

## Tekijä

[Tekoäly-Dani](https://tekoalydani.com)  
[dani@tekoalydani.com](mailto:dani@tekoalydani.com)

---

## Lisenssi

Apache 2.0 — katso [LICENSE](../LICENSE)
