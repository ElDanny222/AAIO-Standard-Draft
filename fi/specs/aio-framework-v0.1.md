# AI Optimization (AIO) -viitekehys v0.1

**Status:** Luonnos  
**Versio:** 0.1.0  
**Päivämäärä:** 2026-04-09  
**Tekijät:** [Tekoäly-Dani](https://tekoalydani.com)  
**Lisenssi:** Apache 2.0  

> 🇬🇧 [English version](../../specs/aio-framework-v0.1.md)

---

## Tiivistelmä

AI Optimization (AIO) on sateenvarjoviitekehys, joka kattaa kaikki digitaalisen läsnäolon optimointikerrokset tekoälyaikakaudella. AIO yhdistää SEO:n, AEO:n, GEO:n ja AAIO:n yhtenäiseksi, kumulatiiviseksi optimointipinoksi. Tämä dokumentti määrittelee AIO-viitekehyksen, sen kerrosarkkitehtuurin, kypsyysmallin ja strategisen implementointiohjauksen.

---

## 1. Johdanto

### 1.1 Ongelma

Organisaatiot kohtaavat hajanaisen kentän optimointivaatimuksia:

- **SEO**-konsultit optimoivat hakukoneiden tarpeisiin
- **AEO**-asiantuntijat optimoivat AI-vastausmoottoreita varten
- **GEO**-ekspertit optimoivat generatiivisen AI:n sisällyttämistä varten
- **AAIO**-arkkitehdit optimoivat autonomisten agenttien kaupankäyntiä varten

Ilman yhdistävää viitekehystä nämä ponnistelut menevät päällekkäin, ovat ristiriidassa tai jättävät aukkoja. AIO tarjoaa strategisen sateenvarjon, joka yhtenäistää kaiken AI-liittynnän optimoinnin yhtenäiseksi, johdonmukaiseksi ohjelmaksi.

### 1.2 Mitä AIO on?

**AI Optimization (AIO)** on kattava käytäntö digitaalisen läsnäolon optimoimiseksi kaikille tekoälyjärjestelmille — hakukoneiden ryömijöistä autonomisiin ostosagentteihin. AIO ei itsessään ole kerros; se on viitekehys, joka organisoi ja yhtenäistää kaikki kerrokset.

### 1.3 Keskeinen periaate

> AIO-kerrokset ovat **kumulatiivisia, eivät vaihtoehtoisia**. Jokainen kerros rakentuu edellisen päälle. Kerrosten ohittaminen luo hauraita optimointeja, jotka epäonnistuvat, kun tekoälyjärjestelmät arvioivat digitaalista läsnäoloasi kokonaisvaltaisesti.

---

## 2. AIO-kerrosarkkitehtuuri

### 2.1 Nelikerrosmalli

```
┌─────────────────────────────────────────────────────────────────┐
│                                                                 │
│   AIO — AI Optimization (Sateenvarjoviitekehys)                 │
│                                                                 │
│   ┌─────────────────────────────────────────────────────────┐   │
│   │  Kerros 4: AAIO — Agentic AI Optimization               │   │
│   │  Autonominen agentin löytäminen, navigointi, transaktio  │   │
│   ├─────────────────────────────────────────────────────────┤   │
│   │  Kerros 3: GEO — Generative Engine Optimization          │   │
│   │  Näky AI:n tuottamissa syntetisoiduissa vastauksissa     │   │
│   ├─────────────────────────────────────────────────────────┤   │
│   │  Kerros 2: AEO — Answer Engine Optimization              │   │
│   │  Tule siteeratuksi AI-vastausmoottoreissa                │   │
│   ├─────────────────────────────────────────────────────────┤   │
│   │  Kerros 1: SEO — Search Engine Optimization              │   │
│   │  Ole ryömittävissä, indeksoitavissa ja sijoitettavissa   │   │
│   └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### 2.2 Kerrosten määrittelyt

| Kerros | Nimi | Koko nimi | Ensisijainen yleisö | Tavoite | Tärkeimmät toimitukset |
|--------|------|-----------|---------------------|---------|----------------------|
| 1 | **SEO** | Search Engine Optimization | Hakukoneiden ryömijät + ihmiset | Sijoitu hakutuloksissa | robots.txt, sivukartat, Schema.org, metatagit |
| 2 | **AEO** | Answer Engine Optimization | AI-vastausmoottorit (ChatGPT, Perplexity, Gemini) | Tule siteeratuksi lähteenä | llms.txt, FAQ-merkinnät, faktuaalinen sisältö |
| 3 | **GEO** | Generative Engine Optimization | Generatiivisen AI:n synteesiputket | Näky tuotetuissa vastauksissa | Aiheautoriteetti, määräävä sisältö, data |
| 4 | **AAIO** | Agentic AI Optimization | Autonomiset AI-agentit | Mahdollista löytäminen + transaktio | Agenttimanifesti, rajapinnat, protokollapäätepisteet |

### 2.3 Kerrosten riippuvuudet

Jokaisella kerroksella on kovat riippuvuudet alla oleviin kerroksiin:

```
AAIO vaatii: GEO + AEO + SEO
GEO  vaatii: AEO + SEO
AEO  vaatii: SEO
SEO  vaatii: (web-standardien perusta)
```

**Käytännön seuraus:** Organisaatio ei voi toteuttaa AAIO:ta saavuttamatta ensin perus-SEO:n, AEO:n ja GEO:n valmiustasoa.

### 2.4 Täydentävät näkökulmat

Kaksi lisätermiä tarjoaa vaihtoehtoisia linssejä AIO:hon:

| Termi | Koko nimi | Näkökulma | Yleisö |
|-------|-----------|-----------|--------|
| **AXO** | Agent Experience Optimization | UX/CX-linssi AAIO:on | UX-suunnittelijat, CX-johtajat |
| **AIO** | AI Optimization | Strateginen sateenvarjo | Johtoryhmä, markkinoijat |

AXO ei ole erillinen kerros — se on käyttäjäkokemusnäkökulma AAIO:on.

---

## 3. AIO-kypsyysmalli

### 3.1 Viisi kypsyystasoa

| Taso | Nimi | Kuvaus | Tyypillinen pistealue |
|------|------|--------|----------------------|
| **L0** | **Optimoimaton** | Ei tarkoituksellista AI-optimointia. Perustason verkkoläsnäolo. | 0–19 |
| **L1** | **SEO-valmis** | Vahva SEO-perusta: ryömittävissä, indeksoitu, rakenteinen data. | 20–39 |
| **L2** | **AI-näkyvä** | AEO + GEO toteutettu. Sisältö näkyy AI-vastauksissa ja viittauksissa. | 40–59 |
| **L3** | **Agenttivalmis** | AAIO-taso 1–2: agentit voivat löytää ja lukea rakenteista dataa. | 60–79 |
| **L4** | **Agenttioptimioitu** | Täysi AAIO: agentit voivat löytää, navigoida JA asioida autonomisesti. | 80–100 |

### 3.2 Kypsyysarviointi

| Dimensio | L0 | L1 | L2 | L3 | L4 |
|----------|----|----|----|----|-----|
| **Ryömittävyys** | Osittainen | Täysi | Täysi | Täysi | Täysi |
| **Rakenteinen data** | Ei | Perus Schema.org | Rikas Schema.org + llms.txt | + Agenttimanifesti | + Täysi protokollaintegraatio |
| **AI-viittaus** | Ei | Satunnainen | Systemaattinen | Systemaattinen | Systemaattinen |
| **Agentin löytäminen** | Ei | Ei | Osittainen | Täysi | Täysi |
| **Agentin navigointi** | Ei | Ei | Ei | Rajapinnat + haku | Täysi ohjelmoitava pääsy |
| **Agentin transaktio** | Ei | Ei | Ei | Vain tiedot | Autonominen kaupankäynti |
| **Protokollatuki** | Ei | Ei | Ei | MCP-perus | MCP + ACP + A2A |

### 3.3 Etenemispolku

```
L0 → L1:  Toteuta SEO-perusta (3–6 kuukautta tyypilliselle sivustolle)
L1 → L2:  Lisää AEO/GEO-sisältöstrategia (3–6 kuukautta)
L2 → L3:  Ota käyttöön agenttimanifesti + rajapinnat (6–12 kuukautta)
L3 → L4:  Toteuta täysi protokollapino + autonominen kaupankäynti (12–24 kuukautta)
```

---

## 4. AIO-strategiakehys

### 4.1 Strategiset pilarit

Tehokas AIO-ohjelma lepää neljän strategisen pilarin varassa:

#### Pilari 1: Tekninen infrastruktuuri

Tekninen perusta, joka mahdollistaa kaikki AIO-kerrokset:
- Palvelinpuolen renderöinti tai staattinen generointi
- Rakenteinen data (Schema.org JSON-LD) kaikilla sivuilla
- Suorituskyvyn optimointi (Core Web Vitals)
- Turvallisuus (HTTPS, HSTS)
- Rajapintainfrastruktuuri agentin pääsyä varten

#### Pilari 2: Sisältöautoriteetti

Sisältö, joka asemoittaa organisaation määräävänä lähteenä:
- Kattava pilari-sisältö ydinkonsepteista
- Alkuperäinen tutkimus, data ja vertailut
- Asiantuntija-kirjoitettu sisältö E-E-A-T-signaaleilla
- Säännöllinen päivitystahti `dateModified`-seurannalla
- Moniformaattinen sisältö (teksti, data, rakenteinen)

#### Pilari 3: Koneluettavuus

Kaiken sisällön ja datan tekeminen AI-järjestelmien saavutettavaksi:
- Schema.org-merkinnät kaikille sisältötyypeille
- `llms.txt` LLM-luettavaan sivustoyhteenvetoon
- OpenAPI-spesifikaatio rajapinnoille
- Tuote-/palvelusyötteet koneluettavissa muodoissa
- AAIO-agenttimanifesti

#### Pilari 4: Agenttikaupankäynti

Autonomisten transaktioiden mahdollistaminen:
- API-pohjainen ostoskori ja kassa
- Protokollatuki (MCP, ACP, A2A)
- Tunnistautuminen agentin pääsylle (OAuth2, API-avaimet)
- Koneluettavat ehdot, käytännöt ja vahvistukset

### 4.2 Organisatorinen yhteensovitus

AIO on poikkifunktionaalinen. Vastuunjako:

| Toiminto | AIO-vastuu |
|----------|-----------|
| **Markkinointi** | Sisältöstrategia, brändiautoriteetti, AEO/GEO-sisältö |
| **Kehitys** | Tekninen SEO, rakenteinen data, rajapinnat, protokollaintegraatio |
| **Tuote** | Agenttikokemus (AXO), kassavirrat, data-arkkitehtuuri |
| **Lakiasiat** | AI-käytäntö (`ai.txt`), käyttöehdot, tietosuoja |
| **Johtoryhmä** | AIO-strategia, investointipriorisointi, kypsyystavoitteet |

---

## 5. AIO-implementointitiekartta

### 5.1 Vaihe 1: SEO-perusta (L0 → L1)

**Kesto:** 1–3 kuukautta | **Investointi:** Matala | **Vastuu:** Kehitys + Markkinointi

| Tehtävä | Prioriteetti | Toimitus |
|---------|-------------|---------|
| Tekninen SEO-audit | PAKKO | Auditiraportti toimenpiteineen |
| robots.txt AI-ryömijöillä | PAKKO | Päivitetty robots.txt |
| XML-sivukartan automaatio | PAKKO | Automaattisesti generoitu sivukartta |
| Schema.org-perusta | PAKKO | Organization + WebSite + Product/Service -merkinnät |
| Core Web Vitals | PAKKO | Kaikki mittarit "Hyvä"-alueella |
| Kanonistinen URL | PAKKO | `rel="canonical"` kaikilla sivuilla |

### 5.2 Vaihe 2: AEO/GEO-näkyvyys (L1 → L2)

**Kesto:** 3–6 kuukautta | **Investointi:** Kohtalainen | **Vastuu:** Markkinointi + Kehitys

| Tehtävä | Prioriteetti | Toimitus |
|---------|-------------|---------|
| `llms.txt`-luominen | PAKKO | LLM-luettava sivustoyhteenveto |
| `ai.txt`-käytäntö | PITÄISI | AI-käyttöilmoitus |
| FAQPage-merkinnät | PAKKO | FAQ-skeema tietokantasivuilla |
| Sisältöautoriteettiaudit | PAKKO | Tunnista ja täytä aihepuutteet |
| Pilari-sisällön luominen | PAKKO | 5–10 määräävää aihe-sivua |
| Tekijämerkinnät | PITÄISI | `Person` Schema.org asiantuntijoille |

### 5.3 Vaihe 3: Agenttivalmius (L2 → L3)

**Kesto:** 6–12 kuukautta | **Investointi:** Korkea | **Vastuu:** Kehitys + Tuote

| Tehtävä | Prioriteetti | Toimitus |
|---------|-------------|---------|
| AAIO-agenttimanifesti | PAKKO | `/.well-known/aaio-manifest.json` |
| Sisäinen hakurajapinta | PAKKO | JSON-pohjainen hakupäätepiste |
| OpenAPI-spesifikaatio | PITÄISI | Rajapinnan dokumentaatio |
| Tuote-/palvelusyötteet | PITÄISI | Koneluettava luettelo |
| MCP-työkalukuvaukset | PITÄISI | MCP-yhteensopivat rajapintametatiedot |
| Agentin tunnistautuminen | PITÄISI | OAuth2 tai API-avain -järjestelmä |

### 5.4 Vaihe 4: Autonominen kaupankäynti (L3 → L4)

**Kesto:** 12–24 kuukautta | **Investointi:** Erittäin korkea | **Vastuu:** Kehitys + Tuote + Lakiasiat

| Tehtävä | Prioriteetti | Toimitus |
|---------|-------------|---------|
| API-pohjainen kassa | PAKKO | REST/GraphQL-tilausrajapinta |
| ACP-integraatio | PITÄISI | Kone-kone-maksu |
| A2A-agenttipäätepiste | PITÄISI | `/.well-known/agent.json` |
| Koneluettavat käyttöehdot | PAKKO | Jäsennetyt palveluehdot |
| Palautuskäytäntömerkinnät | PITÄISI | `MerchantReturnPolicy` Schema.org |
| Transaktiokirjanpito | PAKKO | Agenttitransaktioiden jäljitysketju |

---

## 6. AIO-pisteytys

### 6.1 Yhdistetty AIO-pisteet

| Komponentti | Paino | Arviointimenetelmä |
|-------------|-------|-------------------|
| SEO-pisteet | 20 % | Tekninen SEO-audit (automatisoitu) |
| AEO-pisteet | 20 % | Viittausten seuranta + rakenteisen datan audit |
| GEO-pisteet | 25 % | AI-synteesin sisällyttämisaudit |
| AAIO-pisteet | 35 % | AAIO-valmiuspisteet (ks. [ydinspesifikaatio](aaio-core-v0.1.md)) |
| **AIO-kokonaispisteet** | **100 %** | |

### 6.2 Pisteytyksen tulkinta

| Pisteet | Kypsyys | Selite |
|---------|---------|--------|
| 0–19 | L0 | **Optimoimaton** — Näkymätön AI-järjestelmille |
| 20–39 | L1 | **SEO-valmis** — Ryömittävissä, mutta ei AI-optimoitu |
| 40–59 | L2 | **AI-näkyvä** — Näkyy AI-vastauksissa |
| 60–79 | L3 | **Agenttivalmis** — Agentit voivat löytää ja lukea |
| 80–100 | L4 | **Agenttioptimioitu** — Täysi autonominen kaupankäynti |

---

## 7. Toimialakohtaiset sovellukset

### 7.1 Verkkokauppa

**AIO-prioriteetti:** L4 (Täysi autonominen kaupankäynti)

AI-ostosagentti muuttavat verkkokauppaa. Vähittäiskauppiaat, jotka saavuttavat L4-kypsyyden, saavat suoran kanavan agenttien ajamille ostoille.

### 7.2 Ammatilliset palvelut

**AIO-prioriteetti:** L3 (Agenttivalmis löydettävyys)

Palveluyritykset hyötyvät agenttinäkyvyydestä ja automatisoiduista varaus-/kyselyvirroista.

### 7.3 SaaS / Teknologia

**AIO-prioriteetti:** L3–L4 (Rajapintapohjaiseen agenttipääsy)

Ohjelmistoyritykset ovat luonnostaan sopivia AAIO:lle — tuotteillaan on jo rajapinnat.

### 7.4 Media / Kustannus

**AIO-prioriteetti:** L2–L3 (AI-viittaus ja -synteesi)

Mediayritysten ensisijainen arvo on sisältöautoriteetti — AEO ja GEO ovat kriittisiä.

---

## 8. AIO-hallinto

### 8.1 Roolit

| Rooli | Vastuu |
|-------|--------|
| **AIO-johtaja** | Kokonaisstrategia, kypsyystavoitteet, poikkifunktionaalinen yhteensovitus |
| **Tekninen AIO** | SEO-infrastruktuuri, Schema.org, rajapintakehitys |
| **Sisältö-AIO** | AEO/GEO-sisältöstrategia, autoriteettirakentaminen |
| **Kaupankäynti-AIO** | AAIO-agenttikokemus, protokollaintegraatio |

### 8.2 Arviointitahti

| Toiminta | Taajuus | Omistaja |
|----------|---------|---------|
| AIO-pisteytysarvio | Neljännesvuosittain | AIO-johtaja |
| AI-viittausaudit | Kuukausittain | Sisältö-AIO |
| Tekninen SEO-audit | Kuukausittain | Tekninen AIO |
| Agenttivalmiustesti | Neljännesvuosittain | Kaupankäynti-AIO |
| Strategiakatsaus | Puolivuosittain | Johtoryhmä |

---

## 9. Usein kysytyt kysymykset

### K: Korvataako AIO SEO:n?

**Ei.** AIO on sateenvarjo, joka *sisältää* SEO:n. SEO pysyy perustana. AIO lisää AEO:n, GEO:n ja AAIO:n päälle.

### K: Tarvitsenko kaikki neljä kerrosta?

Riippuu liiketoimintamallista. Jokainen yritys tarvitsee L1:n (SEO). Useimmat hyötyvät L2:sta (AEO/GEO). Verkkokauppa- ja palveluyritykset tulisi tavoitella L3–L4:ää (AAIO).

### K: Mikä on AIO:n ja AXO:n suhde?

AXO (Agent Experience Optimization) on UX-näkökulma AIO:n AAIO-kerrokseen. AXO:a käytetään UX/CX-päättäjien kanssa kommunikoidessa samasta teknisestä työstä.

---

## Liite A: Viitteet

- [SEO Foundations v0.1](seo-foundations-v0.1.md) — SEO-kerroksen spesifikaatio
- [AEO Guidelines v0.1](aeo-guidelines-v0.1.md) — AEO-kerroksen spesifikaatio
- [GEO Guidelines v0.1](geo-guidelines-v0.1.md) — GEO-kerroksen spesifikaatio
- [AAIO Core Specification v0.1](aaio-core-v0.1.md) — AAIO-kerroksen spesifikaatio
- [AXO Framework v0.1](axo-framework-v0.1.md) — Agenttikokemusoptimointi
- [Schema.org](https://schema.org/) — Rakenteisen datan sanasto

---

*Tämä dokumentti on osa [AAIO Standard Draft](../../README.md) -projektia, jonka ylläpitäjä on [Tekoäly-Dani](https://tekoalydani.com).*
