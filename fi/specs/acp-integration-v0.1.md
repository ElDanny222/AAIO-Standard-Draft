# Agent Commerce Protocol (ACP) -integrointispesifikaatio

**Versio:** 0.1-luonnos  
**Status:** Luonnos  
**Päivämäärä:** 2026-04-09  
**Tekijät:** Tekoäly-Dani AAIO-työryhmä  

> 🇬🇧 [English version](../../specs/acp-integration-v0.1.md)

---

## Tiivistelmä

Tämä dokumentti määrittelee, miten Agentic AI Optimization (AAIO) -yhteensopivat verkkosivustot toteuttavat Agent Commerce Protocol (ACP) -protokollan mahdollistaakseen turvalliset, autonomiset kone-kone-transaktiot. ACP tarjoaa kuljetuskerroksen käytännöt — HTTP-otsakkeet, tunnistautumisvirrat ja transaktioiden elinkaarenhallinta — jotka mahdollistavat AI-ostoagenttien löytää, neuvotella ja suorittaa maksuja ihmisprinsipaaliensa puolesta.

Tämä spesifikaatio ei määrittele uutta protokollaa. Se profiloi ACP-kehyksen (Stripe & OpenAI:n kehittämä, Apache 2.0 -avoimen standardin mukainen) AAIO-optimointikerroksen sisällä, määrittäen miten verkkokauppa- ja palvelualustat paljastavat ACP-päätepisteet niin, että autonomiset agentit voivat asioida luotettavasti ja turvallisesti.

---

## Tämän dokumentin status

Tämä on luonnosspesifikaatio (v0.1), joka on julkaistu yhteisöarviointia varten. Se ei vielä sovellu tuotantototeutukseen ilman lisävalidointia. Palaute tulisi osoittaa AAIO-Standard-Draft-repositorioon.

---

## 1. Termistö

Tässä asiakirjassa käytetyt avainsanat "PAKKO", "EI SAA", "VAADITTU", "PITÄISI" ja "VOI" tulkitaan [RFC 2119:n](https://www.rfc-editor.org/rfc/rfc2119) mukaisesti.

| Termi | Määritelmä |
|-------|-----------|
| **ACP** | Agent Commerce Protocol — Stripen ja OpenAI:n avoimen standardin (Apache 2.0) mukainen protokolla kone-koneen välisille maksutransaktioille |
| **AAIO** | Agentic AI Optimization — optimointikerros, joka varmistaa, että verkkosivustot ovat löydettäviä, ymmärrettäviä ja asiointikelpoisia autonomisten AI-agenttien kannalta |
| **Ostoagentti** | AI-agentti, joka toimii ihmisprinsipaali puolesta löytääkseen, arvioidakseen ja ostaakseen tuotteita tai palveluita |
| **Kauppiasagentti** | AI-agentti tai ACP-yhteensopiva päätepiste, joka edustaa myyjää ja pystyy käsittelemään agenttien käynnistämiä transaktioita |
| **Ihmisprinsipaali** | Ihminen, joka on delegoinut ostoauktoriteetin ostoagentille |
| **Transaktiokuori** | ACP-otsakeiden ja kuorman täydellinen kokonaisuus, joka muodostaa yksittäisen atomisen transaktiopyynön |
| **Agenttikorostunut** | Kryptografinen token, joka valtuuttaa agentin toimimaan prinsipaali puolesta |

---

## 2. Yleiskatsaus

### 2.1 Ongelmanasettelu

Perinteiset verkkokaupan kassavirrat on suunniteltu ihmisten vuorovaikutusta varten: monivaiheisia lomakkeita, CAPTCHA-haasteita, visuaalisia vahvistuksia. Nämä ovat ylipääsemättömiä esteitä autonomisille AI-agenteille. ACP ratkaisee tämän määrittelemällä koneluettavan transaktioprotokolan, joka toimii rinnakkain (ei korvaten) ihmisille suunnatun kassan kanssa.

### 2.2 Arkkitehtuuri

```
┌─────────────────┐         ┌──────────────────┐         ┌─────────────────┐
│  Ihmisprinsipaali│         │  Ostoagentti     │         │  Kauppias (AAIO)│
│  (delegoi)       │────────>│  (AI-agentti)    │────────>│  ACP-päätepiste │
│                  │         │                  │<────────│                 │
└─────────────────┘         └──────────────────┘         └─────────────────┘
                                    │                            │
                                    │     ACP-otsakkeet          │
                                    │     + Stripe API           │
                                    └────────────────────────────┘
```

---

## 3. ACP-otsakkeiden spesifikaatio

### 3.1 Pyynnön otsakkeet

Kaikkien ACP-transaktiopyynnöt TÄYTYY sisältää seuraavat HTTP-otsakkeet:

| Otsake | Tyyppi | Pakollisuus | Kuvaus |
|--------|--------|-------------|--------|
| `ACP-Version` | Merkkijono | VAADITTU | Protokollaversio. Nykyinen: `"0.1"`. |
| `ACP-Agent-Id` | Merkkijono | VAADITTU | Ostoagentin uniikki tunniste. |
| `ACP-Principal-Id` | Merkkijono | VAADITTU | Ihmisprinsipaali tunniste, jonka puolesta agentti toimii. |
| `ACP-Transaction-Id` | UUID | VAADITTU | Transaktioiden idempotenssiavain. Ostoagentin generoima. |
| `ACP-Intent` | Enum | VAADITTU | Transaktion tarkoitus: `purchase`, `quote`, `hold`, `cancel`. |
| `ACP-Delegation-Token` | Merkkijono | VAADITTU | Kryptografinen todiste delegoinnista prinsipaali-agentti-välillä. |
| `ACP-Callback-Url` | URL | VALINNAINEN | Webhook-URL asynkronisille transaktiostatuksen päivityksille. |
| `ACP-Max-Amount` | Objekti | VALINNAINEN | Maksimi valtuutettu summa (`{"amount": 5000, "currency": "EUR"}`). |
| `ACP-Metadata` | JSON | VALINNAINEN | Mielivaltaiset avain-arvo-metatiedot transaktiolle. |

### 3.2 Vastausotsakkeet

Kauppiaiden ACP-päätepisteiden TÄYTYY palauttaa seuraavat otsakkeet:

| Otsake | Tyyppi | Kuvaus |
|--------|--------|--------|
| `ACP-Version` | Merkkijono | Kauppiaan tukema protokollaversio. |
| `ACP-Transaction-Id` | UUID | Pyyntö-Transaction-Id:n toisto. |
| `ACP-Status` | Enum | Transaktiostatukset: `accepted`, `pending`, `rejected`, `failed`. |
| `ACP-Payment-Id` | Merkkijono | Stripen Payment Intent -ID (kun `ACP-Status` on `accepted` tai `pending`). |
| `ACP-Receipt-Url` | URL | Koneluettava kuitin URL. |
| `ACP-Retry-After` | Kokonaisluku | Sekuntia ennen uudelleenyritystä (kun `ACP-Status` on `pending`). |

---

## 4. Transaktion elinkaari

### 4.1 Tilasiirtymäkaavio

```
  ┌──────────┐
  │  TARJOUS │ ◄── ACP-Intent: quote
  └────┬─────┘
       │ (agentti vahvistaa)
       ▼
  ┌──────────┐
  │   VARAUS │ ◄── ACP-Intent: hold (valinnainen esiauktorisointi)
  └────┬─────┘
       │ (agentti vahvistaa)
       ▼
  ┌──────────┐     ┌──────────┐
  │  OSTO    │────>│ HYVÄKSYTTY│
  └────┬─────┘     └──────────┘
       │
       ├──────────>┌──────────┐
       │           │ ODOTTAA  │──> (asynkroninen vahvistus callbackin kautta)
       │           └──────────┘
       │
       └──────────>┌──────────┐
                   │  HYLÄTTY │
                   └──────────┘
```

### 4.2 Tarjousvirta

Ostoagentin PITÄISI pyytää tarjous ennen ostoitumista. Tarjousvastaus sisältää nykyisen hinnan, saatavuuden ja ehdot.

```http
POST /acp/v0.1/transactions HTTP/1.1
Host: kauppa.example.fi
ACP-Version: 0.1
ACP-Agent-Id: agentti-ostaja-001
ACP-Principal-Id: kayttaja-12345
ACP-Transaction-Id: 550e8400-e29b-41d4-a716-446655440000
ACP-Intent: quote
ACP-Delegation-Token: eyJhbGciOi...
Content-Type: application/json

{
  "items": [
    {
      "sku": "TUOTE-PRO-2026",
      "quantity": 2,
      "schema_ref": "aaio-product/v0.1"
    }
  ],
  "shipping": {
    "country": "FI",
    "postal_code": "00100"
  }
}
```

### 4.3 Ostovirta

```http
POST /acp/v0.1/transactions HTTP/1.1
Host: kauppa.example.fi
ACP-Version: 0.1
ACP-Agent-Id: agentti-ostaja-001
ACP-Principal-Id: kayttaja-12345
ACP-Transaction-Id: 550e8400-e29b-41d4-a716-446655440001
ACP-Intent: purchase
ACP-Delegation-Token: eyJhbGciOi...
ACP-Max-Amount: {"amount": 10000, "currency": "EUR"}
Content-Type: application/json

{
  "items": [
    {
      "sku": "TUOTE-PRO-2026",
      "quantity": 2
    }
  ],
  "payment_method": "pm_card_visa",
  "shipping": {
    "country": "FI",
    "postal_code": "00100",
    "address_line1": "Mannerheimintie 1"
  }
}
```

### 4.4 Idempotenssitakuu

`ACP-Transaction-Id` toimii idempotenssiavaimena. Kauppiaiden TÄYTYY palauttaa sama vastaus duplikaattipyynnöille, joilla on sama Transaction-Id. Idempotenssiikkunan TÄYTYY olla vähintään 24 tuntia.

---

## 5. Tunnistautuminen ja valtuutus

### 5.1 Agentin tunnistautuminen

Ostoagentit tunnistautuvat kauppiaiden ACP-päätepisteisiin käyttäen yhtä seuraavista tavoista (suositusjärjestyksessä):

1. **OAuth2-asiakastunnukset** — SUOSITELTU B2B-agenttiinteraktioihin
2. **API-avain** — Ennalta jaettu API-avain, joka välitetään `Authorization: Bearer <api-key>` -otsakkeella
3. **mTLS** — Keskinäinen TLS arvokkaissa tai säännellyissä transaktioissa

### 5.2 Delegointitodiste

`ACP-Delegation-Token`-otsakkeen TÄYTYY olla allekirjoitettu JWT, joka sisältää:

```json
{
  "iss": "prinsipaali-identiteettitarjoaja",
  "sub": "kayttaja-12345",
  "aud": "agentti-ostaja-001",
  "scope": "purchase",
  "max_amount": {
    "amount": 50000,
    "currency": "EUR"
  },
  "categories": ["elektroniikka", "ohjelmisto"],
  "exp": 1735689600,
  "iat": 1735603200,
  "jti": "delegointi-uuid-tahan"
}
```

Kentät:
- `scope`: TÄYTYY olla yksi: `purchase`, `quote`, `hold`.
- `max_amount`: Maksimi yksittäistransaktion summa, jonka agentti on valtuutettu käyttämään.
- `categories`: VALINNAINEN tuotekategoriorajoitukset.
- `exp`: Delegoinnin vanhentuminen. EI SAA ylittää 30 päivää `iat`-ajankohdasta.

### 5.3 Stripe-integraatio

ACP-transaktiot selvitetään Stripen Payments API:n kautta. Kauppiaan ACP-päätepiste:

1. Validoi ACP-otsakkeet ja delegointitoken
2. Luo Stripe PaymentIntent transaktion tiedoilla
3. Vahvistaa PaymentIntentin käyttäen annettua maksutapaa
4. Palauttaa `ACP-Payment-Id`:n (Stripen PaymentIntent-ID) vastauksessa

---

## 6. AAIO-integrointivaatimukset

### 6.1 Löydettävyys

AAIO-yhteensopivien kauppiaiden TÄYTYY mainostaa ACP-tukea AAIO-manifestissaan (`/.well-known/aaio-manifest.json`):

```json
{
  "aaioVersion": "0.1",
  "protocols": {
    "acp": {
      "version": "0.1",
      "endpoint": "/acp/v0.1/transactions",
      "authentication": ["oauth2_client_credentials", "api_key"],
      "supported_intents": ["quote", "purchase", "hold", "cancel"],
      "supported_currencies": ["EUR", "USD", "GBP"],
      "max_transaction_amount": {
        "EUR": 100000
      }
    }
  }
}
```

### 6.2 Tuotedata

ACP-transaktion kohteiden TÄYTYY viitata `aaio-product.schema.json`- tai `aaio-service.schema.json`-skeemoilla kuvattuihin tuotteisiin. Tämä varmistaa, että ostoagentti voi ohjelmallisesti tarkistaa tuoteominaisuudet ennen transaktioitumista.

---

## 7. Virheenkäsittely

### 7.1 Virhevastauksen muoto

```json
{
  "error": {
    "code": "ACP_INSUFFICIENT_DELEGATION",
    "message": "Delegointitoken ei valtuuta tätä summaa",
    "details": {
      "requested_amount": 15000,
      "max_authorized": 10000,
      "currency": "EUR"
    }
  }
}
```

### 7.2 Virhekoodit

| Koodi | HTTP-status | Kuvaus |
|-------|-------------|--------|
| `ACP_INVALID_HEADER` | 400 | Puuttuva tai muodoltaan väärä ACP-otsake. |
| `ACP_INVALID_VERSION` | 400 | Ei-tuettu ACP-versio. |
| `ACP_INVALID_DELEGATION` | 401 | Delegointitoken on virheellinen, vanhentunut tai peruutettu. |
| `ACP_INSUFFICIENT_DELEGATION` | 403 | Delegoinnin laajuus ei kata pyydettyä toimintoa. |
| `ACP_AGENT_NOT_AUTHORIZED` | 403 | Agentti ei ole rekisteröity tai valtuutettu tällä kauppiaalla. |
| `ACP_DUPLICATE_TRANSACTION` | 409 | Transaction-Id on jo käsitelty eri parametreilla. |
| `ACP_ITEM_UNAVAILABLE` | 422 | Pyydetty tuote on loppuunmyyty tai lopetettu. |
| `ACP_AMOUNT_EXCEEDED` | 422 | Transaktion summa ylittää ACP-Max-Amount tai delegointirajan. |
| `ACP_PAYMENT_FAILED` | 502 | Stripen maksunkäsittely epäonnistui. |
| `ACP_MERCHANT_UNAVAILABLE` | 503 | Kauppiaan ACP-päätepiste tilapäisesti poissa käytöstä. |

---

## 8. Turvallisuusnäkökohdat

### 8.1 Delegointitokenien turvallisuus

- Delegointitokenit TÄYTYY olla lyhytikäisiä (enintään 30 päivää).
- Tokenien TÄYTYY olla rajattu tiettyihin kategorioihin ja enimmäissummiin.
- Kauppiaiden TÄYTYY validoida tokenin allekirjoitus liikkeeseenlaskijan julkisen avaimen avulla.
- Tokenit EI SAA olla uudelleenkäytettäviä eri kauppiailla.

### 8.2 Transaktion turvallisuus

- Kaiken ACP-kommunikaation TÄYTYY tapahtua TLS 1.2:n tai uudemman kautta.
- `ACP-Transaction-Id`:n TÄYTYY olla kryptografisesti satunnainen UUID v4.
- Kauppiaiden TÄYTYY toteuttaa nopeusrajoitukset `ACP-Agent-Id`-kohtaisesti (SUOSITELTU: 100 transaktiota tunnissa per agentti).

### 8.3 Kirjanpito

- Kauppiaiden TÄYTYY kirjata kaikki ACP-transaktiot täysin otsakkeineen vähintään 7 vuodeksi (PCI DSS -vaatimusten mukaisesti).
- Lokien TÄYTYY sisältää: aikaleima, ACP-Agent-Id, ACP-Principal-Id, ACP-Transaction-Id, ACP-Intent, summa ja ACP-Status.

### 8.4 Petosten estäminen

- Kauppiaiden PITÄISI integroitua Stripe Radariin agenttien käynnistämien transaktioiden automaattiseen petostentunnistukseen.
- Ihmisrinsipaaleilla TÄYTYY olla mahdollisuus peruuttaa agentin delegointi milloin tahansa, mitätöiden kaikki voimassa olevat delegointitokenit.

### 8.5 Tietosuoja

- `ACP-Principal-Id`-tunnisteen PITÄISI olla pseudonyymi tunniste, ei henkilökohtaisesti tunnistettava arvo.
- Kauppiaiden EI SALLITA jakaa prinsipaali-identiteettiä eri transaktioiden välillä tai kolmansien osapuolten kanssa, paitsi maksun käsittelyn kannalta välttämättömässä laajuudessa.

---

## 9. Vaatimustenmukaisuus

Toteutus on tämän spesifikaation mukainen, jos se:

1. Toteuttaa kaikki VAADITUT ACP-pyyntö- ja vastausotsakkeet (luku 3).
2. Tukee vähintään `quote`- ja `purchase`-tarkoituksia (luku 4).
3. Validoi delegointitokenit luvun 5.2 mukaisesti.
4. Mainostaa ACP-tukea AAIO-manifestissa (luku 6.1).
5. Viittaa AAIO-tuote-/palveluskeemoihin transaktiotuotteille (luku 6.2).
6. Toteuttaa kaikki luvussa 7.2 määritellyt virhekoodit.
7. Täyttää kaikki luvun 8 turvallisuusvaatimukset.

---

## 10. Viitteet

### Normatiiviset viitteet

- [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) — Avainsanat RFC-dokumentteja varten
- [RFC 7519](https://www.rfc-editor.org/rfc/rfc7519) — JSON Web Token (JWT)
- [RFC 6749](https://www.rfc-editor.org/rfc/rfc6749) — OAuth 2.0 -valtuutuskehys
- [Stripe Payments API](https://docs.stripe.com/api/payment_intents) — PaymentIntent API -viite
- [AAIO Core Specification](aaio-core-v0.1.md) — Agentic AI Optimization -ydinstandardi

### Informatiiviset viitteet

- [A2A Commerce Protocol Profile](a2a-commerce-v0.1.md) — Agentti-agentti-kaupankäynti
- [UCP Integration Specification](ucp-integration-v0.1.md) — Universal Commerce Protocol
- [PCI DSS v4.0](https://www.pcisecuritystandards.org/) — Maksukorttialan tietoturvastandardi

---

*Tekijänoikeus 2026 Tekoäly-Dani. Lisenssoitu Apache 2.0:lla.*
