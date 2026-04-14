# A2A Commerce Protocol Profile

**Versio:** 0.1-luonnos  
**Status:** Luonnos  
**Päivämäärä:** 2026-04-09  
**Tekijät:** Tekoäly-Dani AAIO Working Group  

> 🇬🇧 [English version](../../specs/a2a-commerce-v0.1.md)

---

## Tiivistelmä

Tämä dokumentti määrittelee kauppaprofiinin Agent-to-Agent (A2A) -protokollalle (Linux Foundation, v1.0). Se kuvaa, miten ostaja- ja myyjäagentit käyttävät A2A-protokollaa löytääkseen toisensa, neuvotellakseen ehdoista, suorittaakseen ostoksia ja hallinnoidakseen jälkitapahtumaprosesseja. Profiili lisää kauppakohtaiset käytännöt — AgentCard-laajennukset, neuvottelutehtävävuot ja artefaktiskeemaatit — A2A-perusspesifikaation päälle.

Tämä spesifikaatio ei muuta A2A-protokollaa. Se määrittelee rajoitetun käyttöprofiilin AAIO-optimointikerroksen sisällä varmistaen yhteentoimivuuden eri alustoille rakennettujen autonomisten kauppa-agenttien välillä.

## Tämän dokumentin tila

Tämä on luonnosspesifikaatio (v0.1), joka on julkaistu yhteisön kommentointia varten. Se ei vielä sovellu tuotantototeutukseen ilman lisävalidointia. Palaute tulee osoittaa AAIO-Standard-Draft-repositorioon.

## Sisällysluettelo

1. [Terminologia](#1-terminologia)
2. [Yleiskatsaus](#2-yleiskatsaus)
3. [AgentCard kaupankäyntiä varten](#3-agentcard-kaupank%C3%A4ynti%C3%A4-varten)
4. [Neuvotteluprotokolla](#4-neuvotteluprotokolla)
5. [Tehtävän elinkaari kaupassa](#5-teht%C3%A4v%C3%A4n-elinkaari-kaupassa)
6. [Viesti- ja artefaktiskeemaatit](#6-viesti--ja-artefaktiskeemaatit)
7. [Monivaiheinen neuvottelu](#7-monivaiheinen-neuvottelu)
8. [AAIO-integrointivaatimukset](#8-aaio-integrointivaatimukset)
9. [Tietoturvanäkökohdat](#9-tietoturvan%C3%A4k%C3%B6kohdat)
10. [Vaatimustenmukaisuus](#10-vaatimustenmukaisuus)
11. [Viitteet](#11-viitteet)

---

## 1. Terminologia

Avainsanat "PAKKO" (MUST), "EI SAA" (MUST NOT), "VAADITTU" (REQUIRED), "TULEE" (SHALL), "EI TULE" (SHALL NOT), "PITÄISI" (SHOULD), "EI PITÄISI" (SHOULD NOT), "SUOSITELTU" (RECOMMENDED), "VOI" (MAY) ja "VALINNAINEN" (OPTIONAL) tässä dokumentissa tulee tulkita [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) -standardin mukaisesti.

| Termi | Määritelmä |
|-------|------------|
| **A2A** | Agent-to-Agent -protokolla — Linux Foundationin avoin standardi agenttien yhteentoimivuudelle (v1.0). |
| **AAIO** | Agentic AI Optimization — optimointikerros autonomisten AI-agenttien ja verkkosivustojen vuorovaikutukselle. |
| **Ostaja-agentti** | AI-agentti, joka toimii ihmisen tai organisaation puolesta hankkiakseen tuotteita tai palveluita. |
| **Myyjä-agentti** | AI-agentti, joka edustaa kauppiasta ja pystyy antamaan tarjouksia, neuvottelemaan ehdoista ja käsittelemään tilauksia. |
| **AgentCard** | A2A:n julkinen metadatadokumentti (`.well-known/agent.json`), joka kuvaa agentin kyvykkyydet ja jota laajennetaan tässä kaupankäyntiä varten. |
| **Neuvottelusessio** | `context_id`-ryhmitelty sarja A2A-tehtäviä, jotka muodostavat monivaiheisen kauppaneuvottelun. |
| **Kauppa-artefakti** | Tehtävän artefakti, joka sisältää jäsennettyä kauppietoa (tarjous, tilaus, lasku). |
| **RFQ** | Request for Quote (tarjouspyyntö) — ostajan alkuviesti, jossa pyydetään hinnoittelua ja ehtoja. |

## 2. Yleiskatsaus

### 2.1 Ongelma

A2A-protokolla tarjoaa yleiskäyttöisen agenttien välisen viestinnän: tehtävien luomisen, viestinvaihdon ja artefaktien toimittamisen. Kaupankäynti-interaktiot vaativat kuitenkin erityisiä käytäntöjä: miten ostaja-agentti löytää myyjä-agentin, joka tarjoaa tuotteita? Miten hinnoista neuvotellaan? Miltä tilausvahvistusartefakti näyttää? Ilman kauppaprofiilia jokainen toteutus keksii omat käytäntönsä, mikä rikkoo yhteentoimivuuden.

### 2.2 Arkkitehtuuri

```
┌────────────────┐                                ┌────────────────┐
│  Ostaja-agentti│                                │  Myyjä-agentti │
│  (AI-agentti)  │                                │  (AI-agentti)  │
│                │   A2A-protokolla (HTTP+JSON)   │                │
│  Löytää        │───────────────────────────────>│  Julkaisee     │
│  AgentCardin   │   SendMessage (RFQ)            │  AgentCardin   │
│  kautta        │<───────────────────────────────│  .well-known   │
│                │   Tehtäväartefakti (Tarjous)   │  -osoitteessa  │
│  Arvioi        │───────────────────────────────>│                │
│  tarjouksen    │   SendMessage (PurchaseOrder)  │  Käsittelee    │
│                │<───────────────────────────────│  tilauksen     │
│  Vastaanottaa  │   Tehtäväartefakti (Vahvistus) │                │
│  vahvistuksen  │                                │  Käynnistää    │
└────────────────┘                                │  ACP:n         │
         │                                        └────────────────┘
         │              ┌──────────────┐                  │
         └─────────────>│  ACP-maksu   │<─────────────────┘
                        │  (Stripe)    │
                        └──────────────┘
```

### 2.3 Suhde A2A-perusspesifikaatioon

Tämä profiili käyttää seuraavia A2A v1.0 -primitiivejä:

| A2A-primitiivi | Kauppakäyttö |
|----------------|--------------|
| `SendMessage` | Ostaja lähettää RFQ:n ja tilauksen; myyjä lähettää tarjoukset ja vahvistukset. |
| `GetTask` | Tarkistaa tilauksen tai neuvottelun tilan. |
| `SubscribeToTask` | Reaaliaikaiset päivitykset tilauksen käsittelystä. |
| `context_id` | Ryhmittelee kaikki viestit neuvottelusessioon. |
| `artifacts` | Kantavat jäsennettyä kauppietoa (tarjoukset, tilaukset, laskut). |
| `AgentCard` | Mainostaa kauppakyvykkyydet ja tuetut tuotekategoriat. |
| `AgentExtension` | Julistaa `aaio-commerce`-laajennuksen. |

## 3. AgentCard kaupankäyntiä varten

### 3.1 Myyjä-agentin AgentCard

Myyjä-agentin AgentCardissa PAKKO olla `aaio-commerce`-laajennus ja vähintään yksi kauppaan liittyvä taito:

```json
{
  "name": "ShopBot",
  "description": "AI-myyntiagentti WidgetCorpille — käsittelee tuotekyselyt, tarjoukset ja tilaukset",
  "url": "https://shop.example.com/.well-known/agent.json",
  "version": "1.0.0",
  "capabilities": {
    "streaming": true,
    "pushNotifications": true
  },
  "skills": [
    {
      "id": "product-catalog",
      "name": "Tuotekatalogi",
      "description": "Selaa ja hae tuotekatalogia",
      "tags": ["commerce", "catalog", "search"],
      "examples": [
        "Näytä kaikki widgetit alle 50 EUR",
        "Mitä ammattitason widgettejä teillä on?"
      ]
    },
    {
      "id": "quote",
      "name": "Pyydä tarjous",
      "description": "Hanki hinnoittelu ja saatavuus tietyille tuotteille",
      "tags": ["commerce", "quote", "pricing"],
      "examples": [
        "Tarjous 100 kpl Widget Pro",
        "Mikä on bulktihinnoittelu Widget Prolle?"
      ]
    },
    {
      "id": "purchase",
      "name": "Tee tilaus",
      "description": "Suorita ostotilaus ACP-maksulla",
      "tags": ["commerce", "purchase", "order"],
      "examples": [
        "Tilaa 50 kpl Widget Pro, toimitus Helsinkiin",
        "Osta tilausnumerolla PO-2026-001"
      ]
    },
    {
      "id": "order-status",
      "name": "Tilauksen tila",
      "description": "Tarkista olemassa olevan tilauksen tila",
      "tags": ["commerce", "status", "tracking"],
      "examples": [
        "Mikä on tilauksen ORD-12345 tila?",
        "Seuraa lähetystäni"
      ]
    }
  ],
  "defaultInputModes": ["application/json", "text/plain"],
  "defaultOutputModes": ["application/json", "text/plain"],
  "security": [
    {
      "type": "oauth2",
      "flows": {
        "clientCredentials": {
          "tokenUrl": "https://shop.example.com/oauth/token",
          "scopes": {
            "catalog:read": "Selaa tuotekatalogia",
            "quote:create": "Pyydä hintoja",
            "order:create": "Tee ostotilauksia",
            "order:read": "Tarkista tilauksen tila"
          }
        }
      }
    }
  ],
  "extensions": {
    "aaio-commerce": {
      "version": "0.1",
      "role": "seller",
      "supported_protocols": ["acp", "ucp"],
      "categories": ["electronics/widgets", "electronics/accessories"],
      "currencies": ["EUR", "USD"],
      "regions": ["FI", "SE", "NO", "DK", "EE", "DE"],
      "ucp_endpoint": "/ucp/v0.1/products",
      "acp_endpoint": "/acp/v0.1/transactions"
    }
  }
}
```

### 3.2 Ostaja-agentin AgentCard

Ostaja-agentin AgentCard mainostaa hankintakyvykkyydet:

```json
{
  "name": "ProcureBot",
  "description": "AI-hankinta-agentti — etsii, vertaa ja ostaa tuotteita asiakkaiden puolesta",
  "url": "https://buyer.example.com/.well-known/agent.json",
  "skills": [
    {
      "id": "sourcing",
      "name": "Tuotehankinta",
      "description": "Etsi ja vertaa tuotteita useilta myyjiltä",
      "tags": ["commerce", "sourcing", "comparison"]
    },
    {
      "id": "negotiation",
      "name": "Hintaneuvottelu",
      "description": "Neuvottele hinnoittelusta ja ehdoista myyjä-agenttien kanssa",
      "tags": ["commerce", "negotiation", "pricing"]
    }
  ],
  "extensions": {
    "aaio-commerce": {
      "version": "0.1",
      "role": "buyer",
      "max_budget": {
        "currency": "EUR",
        "amount": 1000000
      },
      "preferred_payment": "acp"
    }
  }
}
```

### 3.3 Laajennusskeema

`aaio-commerce`-laajennuksen kentät:

| Kenttä | Tyyppi | Vaadittu | Kuvaus |
|--------|--------|----------|--------|
| `version` | String | VAADITTU | Kauppaprofiilin versio (esim. `"0.1"`). |
| `role` | Enum | VAADITTU | `"buyer"` tai `"seller"`. |
| `supported_protocols` | Array | VAADITTU (myyjä) | Maksu-/dataprotokolat: `["acp", "ucp"]`. |
| `categories` | Array | SUOSITELTU (myyjä) | Tarjotut tuote-/palvelukategoriat. |
| `currencies` | Array | VAADITTU (myyjä) | Tuetut valuutat (ISO 4217). |
| `regions` | Array | SUOSITELTU | Maantieteelliset alueet (ISO 3166-1). |
| `ucp_endpoint` | String | SUOSITELTU (myyjä) | Polku UCP-katalogipäätteeseen. |
| `acp_endpoint` | String | SUOSITELTU (myyjä) | Polku ACP-transaktiopäätteeseen. |
| `max_budget` | Object | VALINNAINEN (ostaja) | Enimmäisbudjetti transaktiolle. |
| `preferred_payment` | String | VALINNAINEN (ostaja) | Ensisijainen maksuprotokolla. |

## 4. Neuvotteluprotokolla

### 4.1 Viestityypit

Kaupan A2A-viestit käyttävät jäsennettyjä JSON-osia MIME-tyypillä
`application/vnd.aaio.commerce.v0.1+json`. Viestin `type`-kenttä
määrittää kauppatoiminnon:

| Tyyppi | Suunta | Kuvaus |
|--------|--------|--------|
| `rfq` | Ostaja → Myyjä | Tarjouspyyntö — määrittelee tuotteet ja halutut ehdot. |
| `quote` | Myyjä → Ostaja | Hinnasto ehdoilla, voimassaoloajalla ja ehdoilla. |
| `counter_offer` | Kumpi tahansa → Kumpi tahansa | Muutetut ehdot vastauksena tarjoukseen. |
| `purchase_order` | Ostaja → Myyjä | Vahvistettu tilaus maksutiedoilla. |
| `order_confirmation` | Myyjä → Ostaja | Hyväksytty tilaus toimitustiedoilla. |
| `order_rejection` | Myyjä → Ostaja | Hylätty tilaus syineen. |
| `invoice` | Myyjä → Ostaja | Maksulasku transaktiosta. |
| `shipping_update` | Myyjä → Ostaja | Toimitus- ja seurantatiedot. |
| `cancellation` | Kumpi tahansa → Kumpi tahansa | Pyyntö peruuttaa tilaus tai neuvottelu. |

### 4.2 RFQ (Tarjouspyyntö)

```json
{
  "role": "user",
  "parts": [
    {
      "type": "data",
      "mimeType": "application/vnd.aaio.commerce.v0.1+json",
      "data": {
        "type": "rfq",
        "rfq_id": "RFQ-2026-001",
        "items": [
          {
            "product_id": "prod_widget_pro_2026",
            "quantity": 100,
            "required_by": "2026-05-01"
          }
        ],
        "shipping": {
          "country": "FI",
          "postal_code": "00100",
          "method": "standard"
        },
        "payment_terms": "net_30",
        "valid_until": "2026-04-16T23:59:59Z"
      }
    }
  ]
}
```

### 4.3 Tarjousvastaus

```json
{
  "role": "agent",
  "parts": [
    {
      "type": "data",
      "mimeType": "application/vnd.aaio.commerce.v0.1+json",
      "data": {
        "type": "quote",
        "quote_id": "QUO-2026-001",
        "rfq_reference": "RFQ-2026-001",
        "items": [
          {
            "product_id": "prod_widget_pro_2026",
            "quantity": 100,
            "unit_price": {
              "amount": 3999,
              "currency": "EUR"
            },
            "total_price": {
              "amount": 399900,
              "currency": "EUR"
            },
            "availability": "in_stock",
            "lead_time_days": 3
          }
        ],
        "shipping_cost": {
          "amount": 2500,
          "currency": "EUR"
        },
        "total": {
          "amount": 402400,
          "currency": "EUR"
        },
        "payment_terms": "net_30",
        "valid_until": "2026-04-16T23:59:59Z",
        "conditions": [
          "Hinnat riippuvat varastosaldosta tilaushetkellä",
          "Volyymialennus sovellettu 100+ yksikön tilauksille"
        ]
      }
    }
  ]
}
```

### 4.4 Ostotilaus

```json
{
  "role": "user",
  "parts": [
    {
      "type": "data",
      "mimeType": "application/vnd.aaio.commerce.v0.1+json",
      "data": {
        "type": "purchase_order",
        "po_number": "PO-2026-001",
        "quote_reference": "QUO-2026-001",
        "acp_transaction_id": "550e8400-e29b-41d4-a716-446655440001",
        "items": [
          {
            "product_id": "prod_widget_pro_2026",
            "quantity": 100,
            "agreed_unit_price": {
              "amount": 3999,
              "currency": "EUR"
            }
          }
        ],
        "shipping": {
          "country": "FI",
          "postal_code": "00100",
          "address_line1": "Mannerheimintie 1",
          "city": "Helsinki",
          "method": "standard"
        },
        "billing": {
          "company": "BuyerCorp Oy",
          "vat_id": "FI12345678",
          "address": "Aleksanterinkatu 10, 00100 Helsinki"
        }
      }
    }
  ]
}
```

## 5. Tehtävän elinkaari kaupassa

### 5.1 Vastaavuus A2A-tehtävätiloihin

| Kauppavaihe | A2A-tehtävätila | Kuvaus |
|-------------|-----------------|--------|
| RFQ lähetetty | `SUBMITTED` | Ostaja on lähettänyt tarjouspyynnön. |
| Tarjousta valmistellaan | `WORKING` | Myyjä laskee hinnoittelua. |
| Tarjous lähetetty, odotetaan ostajaa | `INPUT_REQUIRED` | Myyjä odottaa ostajan päätöstä. |
| Ostotilaus lähetetty | `WORKING` | Myyjä käsittelee tilausta. |
| Maksu vaaditaan | `AUTH_REQUIRED` | ACP-maksu täytyy suorittaa. |
| Tilaus vahvistettu | `COMPLETED` | Transaktio onnistuneesti suoritettu. |
| Tilaus hylätty | `REJECTED` | Myyjä hylkäsi tilauksen. |
| Peruutus | `CANCELED` | Jompikumpi osapuoli peruutti. |
| Virhe | `FAILED` | Korjaamaton virhe käsittelyn aikana. |

### 5.2 Kontekstiryhmittely

Kaikkien yksittäiseen neuvotteluun kuuluvien viestien PAKKO jakaa sama `context_id`.
Tämä mahdollistaa molemmille agenteille:

- Koko neuvotteluhistorian hakemisen `ListTasks`-komennolla suodatettuna `context_id`:llä.
- Keskeytettyjen neuvottelujen jatkamisen.
- Aiempien tarjousten ja vastatarjousten viittaamisen.

Esimerkki kontekstivirrasta:

```
context_id: "negotiation-2026-04-09-buyer001-seller001"

Tehtävä 1: RFQ (SUBMITTED → WORKING → INPUT_REQUIRED)
  ├── Viesti: RFQ ostajalta
  ├── Viesti: Tarjous myyjältä
  └── Artefakti: tarjousdokumentti

Tehtävä 2: Vastatarjous (SUBMITTED → WORKING → INPUT_REQUIRED)
  ├── Viesti: Vastatarjous ostajalta
  └── Viesti: Tarkistettu tarjous myyjältä

Tehtävä 3: Ostotilaus (SUBMITTED → WORKING → COMPLETED)
  ├── Viesti: Ostotilaus ostajalta
  ├── Viesti: Tilausvahvistus myyjältä
  └── Artefakti: tilausvahvistus
```

### 5.3 Artefaktit

Kauppa-artefaktit ovat tehtäviin liitettyjä jäsennettyjä dataobjekteja:

| Artefaktityyppi | MIME-tyyppi | Kuvaus |
|-----------------|-------------|--------|
| `quote` | `application/vnd.aaio.commerce.quote.v0.1+json` | Virallinen hintajatarjous. |
| `order-confirmation` | `application/vnd.aaio.commerce.order.v0.1+json` | Vahvistetun tilauksen tiedot. |
| `invoice` | `application/vnd.aaio.commerce.invoice.v0.1+json` | Maksulasku. |
| `shipping-label` | `application/pdf` | Lähetysetiketti (tarvittaessa). |

## 6. Viesti- ja artefaktiskeemaatit

### 6.1 Tarjousartefaktin skeema

```json
{
  "type": "quote",
  "quote_id": "QUO-2026-001",
  "seller": {
    "agent_id": "seller-agent-001",
    "company": "WidgetCorp",
    "vat_id": "FI98765432"
  },
  "buyer": {
    "agent_id": "buyer-agent-001",
    "company": "BuyerCorp Oy"
  },
  "items": [
    {
      "product_id": "prod_widget_pro_2026",
      "name": "Widget Pro 2026",
      "quantity": 100,
      "unit_price": {"amount": 3999, "currency": "EUR"},
      "total": {"amount": 399900, "currency": "EUR"},
      "aaio_schema_ref": "aaio-product/v0.1"
    }
  ],
  "subtotal": {"amount": 399900, "currency": "EUR"},
  "shipping": {"amount": 2500, "currency": "EUR"},
  "tax": {"amount": 96576, "currency": "EUR", "rate": 0.24},
  "total": {"amount": 498976, "currency": "EUR"},
  "payment_terms": "net_30",
  "valid_until": "2026-04-16T23:59:59Z",
  "created_at": "2026-04-09T12:00:00Z"
}
```

### 6.2 Tilausvahvistusartefaktin skeema

```json
{
  "type": "order_confirmation",
  "order_id": "ORD-2026-001",
  "po_reference": "PO-2026-001",
  "quote_reference": "QUO-2026-001",
  "acp_transaction_id": "550e8400-e29b-41d4-a716-446655440001",
  "acp_payment_id": "pi_3ABC123",
  "status": "confirmed",
  "items": [
    {
      "product_id": "prod_widget_pro_2026",
      "quantity": 100,
      "unit_price": {"amount": 3999, "currency": "EUR"}
    }
  ],
  "total": {"amount": 498976, "currency": "EUR"},
  "estimated_delivery": "2026-04-12",
  "shipping_method": "standard",
  "tracking_url": null,
  "created_at": "2026-04-09T12:30:00Z"
}
```

## 7. Monivaiheinen neuvottelu

### 7.1 Vastatarjousvirta

Kun ostaja-agentti haluaa neuvotella ehdoista:

1. Ostaja vastaanottaa tarjouksen (tehtävä siirtyy `INPUT_REQUIRED`-tilaan).
2. Ostaja lähettää `counter_offer`-viestin muutetuilla ehdoilla.
3. Myyjä arvioi ja vastaa joko:
   - Tarkistetulla `quote`-viestillä (neuvottelu jatkuu).
   - `order_rejection`-viestillä syineen (neuvottelu epäonnistuu).
   - Hyväksymällä vastatarjouksen ehdot (ostaja siirtyy ostotilaukseen).

### 7.2 Vastatarjousviesti

```json
{
  "type": "counter_offer",
  "quote_reference": "QUO-2026-001",
  "proposed_changes": {
    "items": [
      {
        "product_id": "prod_widget_pro_2026",
        "requested_unit_price": {"amount": 3500, "currency": "EUR"},
        "justification": "Kilpailijan tarjous 3600 EUR/yksikkö vastaavalle tuotteelle"
      }
    ],
    "requested_payment_terms": "net_60",
    "requested_shipping": "express"
  }
}
```

### 7.3 Neuvottelurajoitukset

- Agenttien PITÄISI rajoittaa neuvottelu enintään 5 vastatarjouskierrokseen.
- Rajan jälkeen myyjä-agentin PITÄISI esittää lopullinen "ota tai jätä" -tarjous.
- Ostaja-agenttien PAKKO noudattaa tarjousten `valid_until`-aikaleimoja. Vanhentuneet tarjoukset vaativat uuden RFQ:n.

### 7.4 Push-ilmoitukset asynkroniseen neuvotteluun

Asynkronisille neuvotteluille (joissa agentit eivät välttämättä pollaa jatkuvasti):

1. Ostaja rekisteröi push-ilmoituspäätteen tehtävälle:
   ```
   POST /tasks/{taskId}/pushNotifications
   {
     "url": "https://buyer.example.com/webhooks/a2a",
     "events": ["task_state_changed", "message_received"]
   }
   ```
2. Myyjä lähettää tehtäväpäivitykset rekisteröidyn webhookin kautta.
3. Ostaja käsittelee päivitykset ja vastaa kun on valmis.

## 8. AAIO-integrointivaatimukset

### 8.1 Löydettävyys

Myyjä-agenttien PAKKO olla löydettävissä seuraavasti:

1. **AgentCard** osoitteessa `/.well-known/agent.json` `aaio-commerce`-laajennuksella.
2. **AAIO-manifesti** osoitteessa `/.well-known/aaio-manifest.json` listaamalla A2A-tuki:

```json
{
  "aaioVersion": "0.1",
  "protocols": {
    "a2a": {
      "version": "1.0",
      "agent_card_url": "/.well-known/agent.json",
      "role": "seller",
      "commerce_profile": "0.1",
      "categories": ["electronics/widgets"],
      "supported_message_types": ["rfq", "quote", "purchase_order", "counter_offer"]
    }
  }
}
```

### 8.2 Protokollojen välinen virta

Täydellinen AAIO-kauppavirta kaikilla kolmella protokollalla:

```
1. Löydettävyys:  Ostaja löytää myyjän AgentCardin kautta (A2A)
2. Katalogi:      Ostaja selaa tuotteita UCP-päätteiden kautta
3. Neuvottelu:    Ostaja ja myyjä neuvottelevat A2A-viestien kautta
4. Maksu:         Ostaja maksaa ACP:n kautta (Stripe)
5. Vahvistus:     Myyjä vahvistaa A2A-artefaktilla
6. Toimitus:      Myyjä lähettää toimitusilmoitukset A2A:n kautta
```

### 8.3 Datajohdonmukaisuus

- Tuoteviittausten A2A-kauppaviestissä PAKKO käyttää samaa `product_id`:tä
  kuin UCP-katalogissa.
- Tarjousten hinnoittelun PAKKO olla johdonmukainen nykyisten UCP-tietojen kanssa
  (tarjouksen voimassaoloajan sisällä).
- Ostotilauksessa viitatun ACP:n `Transaction-Id`:n PAKKO täsmätä todelliseen
  ACP-transaktioon.

## 9. Tietoturvanäkökohdat

### 9.1 Agentin autentikointi

- Ostaja- ja myyjä-agenttien PAKKO autentikoida myyjän AgentCardin `security`-osiossa
  ilmoitetulla tavalla.
- OAuth2 Client Credentials -virta on SUOSITELTU B2B-kaupankäynnille.

### 9.2 Viestin eheys

- Agenttien PITÄISI käyttää `AgentCardSignature`-allekirjoitusta (JWS) toistensa
  AgentCardien aitouden varmentamiseen.
- Rahoitustietoja sisältävät kauppaviestit PITÄISI allekirjoittaa lähettävän
  agentin toimesta.

### 9.3 Transaktiosidonta

- Ostotilauksessa olevan `acp_transaction_id`:n PAKKO olla ostaja-agentin luoma
  ja käytettävä johdonmukaisesti A2A-neuvottelun ja ACP-maksun välillä.
- Myyjä-agenttien PAKKO varmentaa, että ACP-maksu vastaa sovittuja ehtoja
  ennen tilauksen vahvistamista.

### 9.4 Pyyntömäärien rajoittaminen

- Myyjä-agenttien PITÄISI toteuttaa pyyntömäärien rajoittaminen RFQ-lähetyksille
  (SUOSITELTU: 10 RFQ:ta per agentti per tunti).
- Neuvottelukierrosten PITÄISI olla aikarajoitettuja (SUOSITELTU: 24 tunnin
  vastausikkuna per kierros).

### 9.5 Yksityisyys

- Agenttien väliset viestit EIVÄT SAA sisältää salaamatonta henkilötietoa
  enemmän kuin on välttämätöntä transaktion kannalta (toimitusosoite, laskutustiedot).
- Agenttien PITÄISI tukea päästä-päähän-salausta maksutietoja sisältäville viesteille.

### 9.6 Riidanratkaisu

- Molempien agenttien PAKKO säilyttää täydellinen neuvotteluhistoria (kaikki tehtävät
  ja viestit `context_id`:n sisällä) vähintään 2 vuotta.
- Tilausvahvistusartefaktit toimivat sitovana sopimuksena osapuolten välillä.

## 10. Vaatimustenmukaisuus

Toteutus on tämän spesifikaation mukainen, jos se:

1. Julkaisee AgentCardin `aaio-commerce`-laajennuksella (Luku 3).
2. Tukee vähintään `rfq`-, `quote`- ja `purchase_order`-viestityyppejä (Luku 4).
3. Kartoittaa kauppavaiheet A2A-tehtävätiloihin Luvun 5.1 mukaisesti.
4. Ryhmittelee neuvotteluviestit yhteisen `context_id`:n alle (Luku 5.2).
5. Käyttää määriteltyjä artefakti-MIME-tyyppejä (Luku 5.3).
6. Mainostaa kauppakyvykkyydet AAIO-manifestissa (Luku 8.1).
7. Täyttää kaikki Luvun 9 tietoturvavaatimukset.

## 11. Viitteet

### Normatiiviset viitteet

- [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) — Avainsanat RFC-käytössä
- [A2A Protocol Specification v1.0](https://github.com/a2aproject/A2A/blob/main/specification/a2a.proto) — Agent-to-Agent-protokolla (Linux Foundation)
- [RFC 7519](https://www.rfc-editor.org/rfc/rfc7519) — JSON Web Token (JWT)
- [RFC 7515](https://www.rfc-editor.org/rfc/rfc7515) — JSON Web Signature (JWS)
- [AAIO-ydinspesifikaatio](aaio-core-v0.1.md) — Agentic AI Optimization Core
- [ACP-integrointispesifikaatio](acp-integration-v0.1.md) — Agent Commerce Protocol
- [UCP-integrointispesifikaatio](ucp-integration-v0.1.md) — Universal Commerce Protocol
- [AAIO-tuoteskeema](../../schemas/aaio-product.schema.json) — Tuotadataskeema
- [AAIO-palveluskeema](../../schemas/aaio-service.schema.json) — Palveludataskeema

### Informatiiviset viitteet

- [A2A GitHub-repositorio](https://github.com/a2aproject/A2A) — Referenssitoteutukset ja esimerkit
- [Schema.org Product](https://schema.org/Product) — Schema.org-tuotetyyppi
- [ISO 3166-1](https://www.iso.org/iso-3166-country-codes.html) — Maakoodit
- [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) — Valuuttakoodit

---

*Copyright 2026 Tekoäly-Dani. Lisensoitu Apache 2.0 -lisenssillä.*
