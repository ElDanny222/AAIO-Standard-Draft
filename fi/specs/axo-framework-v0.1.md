# AXO-viitekehys v0.1

**Status:** Luonnos  
**Versio:** 0.1.0  
**Päivämäärä:** 2026-04-09  
**Tekijät:** [Tekoäly-Dani](https://tekoalydani.com)  
**Lisenssi:** Apache 2.0  
**Yläspesifikaatio:** [AAIO-ydinspesifikaatio v0.1](aaio-core-v0.1.md)  

> 🇬🇧 [English version](../../specs/axo-framework-v0.1.md)

---

## Tiivistelmä

Agent Experience Optimization (AXO) on AAIO:n UX/CX-näkökulma. Siinä missä AAIO määrittelee tekniset vaatimukset agenttivalmiille verkkosivustoille, AXO kehystää saman työn sen kautta, **miten AI-agentit kokevat verkkosivuston**. AXO on suunniteltu UX-suunnittelijoille, CX-johtajille, tuoteomistajille ja liiketoimintapäättäjille, jotka tarvitsevat ymmärrystä AAIO:sta käyttäjäkokemuksen ja asiakaspolkujen termein.

---

## 1. Johdanto

### 1.1 Uusi käyttäjä on saapunut

Verkkosivustollasi on uusi käyttäjäkategoria: **AI-agentti**. Toisin kuin ihmiset, jotka selaavat, vierittävät ja tekevät tunnepohjaisia päätöksiä, AI-agentit:

- Jäsentävät rakenteista dataa, eivät visuaalisia asetteluja
- Seuraavat ohjelmallisia polkuja, eivät visuaalisia hierarkioita
- Arvioivat datan täydellisyyttä, eivät esteettistä suunnittelua
- Tekevät päätöksiä spesifikaatioiden, eivät markkinointiviestien perusteella
- Tarvitsevat millisekuntitason vasteaikoja, eivät sujuvia animaatioita

AXO on se käytäntö, jolla suunnitellaan verkostokokemuksia, jotka palvelevat sekä ihmis- että AI-agenttikuluttajia.

### 1.2 AXO vs. perinteinen UX

| Dimensio | Ihmisen UX | Agenttikokemus (AXO) |
|----------|-----------|---------------------|
| **Syöte** | Visuaalinen, auditiivinen, taktinen | Rakenteinen data (JSON, XML, HTML) |
| **Navigointi** | Klikkaus, vieritys, haku | API-kutsut, linkkien seuranta, sivukartan jäsentäminen |
| **Päätöstekijät** | Brändi, muotoilu, tunne, arvostelut | Datan täydellisyys, hintatarkkuus, saatavuus |
| **Nopeusodotus** | 1–3 sekuntia sivulatausta | < 500ms API-vastaus |
| **Virheenkäsittely** | Ihmisluettavat virhesivut | Jäsennetyt virhevastaukset (JSON virhekoodilla) |
| **Tunnistautuminen** | Kirjautumislomakkeet, SSO | API-avaimet, OAuth 2.0 -tokenit |
| **Luottamussignaalit** | Brändin maine, muotoilun laatu | Schema.org-vaatimustenmukaisuus, datan johdonmukaisuus, HTTPS |
| **Konversio** | Lisää ostoskoriin -painike → kassan lomake | Ostoskori-API → Kassa-API → Maksuvahvistus |

### 1.3 Kohdeyleisö

Tämä viitekehys on kirjoitettu:

- **UX/CX-johtajille** digitaalistrategiaa arvioimassa
- **Tuoteomistajille** tiekarttatoimintojen suunnittelussa
- **Digitaalistrategeille** kilpailuaseman arvioinnissa
- **Verkkokauppajohtajille** konversiovirtojen optimoinnissa

Teknisistä toteutuksen yksityiskohdista, katso [AAIO-ydinspesifikaatio](aaio-core-v0.1.md).

---

## 2. Agenttipolku

### 2.1 Agentin asiakaspolun kartoittaminen

Aivan kuten UX-ammattilaiset kartoittavat ihmisten asiakaspolkuja, AXO kartoittaa **agentin asiakaspolun** — vaiheet, jotka AI-ostoagentti käy läpi ensimmäisestä kyselystä suoritettuun transaktioon.

```
Ihmisen asiakaspolku            Agentin asiakaspolku
━━━━━━━━━━━━━━━━━━━━          ━━━━━━━━━━━━━━━━━━━━━━
1. Tietoisuus (mainos, haku)    1. Löytäminen (ryömintä, manifesti)
2. Kiinnostus (selaa, lue)      2. Datan poiminta (jäsennä rakennettua dataa)
3. Harkinta (vertaile)          3. Vertailu (ristiinainestoanalyysi)
4. Aikomus (lisää koriin)       4. Valinta (parhaiten sopiva algoritmi)
5. Osto (kassa)                 5. Transaktio (API-kassa + maksu)
6. Jälkiosto (tuki)             6. Vahvistus (jäsennetty kuitti)
```

### 2.2 Agenttipolun vaiheet

#### Vaihe 1: Löytäminen

**Mitä tapahtuu:** Agentti etsii tuotetta/palvelua ja löytää verkkosivustosi.

**AXO-kysymykset:**
- Voiko agentti löytää sivustosi vastausmoottoreiden, hakurajapintojen tai suoran ryöminnän kautta?
- Ilmoittaako sivustosi kyvykkyydet AAIO-manifestin kautta?
- Onko `llms.txt` tai `ai.txt`, joka auttaa agenttia ymmärtämään tarjoamasi?

**AXO-mittarit:**
- Löytämisaste: % agenttien kyselyistä, joissa sivustosi näkyy ehdokkaana
- Manifiestin täydellisyys: % AAIO-manifestissa ilmoitetuista kyvykkyyksistä

#### Vaihe 2: Datan poiminta

**Mitä tapahtuu:** Agentti lukee tuote-/palvelutiedot sivuiltasi.

**AXO-kysymykset:**
- Voiko agentti poimia kaiken relevantin datan ilman JavaScript-renderöintiä?
- Onko hinnoittelu, saatavuus ja tuotespesifikaatiot rakenteisessa datassa?
- Onko ristiriitoja saman sivun eri esitysten välillä?

**AXO-mittarit:**
- Datan poiminnan onnistumisaste: % datapisteiden onnistuneesta jäsentämisestä
- Datan täydellisyyspisteet: % odotetuista kentistä läsnä rakenteisessa datassa

#### Vaihe 3: Vertailu

**Mitä tapahtuu:** Agentti vertailee tarjoamaasi kilpailijoihin.

**AXO-kysymykset:**
- Sisältääkö rakenteinen datasi kaikki vertailun kannalta relevantit kentät?
- Onko uniikit tunnisteet (SKU, GTIN) läsnä ristiinainestoparitusta varten?
- Onko hinnoittelusi läpinäkyvä ja koneluettava (ei piilotettuja maksuja)?

**AXO-mittarit:**
- Vertailun sisällyttämisaste: % vertailuista, joissa datasi on riittävän täydellinen sisällyttämiseen
- Hintojen läpinäkyvyyspisteet: % kokonaiskustannuksesta näkyvissä rakenteisessa datassa

#### Vaihe 4: Valinta

**Mitä tapahtuu:** Agentti valitsee tuotteesi/palvelusi parhaana vastaavuutena.

**AXO-kysymykset:**
- Ilmoittaako datasi selkeästi erottavat tekijät (takuu, toimitus, arvostelut)?
- Ovatko arvostelut ja arvioinnit Schema.org-muodossa?
- Onko toimitus-/toimitustiedot koneluettavia?

#### Vaihe 5: Transaktio

**Mitä tapahtuu:** Agentti suorittaa oston sivustollasi.

**AXO-kysymykset:**
- Voiko agentti lisätä ostoskoriin ja käydä kassan API:n kautta?
- Onko kassavirta käytettävissä ilman ihmisen väliintuloa?
- Tukeeko maksuprosessi agentin tunnistautumista?

**AXO-mittarit:**
- Transaktioiden onnistumisaste: % yritetyistä transaktioista suoritettuna
- Transaktioaika: sekuntia valinnasta vahvistukseen

#### Vaihe 6: Vahvistus

**Mitä tapahtuu:** Agentti vastaanottaa ja käsittelee tilausvahvistuksen.

**AXO-kysymykset:**
- Onko vahvistus jäsennetty (JSON) vai vain ihmisluettava (HTML-sähköposti)?
- Sisältääkö vahvistus kaikki tilauksen tiedot, joita agentti tarvitsee raportointiin?
- Onko seurantatiedot koneluettavia?

---

## 3. AXO-arviointikehys

### 3.1 AXO-tuloskortti

AXO-tuloskortti kääntää teknisen AAIO-valmiuspisteen liiketoimintaorientoituneiksi mittareiksi, joita UX/CX-tiimit ymmärtävät.

| AXO-dimensio | AAIO-pilari | Liiketoimintakysymys |
|-------------|-------------|---------------------|
| **Löydettävyys** | Löydettävyys | Voivatko AI-agentit löytää meidät? |
| **Ymmärrettävyys** | Koneluettavuus | Voivatko AI-agentit ymmärtää tarjoamamme? |
| **Käytettävyys** | Navigoitavuus | Voivatko AI-agentit navigoida sivustollamme tehokkaasti? |
| **Konvertoitavuus** | Transaktiokykyisyys | Voivatko AI-agentit ostaa meiltä? |
| **Luotettavuus** | Poikkileikkaava | Voivatko AI-agentit luottaa dataaamme? |

### 3.2 AXO-kypsyysmalli

| Taso | Nimi | Kuvaus | Liiketoimintavaikutus |
|------|------|--------|----------------------|
| **Taso 0** | Näkymätön | Ei AXO-optimointia | AI-agentit eivät löydä tai käytä sivustoasi. Menetät jokaisen agenttivälitteisen myynnin. |
| **Taso 1** | Löydettävä | Perus löydettävyys ja rakenteinen data | Agentit voivat löytää sinut, mutta eivät välttämättä poimia riittävästi dataa. |
| **Taso 2** | Vertailtava | Vahva rakenteinen data, agentit voivat vertailla | Agentit sisällyttävät sinut vertailuihin. Voitatko riippuu tarjoamastasi. |
| **Taso 3** | Transaktiokykyinen | API-pohjainen kaupankäynti, agentit voivat ostaa | Agentit voivat suorittaa ostoksia. Kaappaat agenttivälitteistä liikevaihtoa. |
| **Taso 4** | Optimoitu | Täysi AXO A2A-neuvottelulla | Agentit suosivat sivustoasi. Maksimaalinen agenttivälitteinen konversio. |

### 3.3 Kilpailun vaikutukset

Agenttivälitteisessä kaupankäynnissä korkeamman AXO-tason sivusto voittaa suhteettomasti — agentit optimoivat datan laadun ja transaktiotehokkuuden, eivät brändikuvan mukaan.

---

## 4. AXO-suunnitteluperiaatteet

### 4.1 Periaate 1: Kaksikerroksinen suunnittelu

Suunnittele jokainen sivu kahdella kerroksella:

1. **Ihmiskerros**: Visuaalinen muotoilu, markkinointiteksti, kuvat, interaktiiviset elementit
2. **Agenttikerros**: Rakenteinen data, API-päätepisteet, koneluettavat metatiedot

Nämä kerrokset eivät SAA olla ristiriidassa. Agenttikerroksen täytyy olla uskollinen, koneluettava esitys ihmiskerroksesta.

### 4.2 Periaate 2: Data ensin, esitys toiseksi

Agenttikuluttajille rakenteinen data ON kokemus. Investoi:

- Täydellisiin Schema.org-merkintöihin kaikilla relevanteilla kentillä
- Tarkkaan, reaaliaikaiseen hinnoitteluun ja saatavuuteen
- Uniikkeihin tunnisteisiin jokaiselle entiteetille
- Selkeään kategorisoinnin ja taksonomian

### 4.3 Periaate 3: Epäonnistu hallitusti agenteille

Kun asiat menevät pieleen, agentit tarvitsevat:

- **Jäsennetyt virhevastaukset** (JSON virhekoodilla, viestillä ja palautumissuosituksella)
- **Tarkat HTTP-statuskoodit** (ei pehmeitä 404-virheitä, oikeat 301-uudelleenohjaukset)
- **Nopeusrajoitustiedot** (`429` `Retry-After`-otsikolla)
- **Saatavuusvaihtoehdot** ("loppuunmyyty" → "samanlaisia tuotteita" -päätepiste)

### 4.4 Periaate 4: Nopeus on UX agenteille

Agenttikokemus heikkenee jyrkästi yli 500ms vasteajan jälkeen:

| Vasteaika | Agentin havainto |
|-----------|----------------|
| < 200ms | Erinomainen — suosittu lähde |
| 200–500ms | Hyvä — normaalitason sisällytys |
| 500ms–2s | Heikentynyt — voidaan ohittaa aikarajoitteisissa tehtävissä |
| > 2s | Huono — suljettu pois reaaliaikaisista vertailuista |

### 4.5 Periaate 5: Läpinäkyvyys rakentaa luottamusta

Agentit arvioivat luottamuksen datan johdonmukaisuuden kautta:

- Sivun hinta = Schema.org-hinta = API-vastauksen hinta
- Ilmoitettu saatavuus = saatavuus kassaa yritettäessä
- Toimitusarvio on luotettava ja koneluettava
- Palautuskäytäntö on selkeä ja jäsennetty

---

## 5. AXO verkkokaupalle

### 5.1 Tuotesivun AXO-tarkistuslista

| Elementti | Ihmiskerros | Agenttikerros |
|-----------|-------------|--------------|
| Tuotenimi | `<h1>`-otsikko | `schema:name` |
| Hinta | Näkyvä hinnan esittäminen | `schema:price` + `priceCurrency` |
| Saatavuus | "Varastossa"-merkintä | `schema:availability` |
| Kuvaus | Markkinointiteksti | `schema:description` (faktuaalinen) |
| Kuvat | Tuotegalleria | `schema:image` (URL:t) |
| Arvostelut | Tähtiarvio + arvostelut | `schema:aggregateRating` |
| SKU | Usein piilotettu | `schema:sku` (PAKKO olla läsnä) |
| Brändi | Logo + nimi | `schema:brand` |
| Kategoria | Leivänmuru | `schema:category` + `BreadcrumbList` |
| Toimitus | Toimitustietoja osio | `schema:shippingDetails` |
| Palautukset | Palautuskäytäntölinkki | `schema:hasMerchantReturnPolicy` |

### 5.2 Kassavirran AXO

```
Ihmisen kassavirta              Agentin kassavirta
━━━━━━━━━━━━━━━━━━              ━━━━━━━━━━━━━━━━━━━
1. Klikkaa "Lisää koriin"       1. POST /api/ostoskori/lisaa {sku, maara}
2. Katso ostoskorisivu          2. GET /api/ostoskori
3. Syötä toimitusosoite         3. POST /api/kassa {osoite, ...}
4. Valitse maksutapa            4. POST /api/maksu {tapa, token}
5. Vahvista tilaus              5. POST /api/tilaus/vahvista
6. Katso vahvistussivu          6. GET /api/tilaus/{id} → JSON-kuitti
```

---

## 6. AXO-auditointiprosessi

### 6.1 Miten suorittaa AXO-audit

1. **Agentin simulointi**: Navigoi sivusto kuten AI-agentti tekisi — rakenteista dataa, rajapintoja ja sivukarttaa käyttäen
2. **Datan poimintatesti**: Yritä poimia kaikki tuote-/palveludata pelkästään rakenteisesta datasta
3. **Vertailutesti**: Voiko agentti rakentaa täydellisen vertailutaulukon datastasi?
4. **Transaktiotesti**: Voiko agentti suorittaa oston rajapintojen kautta?
5. **Virheenkäsittelytesti**: Miten sivusto vastaa agenttien virheisiin (väärä SKU, loppuunmyyty)?
6. **Nopeustesti**: Mittaa API-vasteajat realistisessa agentiliikenteessä
7. **Johdonmukaisuustesti**: Vertaa dataa ihmiskerroksen, rakenteisen datan ja API-vastausten välillä

---

## 7. AXO:n liiketoimintaperustelu

### 7.1 Markkinaajurit

- **Agenttikaupankäynti** on arvioitu kasvavan 7,3 miljardiin dollariin vuoteen 2028 mennessä (40 %+ CAGR)
- **Sukupolvenvaihdos**: Nuoremmat kuluttajat delegoivat ostopäätöksiä yhä enemmän AI-avustajille
- **B2B-hankinta**: Yritysostajat ottavat käyttöön AI-agentteja toimittajavalinnoissa
- **Ensimover-etu**: AXO-optimointi tänään luo kilpailuvallin agenttikaupankäynnin kasvaessa

### 7.2 ROI-kehys

| Investointi | Odotettu tuotto |
|------------|----------------|
| Schema.org-merkinnät (1–2 viikkoa) | Sisällytetty AI-vertailuihin, AEO-viittaukset |
| API-pohjainen tuoteluettelo (2–4 viikkoa) | Agentti voi poimia ja vertailla kaikkia tuotteita |
| Kassarajapinta (4–8 viikkoa) | Agentti voi suorittaa ostoksia (uusi tulokanava) |
| Täysi AXO-optimointi (8–16 viikkoa) | Maksimaalinen agenttivälitteinen konversio |

### 7.3 Toimimattomuuden riskit

Sivustot ilman AXO-optimointia kohtaavat:

- **Näkymättömyys agenteille**: Ei sisällytetty AI-välitteisiin ostopäätöksiin
- **Dataepäedullinen asema**: Kilpailijat, joilla on parempi rakenteinen data, voittavat agenttien vertailuissa
- **Tulojen vuoto**: Agenttivälitteinen kaupankäynti kasvaa, markkinaosuutesi pysyy tasaisena
- **Jälkikäteinen kiinniotto**: AXO:n myöhempi toteuttaminen on vaikeampaa kuin nyt

---

## 8. AXO ja ihmisten UX: Synergiat

AXO-investointi ei ole erillinen ihmisten UX-parannuksesta:

| AXO-investointi | Ihmisten UX -hyöty |
|----------------|-------------------|
| Schema.org-merkinnät | Rikkaat hakutulokset, parempi SEO |
| Nopeammat API-vastaukset | Nopeammat sivulataukset myös ihmisille |
| Jäsennetty virheenkäsittely | Paremmat virhesivut ihmiskuluttajille |
| Täydellinen tuotedata | Paremmat tuotesivut ihmisselailulle |
| API-pohjainen kassa | Headless-kaupankäynti, mobiilioptimointi |
| Datan johdonmukaisuus | Vähemmän asiakasvalituksia väärästä hinnoittelusta |

AXO ei ole kustannuskeskus, joka kilpailee ihmisten UX:n kanssa — se on kerroin, joka parantaa molempia kanavia samanaikaisesti.

---

## Liite A: AXO-sanasto

| Termi | Määritelmä |
|-------|-----------|
| **AXO** | Agent Experience Optimization — AAIO:n UX-näkökulma |
| **Agenttipolku** | Vaiheet, jotka AI-agentti käy läpi löytämisestä transaktioon |
| **Kaksikerroksinen suunnittelu** | Sivujen suunnitteleminen sekä ihmis- että agenttikerroksella |
| **AXO-tuloskortti** | Liiketoimintaorientoitunut arvio agenttikokemusen laadusta |
| **Konvertoitavuus** | Agentin kyky suorittaa transaktio verkkosivustolla |
| **Dataetu** | Kilpailijoita täydellisempi/tarkempi rakenteinen data |

---

*Tämä viitekehys on osa [AAIO Standard Draft](../../README.md) -projektia, jonka ylläpitäjä on [Tekoäly-Dani](https://tekoalydani.com).*
