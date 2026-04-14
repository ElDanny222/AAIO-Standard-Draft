# AAIO-käyttöönotto-opas

> **Status:** Draft v0.1 | Ylläpitäjä: [Tekoäly-Dani](https://tekoalydani.com)

> 🇬🇧 [English version](../../docs/implementation-roadmap.md)

Käytännönläheinen, vaiheittainen opas organisaatioille, jotka toteuttavat Agentic AI Optimization (AAIO) -standardia.

---

## Ennen aloittamista

AAIO-implementaatio ei ole kaikki tai ei mitään -projekti. Jokainen vaihe tuottaa itsenäistä arvoa. Vaiheessa 2 oleva yritys on merkittävästi paremmin asemoitunut kuin vaiheessa 0 — vaikka se ei koskaan saavuttaisi vaihetta 4.

Aloita [AAIO-auditilla](#aaio-auditin-tilaaminen) ymmärtääksesi nykyisen lähtötasosi ennen tiekarttaan sitoutumista.

---

## Vaihe 0 — Arviointi

**Tavoite:** Ymmärrä, missä olet tänään.

### Toimenpiteet

1. **Auditoi nykyinen agenttivalmiutesi**
   - Voivatko AI-agentit tällä hetkellä käyttää tuote-/palveludataasi jäsennetyssä muodossa?
   - Onko sinulla `AGENTS.md` tai `ai-instructions.txt` verkkosivustosi juuressa?
   - Onko Schema.org-rakenteinen datasi täydellinen ja ajantasainen?
   - Onko sinulla rajapinta tai MCP-palvelin?

2. **Määrittele tavoitekäyttötapaus**
   - Tarvitsevatko agentit löytää sinut? (taso 1 -tavoite)
   - Tarvitsevatko agentit lukea ja vertailla palveluitasi? (taso 2 -tavoite)
   - Tarvitsevatko agentit tehdä tilauksia autonomisesti? (taso 3–4 -tavoite)

3. **Inventoi olemassa oleva infrastruktuurisi**
   - Mitä rajapintoja sinulla on jo käytössä?
   - Mitä CMS- tai verkkokauppa-alustaa käytät?
   - Mikä on nykyinen Schema.org-implementaatiosi?

**Toimitus:** Selkeä kuva nykyisestä AAIO-tasostasi (0–4) ja tavoitetasostasi.

---

## Vaihe 1 — Löydettävyyskerros

**Tavoite:** Tee yrityksestäsi AI-agenttien löydettävissä. (AAIO-taso 1)

**Arvioitu työmäärä:** 1–3 päivää

### Toimenpiteet

1. **Luo `AGENTS.md`** verkkosivustosi juureen (`yourdomain.com/AGENTS.md`)

   Vähimmäissisältö:
   ```markdown
   # Agentin ohjeet

   ## Mitä tämä sivusto on
   [Yksi kappale, jossa kuvaat yrityksesi ja mitä tarjoat]

   ## Mitä agentit voivat tehdä täällä
   - [Luettele toiminnot, jotka agentit saavat tehdä]

   ## Tärkeimmät päätepisteet
   - Tuotteet/palvelut: [URL]
   - Hinnoittelu: [URL]
   - Yhteystiedot/varaus: [URL]

   ## Saatavilla olevat datamuodot
   - [JSON-LD / XML / API / jne.]
   ```

2. **Päivitä `robots.txt`**

   Varmista, että oikeutettuja AI-ryömijiä ei ole estetty:
   ```
   User-agent: GPTBot
   Allow: /

   User-agent: ClaudeBot
   Allow: /

   User-agent: PerplexityBot
   Allow: /
   ```

3. **Tarkista ja täydennä Schema.org-rakenteinen data**
   - `Organization` kaikilla kentillä
   - `Product` tai `Service` kaikille tärkeimmille tarjoamille
   - `FAQPage` yleisimmille kysymyksille
   - `ContactPoint` agenttien käytettäväksi

4. **Ilmoittaudu AI-hakemistoihin ja viittauslähteisiin**
   - Varmista, että Wikipedia, Wikidata ja LinkedIn ovat ajantasaisia
   - Ilmoittaudu relevantteihin toimialahakemistoihin

**Varmennus:** Pyydä ChatGPT:tä, Claudea tai Perplexityä kuvaamaan yrityksesi. Vertaa vastausta todelliseen tarjoamaasi. Aukot viittaavat puuttuvaan rakenteiseen dataan tai heikkoon viittauskattavuuteen.

---

## Vaihe 2 — Luettavuuskerros

**Tavoite:** Mahdollista AI-agenttien kyky lukea, jäsentää ja vertailla tarjoamiasi ohjelmallisesti. (AAIO-taso 2)

**Arvioitu työmäärä:** 1–4 viikkoa

### Toimenpiteet

1. **Tarjoa koneluettava tuote-/palvelurajapinta**

   Datasi täytyy olla saatavilla vakaassa päätepisteessä JSON- tai JSON-LD-muodossa. Palvelutarjoaman vähimmäiskentät:
   - Nimi, kuvaus, kategoria
   - Hinnoittelu (summa, valuutta, laskutusjakso)
   - Saatavuus / kapasiteetti
   - Toimitustapa (etänä, paikan päällä jne.)
   - Yhteystieto tai varauksen päätepiste

2. **Toteuta UCP-yhteensopiva datarakenne**

   Noudata [UCP-integrointiopasta](../../specs/ucp-integration-v0.1.md) varmistaaksesi, että datakentät vastaavat agenttien luettavaa standardia.

3. **Ota käyttöön MCP-palvelin** (suositeltu)

   MCP-palvelin antaa AI-agenteille jäsennetyn, työkalupohjaisen rajapinnan dataasi. Se korvaa webscraping-tekniikan puhtailla API-kutsuilla.

   Perustoiminnot MCP-palvelimessa:
   - `list_products` tai `list_services`
   - `get_product_details` (ID:llä tai nimellä)
   - `check_availability`
   - `get_pricing`

4. **Testaa oikeilla AI-agenteilla**

   Käytä Claude-, GPT-4- tai Perplexity-rajapintaa MCP-palvelimesi tai rajapintasi suoraan hakemiseen. Varmista, että vastaukset ovat täydellisiä, tarkkoja ja jäsennettävissä.

**Varmennus:** AI-agentin pitäisi pystyä tuottamaan tarkka tuotevertailutaulukko käyttäen vain koneluettavaa dataasi, ilman vierailua verkkosivustollasi.

---

## Vaihe 3 — Transaktiokerros

**Tavoite:** Mahdollista AI-agenttien kyky käynnistää ja suorittaa transaktioita ihmisprinsipaaliensa puolesta. (AAIO-taso 3)

**Arvioitu työmäärä:** 2–8 viikkoa (riippuu paljon olemassa olevasta maksuinfrastruktuurista)

### Toimenpiteet

1. **Toteuta ACP-otsakkeet transaktiorajapintaasi**

   Noudata [ACP-integrointiopasta](../../specs/acp-integration-v0.1.md). Tärkeimmät vaatimukset:
   - Agentin identiteettiotsake (`ACP-Agent-Id`)
   - Valtuutustokeniotsake (`ACP-Delegation-Token`)
   - Idempotenssiavaintuki (`ACP-Transaction-Id`)
   - Koneluettavat virhevastaukset

2. **Luo agentille saavutettava kassavirta**

   Nykyinen kassaprosessisi on lähes varmasti suunniteltu ihmisille (HTML-lomakkeet, uudelleenohjaukset, CAPTCHA). Agentit tarvitsevat:
   - Puhtaasti API-pohjaisen tilauksen luontipäätepisteen
   - Selkeän vahvistus- ja kuittidata JSON-muodossa
   - Tilakyselyt tai webhook asynkroniseen vahvistukseen

3. **Määrittele agentin transaktioikäytännöt**

   Dokumentoi ja toimeenpane:
   - Enimmäistransaktiosumma, jonka agentti voi valtuuttaa ilman ihmisen vahvistusta
   - Sallitut tuote-/palvelukategoriat autonomiselle ostolle
   - Palautus- ja peruutusrajapinnat (agentit tarvitsevat myös ostojensa peruuttamista)

4. **Lisää agentin tunnistautuminen**

   Agentit täytyy pystyä tunnistamaan. Toteuta:
   - API-avainten myöntäminen agenttiasiakkaille
   - Nopeusrajoitukset agentin identiteetin mukaan
   - Kirjanpito kaikista agentin käynnistämistä transaktioista

**Varmennus:** Testiagentti pitäisi pystyä selaamaan, valitsemaan ja ostamaan tuotteen tai palvelun kokonaan API-kutsujen kautta — ilman ihmisille suunnattua web-käyttöliittymää.

---

## Vaihe 4 — Täysi agenttinen kaupankäynti

**Tavoite:** Salli autonomisten agenttien löytää, arvioida, neuvotella ja asioida suoraan agentti-infrastruktuurisi kanssa. (AAIO-taso 4)

**Arvioitu työmäärä:** 4–12 viikkoa

### Toimenpiteet

1. **Ota käyttöön A2A-yhteensopiva agenttipäätepiste**

   Noudata [A2A Commerce Protocol -profiilia](../../specs/a2a-commerce-v0.1.md). Agenttipäätepisteesi täytyy tukea:
   - Kyvykkyyksien ilmoittaminen (mitä agenttisi voi tehdä)
   - Tehtävien vastaanottaminen ja käsittely
   - Jäsennettyjen tulosten palauttaminen
   - Agentti-agentti-neuvottelu hinnoista/ehdoista (tarvittaessa)

2. **Rekisteröidy A2A-agenttipalveluihin** (saatavilla myöhemmin)

   A2A-infrastruktuurin kypsyessä syntyy agentin löytämispalveluja. Varmista, että agenttipäätepisteesi on rekisteröity ja kyvykkyydet on kuvattu oikein.

3. **Toteuta agentin istunnonhallinta**

   Monivuoroiset agenttikonversaatiot vaativat:
   - Istuntotunnukset
   - Tilan pysyvyyden kutsujen välillä
   - Aikakatkaisu- ja siivoustoiminnot

4. **Testaa ostaja-agenteilla hiekkalaatikkoympäristössä**

   Ennen tuotantoon siirtymistä testaa realistisilla ostaja-agentin työkuormilla:
   - Löytäminen → kysely → vertailu → osto -sekvenssit
   - Neuvottelusekvensit (tarvittaessa)
   - Virhe- ja poikkeuspolut

**Varmennus:** Autonominen ostaja-agentti — jolle annetaan vain verkkotunnuksesi — pitäisi pystyä löytämään tarjoamasi, vertailemaan niitä kilpailijoihin, neuvottelemaan tarvittaessa ja suorittamaan transaktion ilman minkäänlaista ihmisen väliintuloa.

---

## AAIO-auditin tilaaminen

Etkö tiedä mistä aloittaa? AAIO-audit antaa sinulle:

- Nykyisen AAIO-valmiuspisteesi (0–100)
- Aukkoanalyysin taso 1–4 -vaatimuksia vastaan
- Priorisoidun implementaatiosuunnitelman teknologiapinollesi sopivana
- Arvioitu työmäärä vaihetta kohden

**AAIO-audit — 990 EUR**  
Toimittaa [Tekoäly-Dani](https://tekoalydani.com) 5 työpäivässä.

Yhteystiedot: [dani@tekoalydani.com](mailto:dani@tekoalydani.com) | [tekoalydani.com](https://tekoalydani.com)

---

## Yleisimmät virheet

| Virhe | Miksi se epäonnistuu | Mitä tehdä sen sijaan |
|-------|---------------------|----------------------|
| Kaikkien AI-ryömijöiden estäminen robots.txt:ssä | Agentit eivät löydä sinua | Salli oikeutetut agenttiryömijät nimellä |
| CAPTCHA kaikissa tärkeimmissä päätepisteissä | Agentit eivät pysty jatkamaan | Lisää erillinen, CAPTCHA-vapaa API-polku |
| Hinnoittelu piilossa kirjautumisen takana | Agentit eivät pysty vertailemaan | Tarjoa vähintään perushinnoittelu julkisesti |
| Schema.org-data puutteellinen | AI viittaa väärään tietoon | Validoi Google Rich Results Test -työkalulla |
| MCP:n pitäminen valinnaisena | Menetät suurimman osan agentiliikenteestä | Agentit suosivat MCP:tä web-kaappauksen sijaan |
| Agentin virhevastausten huomioimatta jättäminen | Agentit epäonnistuvat hiljaisesti | Palauta jäsennetyt JSON-virheet selkeillä viesteillä |

---

## Katso myös

- [Protokollakartta](protocol-landscape.md) — miten protokollat suhteutuvat toisiinsa
- [AAIO-ydinspesifikaatio](../../specs/aaio-core-v0.1.md) — täydelliset tekniset vaatimukset
