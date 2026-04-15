# Universal Commerce Protocol (UCP) -integrointispesifikaatio

**Versio:** 0.1-luonnos  
**Status:** Luonnos  
**Päivämäärä:** 2026-04-09  
**Tekijät:** Tekoäly-Dani AAIO-työryhmä  

> 🇬🇧 [English version](../../specs/ucp-integration-v0.1.md)

---

## Tiivistelmä

Tämä dokumentti määrittelee, miten Agentic AI Optimization (AAIO) -yhteensopivat verkkosivustot toteuttavat Universal Commerce Protocol (UCP) -protokollan paljastaakseen tuote- ja palveludatan standardoidussa, koneluettavassa muodossa. UCP, joka on lähtöisin Google/Shopify-kaupankäynti-infrastruktuurista, tarjoaa yhtenäisen datakerroksen, jota AI-agentit voivat käyttää löytämiseen, vertailuun ja ostopäätöksiin.

Tämä spesifikaatio ei määrittele uutta protokollaa. Se profiloi olemassa olevan UCP-kehyksen AAIO-optimointikerroksen sisällä, määrittäen miten kaupankäyntialustat rakentavat ja tarjoilevat tuote-/palveludata niin, että autonomiset agentit voivat tehokkaasti jäsentää, vertailla ja toimia katalogitiedon perusteella.

---

## 1. Termistö

| Termi | Määritelmä |
|-------|-----------|
| **UCP** | Universal Commerce Protocol — standardoitu tiedonvaihtomuoto tuote- ja palvelutiedoille kaupankäyntialustojen välillä (Google/Shopify-ekosysteemi) |
| **AAIO** | Agentic AI Optimization — optimointikerros, joka varmistaa, että verkkosivustot ovat löydettäviä, ymmärrettäviä ja asiointikelpoisia autonomisille AI-agenteille |
| **Katalogiagi** | AI-agentti, joka ryömii, indeksoi ja vertailee tuote-/palvelutarjoamia useista UCP-yhteensopivista lähteistä |
| **Kauppiassyöte** | Jäsennetty datavienti kauppiaan katalogista UCP-muodossa |
| **Tuoteen entiteetti** | Normalisoitu tuoterepresentaatio AAIO-tuoteskeeman mukaisesti |
| **Palvelun entiteetti** | Normalisoitu palvelurepresentaatio AAIO-palveluskeeman mukaisesti |
| **Skeemakuvaus** | Määritelty muunnos alustakohtaisesta datamuodosta (Shopify, WooCommerce jne.) AAIO-kanoniseen skeemaan |

---

## 2. Yleiskatsaus

### 2.1 Ongelmanasettelu

AI-agentit, jotka vertailevat tuotteita useiden toimittajien välillä, kohtaavat pirstaloitumisongelman: jokainen verkkokauppa-alusta käyttää omaa datamalliaan, attribuuttien nimeämiskäytäntöjään ja rajapintarakennettaan. Agentti, joka arvioi kannettavaa tietokonetta, joutuu normalisoimaan "RAM", "Memory", "memory_gb" ja "ram_size" eri lähteistä. UCP-integraatio AAIO:n puitteissa ratkaisee tämän edellyttämällä kanonista datamuotoa.

### 2.2 Arkkitehtuuri

```
┌─────────────────┐     ┌───────────────────┐     ┌──────────────────┐
│Kaupankäyntialusta│     │  UCP-muunnoskerros│     │  AAIO-päätepiste │
│ (Shopify, jne.)  │────>│  Skeemakuvaus     │────>│  /ucp/v0.1/      │
│  Natiivi data    │     │                   │     │  Kanoninen data  │
└─────────────────┘     └───────────────────┘     └──────┬───────────┘
                                                         │
                                                         ▼
                                                  ┌──────────────┐
                                                  │ Katalogiagi  │
                                                  │ (AI-agentti) │
                                                  └──────────────┘
```

### 2.3 Suhde AAIO:on

UCP on AAIO-protokollapinon datakerros:

- **UCP** (tämä dokumentti) — Standardoitu tuote-/palveludata
- **ACP** — Maksun suoritus Stripen kautta
- **A2A** — Agentti-agentti-neuvottelu

UCP tarjoaa datan, jota agentit kuluttavat ennen ACP-transaktioiden tai A2A-neuvotteluiden käynnistämistä.

---

## 3. Datamalli

### 3.1 Tuoteen entiteetti

Tuotteiden TÄYTYY noudattaa `aaio-product.schema.json`-skeemaa. Kanoninen tuoterepresentaatio sisältää:

```json
{
  "aaio_schema": "aaio-product/v0.1",
  "id": "prod_widget_pro_2026",
  "gtin": "0614141000036",
  "name": "Widget Pro 2026",
  "description": "Ammattilaistason widget AI-integraatiolla",
  "category": {
    "primary": "elektroniikka/widgetit",
    "google_product_category": 1234
  },
  "brand": {
    "name": "WidgetCorp",
    "url": "https://widgetcorp.example.com"
  },
  "pricing": {
    "currency": "EUR",
    "amount": 4999,
    "amount_decimal": "49.99",
    "tax_included": true
  },
  "availability": {
    "status": "in_stock",
    "quantity": 342,
    "lead_time_days": 1
  },
  "attributes": {
    "weight_g": 250,
    "dimensions_mm": {"length": 150, "width": 80, "height": 20},
    "color": "midnight_blue",
    "material": "alumiini"
  },
  "agent_metadata": {
    "comparison_attributes": ["weight_g", "dimensions_mm", "color"],
    "decision_factors": ["pricing.amount", "availability.status", "attributes.material"],
    "alternatives": ["prod_widget_standard_2026", "prod_widget_lite_2026"]
  }
}
```

### 3.2 Palvelun entiteetti

Palveluiden TÄYTYY noudattaa `aaio-service.schema.json`-skeemaa:

```json
{
  "aaio_schema": "aaio-service/v0.1",
  "id": "svc_aaio_audit",
  "name": "AAIO-valmiusaudit",
  "description": "Kattava audit verkkosivuston valmiudesta autonomisille AI-agenteille",
  "category": {
    "primary": "konsultointi/ai-optimointi"
  },
  "provider": {
    "name": "Tekoäly-Dani",
    "url": "https://tekoalydani.com"
  },
  "pricing": {
    "model": "fixed",
    "currency": "EUR",
    "amount": 99000,
    "amount_decimal": "990.00",
    "billing_period": null
  },
  "delivery": {
    "model": "project",
    "estimated_duration_days": 5,
    "regions": ["FI", "SE", "NO", "DK", "EE"],
    "remote_available": true
  },
  "availability": {
    "status": "available",
    "next_available_date": "2026-04-15",
    "booking_url": "/acp/v0.1/transactions"
  }
}
```

### 3.3 Yhteiset kentät

Kaikki UCP-entiteetit jakavat nämä peruskentät:

| Kenttä | Tyyppi | Pakollisuus | Kuvaus |
|--------|--------|-------------|--------|
| `aaio_schema` | Merkkijono | VAADITTU | Skeeman tunniste ja versio (esim. `"aaio-product/v0.1"`). |
| `id` | Merkkijono | VAADITTU | Kauppiaalle uniikki vakaa tunniste. |
| `name` | Merkkijono | VAADITTU | Ihmisille ja agenteille luettava nimi. |
| `description` | Merkkijono | VAADITTU | Pelkkä teksti -kuvaus (ei HTML:ää). |
| `category` | Objekti | VAADITTU | Kategorisointi `primary`-kentällä. |
| `pricing` | Objekti | VAADITTU | Hintatiedot. |
| `availability` | Objekti | VAADITTU | Nykyinen saatavuusstatus. |
| `agent_metadata` | Objekti | SUOSITELTU | Agentin päätöksentekoa optimoivat vihjeet. |

---

## 4. Rajapintaspesifikaatio

### 4.1 Päätepisteet

UCP-dataa tarjoillaan RESTful-rajapinnan kautta:

| Päätepiste | Metodi | Kuvaus |
|------------|--------|--------|
| `/ucp/v0.1/products` | GET | Listaa tuotteet sivutuksella ja suodatuksella. |
| `/ucp/v0.1/products/{id}` | GET | Hae yksittäinen tuote ID:llä. |
| `/ucp/v0.1/services` | GET | Listaa palvelut sivutuksella ja suodatuksella. |
| `/ucp/v0.1/services/{id}` | GET | Hae yksittäinen palvelu ID:llä. |
| `/ucp/v0.1/categories` | GET | Listaa saatavilla olevat kategoriat. |
| `/ucp/v0.1/search` | GET | Koko tekstin haku tuotteista ja palveluista. |
| `/ucp/v0.1/feed` | GET | Massavienti NDJSON-muodossa. |

### 4.2 Kyselyparametrit

| Parametri | Tyyppi | Kuvaus |
|-----------|--------|--------|
| `page` | Kokonaisluku | Sivunumero (1-indeksoitu). Oletus: 1. |
| `per_page` | Kokonaisluku | Kohteet sivua kohden. Oletus: 50. Maks: 200. |
| `category` | Merkkijono | Suodata ensisijaisen kategoriapolun mukaan. |
| `min_price` | Kokonaisluku | Minimihinta pienimmässä valuuttayksikössä. |
| `max_price` | Kokonaisluku | Maksimihinta pienimmässä valuuttayksikössä. |
| `currency` | Merkkijono | ISO 4217 -valuuttakoodi. |
| `availability` | Enum | `in_stock`, `preorder`, `backorder`, `out_of_stock`. |
| `sort` | Merkkijono | Lajittelukenttä. Vaihtoehdot: `price`, `name`, `updated_at`, `relevance`. |
| `q` | Merkkijono | Hakukysely (`/search`-päätepiste). |
| `updated_since` | ISO 8601 | Palauta tämän ajanhetken jälkeen muokatut kohteet. |

### 4.3 Sivutus

Kaikki listausvastauksissa TÄYTYY sisältää sivutusmetatiedot:

```json
{
  "data": [...],
  "pagination": {
    "page": 1,
    "per_page": 50,
    "total_items": 1523,
    "total_pages": 31,
    "next_cursor": "cursor_abc123"
  }
}
```

---

## 5. Skeemakuvaukset

### 5.1 Shopify-kuvaus

| Shopify-kenttä | UCP/AAIO-kenttä |
|----------------|----------------|
| `product.id` | `id` (etuliitteellä `shopify_`) |
| `product.title` | `name` |
| `product.body_html` | `description` (puhdistettu HTML:stä) |
| `product.product_type` | `category.primary` |
| `variant.price` | `pricing.amount_decimal` |
| `variant.sku` | `attributes.sku` |
| `variant.inventory_quantity` | `availability.quantity` |
| `variant.available` | `availability.status` (kartoitettu) |

### 5.2 Google Merchant Center -kuvaus

| Google MC -kenttä | UCP/AAIO-kenttä |
|-------------------|----------------|
| `offerId` | `id` |
| `title` | `name` |
| `description` | `description` |
| `googleProductCategory` | `category.google_product_category` |
| `brand` | `brand.name` |
| `price.value` | `pricing.amount_decimal` |
| `price.currency` | `pricing.currency` |
| `gtin` | `gtin` |
| `availability` | `availability.status` (kartoitettu) |

---

## 6. AAIO-integrointivaatimukset

### 6.1 Löydettävyys

AAIO-yhteensopivien kauppiaiden TÄYTYY mainostaa UCP-tukea AAIO-manifestissaan:

```json
{
  "aaioVersion": "0.1",
  "protocols": {
    "ucp": {
      "version": "0.1",
      "catalog_endpoint": "/ucp/v0.1/products",
      "service_endpoint": "/ucp/v0.1/services",
      "feed_endpoint": "/ucp/v0.1/feed",
      "search_endpoint": "/ucp/v0.1/search",
      "total_products": 1523,
      "total_services": 12,
      "supported_currencies": ["EUR", "USD"],
      "default_locale": "fi-FI",
      "update_frequency": "hourly"
    }
  }
}
```

### 6.2 Skeemavaatimustenmukaisuus

Kaikkien UCP-päätepisteiden palauttamien tuoteen entiteettien TÄYTYY validoitua `aaio-product.schema.json`-skeemaa vastaan. Kaikkien palvelun entiteettien TÄYTYY validoitua `aaio-service.schema.json`-skeemaa vastaan.

Kauppiaiden PITÄISI sisällyttää `agent_metadata`-osio agentin päätöksenteon optimoimiseksi.

### 6.3 Tuoreus

- UCP-päätepisteiden TÄYTYY palauttaa dataa, joka on enintään 1 tunnin vanhaa.
- Hinnoittelu- ja saatavuusmuutosten TÄYTYY heijastua 15 minuutin kuluessa.
- `updated_since`-parametrin TÄYTYY olla tuettu inkrementaaliseen synkronointiin.

### 6.4 Poikkiprotokolla-viittaukset

UCP-entiteettien, jotka ovat ostettavissa ACP:n kautta, PITÄISI sisältää viittaus ACP-transaktiopäätepisteeseen:

```json
{
  "id": "prod_widget_pro_2026",
  "acp_reference": {
    "endpoint": "/acp/v0.1/transactions",
    "purchasable": true,
    "requires_quote": false
  }
}
```

---

## 7. Virheenkäsittely

### 7.1 Virhevastauksen muoto

```json
{
  "error": {
    "code": "UCP_ITEM_NOT_FOUND",
    "message": "Tuotetta ID:llä 'prod_nonexistent' ei löydy",
    "details": {
      "requested_id": "prod_nonexistent",
      "suggestion": "Käytä /ucp/v0.1/search?q=widget löytääksesi samankaltaisia tuotteita"
    }
  }
}
```

### 7.2 Virhekoodit

| Koodi | HTTP-status | Kuvaus |
|-------|-------------|--------|
| `UCP_INVALID_PARAMETER` | 400 | Virheellinen kyselyparametrin arvo. |
| `UCP_UNAUTHORIZED` | 401 | Tunnistautuminen vaaditaan tai token virheellinen. |
| `UCP_RATE_LIMITED` | 429 | Agentti on ylittänyt pyyntönopeusrajat. |
| `UCP_ITEM_NOT_FOUND` | 404 | Pyydettyä tuotetta tai palvelua ei löydy. |
| `UCP_FEED_UNAVAILABLE` | 503 | Massasyöte tilapäisesti poissa käytöstä. |
| `UCP_SCHEMA_ERROR` | 500 | Sisäinen skeemakuvauksen virhe. |

---

## 8. Turvallisuusnäkökohdat

### 8.1 Tunnistautuminen

UCP-päätepisteet VOIVAT olla julkisesti saatavilla tuotteiden löytämistä varten. Kuitenkin:

- Massasyötteiden päätepisteiden (`/ucp/v0.1/feed`) PITÄISI vaatia tunnistautuminen kaappaamisväärinkäytösten estämiseksi.
- Nopeusrajoitukset TÄYTYY soveltaa agentin tunnisteen tai IP-osoitteen mukaan.
- SUOSITELLUT nopeusrajoitukset: 1000 pyyntöä/tunti katalogipäätepisteille, 10 pyyntöä/tunti massasyötteille.

### 8.2 Tietosuoja

- UCP-vastaukset EI SAA sisältää henkilökohtaisesti tunnistettavaa tietoa (PII).
- Hintatiedot VOIVAT olla personoituja (esim. B2B-hinnoittelu), mutta vain tunnistautuneille agenteille.

### 8.3 Liiketoiminnan luottamuksellisuus

Kauppiaiden PITÄISI huomioida, että UCP-data on suunniteltu agenttien kulutettavaksi ja voidaan koota kilpailijoiden yli. Arkaluontoista kilpailullista dataa (kustannushinnat, toimittajatiedot) EI SALLITA sisällyttää UCP-vastauksiin.

---

## 9. Vaatimustenmukaisuus

Toteutus on tämän spesifikaation mukainen, jos se:

1. Tarjoilee tuoteen dataa `aaio-product.schema.json`-skeeman mukaisesti (luku 3.1).
2. Tarjoilee palvelun dataa `aaio-service.schema.json`-skeeman mukaisesti (luku 3.2).
3. Toteuttaa vähintään lista- ja haku-päätepisteet (luku 4.1).
4. Tukee sivutusta (luku 4.3).
5. Mainostaa UCP-tukea AAIO-manifestissa (luku 6.1).
6. Täyttää tuoreusvaatimukset (luku 6.3).
7. Toteuttaa luvussa 7.2 määritellyt virhekoodit.
8. Täyttää luvun 8 turvallisuusvaatimukset.

---

## 10. Viitteet

### Normatiiviset viitteet

- [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) — Avainsanat RFC-dokumentteja varten
- [RFC 8259](https://www.rfc-editor.org/rfc/rfc8259) — JSON-tiedonvaihtomuoto
- [JSON Schema](https://json-schema.org/specification) — JSON-skeemaspesifikaatio
- [Google Merchant Center](https://developers.google.com/shopping-content/reference/rest) — Kauppasisältörajapinta
- [AAIO Core Specification](aaio-core-v0.1.md) — Agentic AI Optimization -ydinstandardi

### Informatiiviset viitteet

- [ACP Integration Specification](acp-integration-v0.1.md) — Agent Commerce Protocol
- [A2A Commerce Protocol Profile](a2a-commerce-v0.1.md) — Agentti-agentti-kaupankäynti

---

*Tekijänoikeus 2026 Tekoäly-Dani. Lisenssoitu Apache 2.0:lla.*
