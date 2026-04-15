# Muutosloki

Kaikki merkittävät muutokset AAIO Standard Draftiin dokumentoidaan tähän tiedostoon.

Muoto perustuu [Keep a Changelog](https://keepachangelog.com/en/1.1.0/) -käytäntöön.

> 🇬🇧 [English version](../CHANGELOG.md)

## [Julkaisematon]

### Lisätty
- Repositorion rakenne: `specs/`-, `schemas/`-, `examples/`-, `docs/`-hakemistot
- Apache 2.0 -lisenssi
- Osallistumisohjeet (`CONTRIBUTING.md`)
- Tämä muutosloki
- **AIO Framework** (`specs/aio-framework-v0.1.md`) — sateenvarjoviitekehys, joka yhdistää kaikki AI-optimointikerrokset
- **SEO Foundations** (`specs/seo-foundations-v0.1.md`) — SEO-vaatimukset AI-optimoinnin perustana
- **AEO Guidelines** (`specs/aeo-guidelines-v0.1.md`) — vastausmoottorioptimoinnin parhaat käytännöt
- **GEO Guidelines** (`specs/geo-guidelines-v0.1.md`) — generatiivisten moottoreiden optimointiohjeistus
- **AAIO Core Specification** (`specs/aaio-core-v0.1.md`) — agenttivalmiuden ydinvaatimukset ja pisteytys
- **AXO Framework** (`specs/axo-framework-v0.1.md`) — agenttikokemusoptimointiviitekehys (UX-näkökulma)
- **ACP Integration** (`specs/acp-integration-v0.1.md`) — Agent Commerce Protocol -integrointi
- **UCP Integration** (`specs/ucp-integration-v0.1.md`) — Universal Commerce Protocol -integrointi
- **A2A Commerce** (`specs/a2a-commerce-v0.1.md`) — agentti-agentti-neuvotteluprotokollan profiili
- JSON-skeemat: `aaio-manifest`, `aaio-product`, `aaio-service`, `aaio-scoring`
- Termistösanasto (`docs/terminology.md`)
- Protokollalandscape-yleiskatsaus (`docs/protocol-landscape.md`)
- Käyttöönotto-opas (`docs/implementation-roadmap.md`)
- Suomenkieliset käännökset kaikista dokumenteista (`fi/`-hakemisto)

### Korjattu
- Skeemakentän nimen johdonmukaisuus: `aaioVersion` (camelCase) käytössä kaikkialla
- Valuuttakoodit noudattavat ISO 4217 -isot kirjaimet -muotoa (`EUR`, ei `eur`)
- ACP-otsakkeiden nimet yhtenäistetty spesifikaatioiden ja tiekartan välillä
- Skeeman `$id`-verkkotunnukset yhtenäistetty osoitteeseen `aaio-standard.org`
- Palveluskeeman `billing_period`-null-käsittely korjattu
