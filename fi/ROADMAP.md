# AAIO Standard Draft — Tiekartta

> **Status:** Draft v0.1 | Ylläpitäjä: [Tekoäly-Dani](https://tekoalydani.com)

> 🇬🇧 [English version](../ROADMAP.md)

Tämä dokumentti kuvaa AAIO Standard -spesifikaatioiden suunnitellun kehityspolun. Kohteet voivat muuttua protokollaekosysteemin kehityksen ja yhteisöpalautteen perusteella.

---

## Nykytila: v0.1 (huhtikuu 2026)

v0.1-julkaisu luo AAIO-spesifikaatioiden perustan:

- ✅ AIO Framework (sateenvarjoviitekehys)
- ✅ SEO-, AEO-, GEO-spesifikaatiot
- ✅ AAIO-ydinspesifikaatio
- ✅ AXO-viitekehys
- ✅ Protokollaintegrointiopaat (MCP, ACP, UCP, A2A)
- ✅ JSON-skeemat (manifesti, tuote, palvelu, pisteytys)
- ✅ Käyttöönotto-opas ja termistö
- 🔄 Viiteimplementaatiot (työn alla)

---

## v0.2 — Viiteimplementaatiot (Q2 2026)

**Teema:** Näytä, älä vain kerro.

- [ ] Viimeistele `examples/service-provider/` — ammatillisia palveluita tarjoava yritys (konsultti, toimisto)
- [ ] Viimeistele `examples/ecommerce/` — tuotteita myyvä yritys
- [ ] Viimeistele `examples/saas-platform/` — SaaS-tuote
- [ ] Validointityökalu: CLI-työkalu URL-osoitteen tarkistamiseksi AAIO-vaatimuksia vastaan
- [ ] `ai.txt` -muodollinen spesifikaatioyhteensovitus (standardin kypsyessä)

---

## v0.3 — Ekosysteemipäivitykset (Q3 2026)

**Teema:** Seuraa protokollaekosysteemiä.

- [ ] MCP-palvelimen implementointiopas (päivitetty uusimpaan MCP-spesifikaatioon)
- [ ] A2A v1.0 -yhteensovitus (jos spesifikaatio vakiintuu)
- [ ] ACP-kauppiaan käyttöönoton opas
- [ ] AAIO Readiness Score -laskuri (verkkotyökalu)

---

## v1.0 — Vakaa spesifikaatio (tavoite: Q4 2026)

**Teema:** Tuotantovalmis standardi.

- [ ] Yhteisöarviointijakso (30 päivää)
- [ ] Kaikki spesifikaatiot siirretty `draft`-tilasta `stable`-tilaan
- [ ] Versioskeema (`aaio-manifest`) lukittu taaksepäin yhteensopivuuden takaamiseksi
- [ ] Vähintään 3 tosielämän tapaustutkimusta elävistä implementaatioista

---

## Mikä ei kuulu laajuuteen

- AAIO ei ole itsessään protokolla — emme määrittele uutta protokollaa
- AAIO ei korvaa SEO:ta, AEO:ta, GEO:ta eikä mitään olemassa olevaa protokollaa
- Emme ylläpidä implementaatioita — vain spesifikaatioita ja viiteesimerkkejä

---

## Osallistuminen

Onko sinulla palautetta tiekartasta? Avaa [GitHub Discussion](../../discussions) tai tee issue. Katso [CONTRIBUTING.md](CONTRIBUTING.md) ohjeistusta varten.

---

## Versiointikäytäntö

Kaikki spesifikaatiot noudattavat **semanttista versiointia** `specs/`-hakemistossa:

- **Patch** (0.1.x): Selvennykset, kirjoitusvirhekorjaukset, ei-normatiiviset lisäykset
- **Minor** (0.x.0): Uudet normatiiviset vaatimukset, laajennettu laajuus, uudet protokollaintegroinnit
- **Major** (x.0.0): Rikkovat muutokset pakollisiin kenttiin, pisteytystmalliin tai skeemarakenteeseen

Repositorion versio (tiedostossa `CHANGELOG.md`) seuraa koko kokoelmaa, ei yksittäisiä spesifikaatioita.
