# Esimerkki: Palveluntarjoaja (AAIO-taso 2)

> 🇬🇧 [English version](../../../examples/service-provider/README.md)

Tämä esimerkki näyttää täydellisen AAIO-tason 2 toteutuksen **ammatillisia palveluita tarjoavalle yritykselle** — konsultille, toimistolle tai erikoistuneelle yritykselle, joka haluaa AI-agenttien löytävän ja ymmärtävän palvelunsa.

**Yritystyyppi:** AI-optimointikonsultointiyritys  
**AAIO-tavoitetaso:** Taso 2 (Luettava)  
**Arvioitu toteutusaika:** 1–2 päivää

---

## Mitä tämä esimerkki sisältää

| Tiedosto | Kuvaus |
|----------|--------|
| `aaio-manifest.json` | Sivustotason AAIO-manifesti (sijoita osoitteeseen `yourdomain.com/.well-known/aaio-manifest.json`) |
| `AGENTS.md` | Agenttiohjetiedosto (sijoita osoitteeseen `yourdomain.com/AGENTS.md`) |
| `llms.txt` | LLM-luettava sivustoyhteenveto (sijoita osoitteeseen `yourdomain.com/llms.txt`) |
| `ai.txt` | AI-käytäntöilmoitus (sijoita osoitteeseen `yourdomain.com/ai.txt`) |
| `service.json` | UCP-yhteensopiva palvelulistausesimerkki |

---

## AAIO-tason 2 vaatimukset

Tason 2 (Luettava) saavuttamiseksi palveluntarjoaja tarvitsee:

1. **Taso 1 (Löydettävä):** `AGENTS.md`, `robots.txt`-direktiivit, `llms.txt`
2. **Tason 2 lisäykset:** Jäsennetty palveludata (UCP-yhteensopiva), MCP-palvelin tai jäsennetty API, `aaio-manifest.json`

Tämä esimerkki kattaa molemmat tasot yhdessä toteutuspaketissa.

---

## Mukauttaminen omalle yrityksellesi

Korvaa kaikki paikkamerkkiarvot:

- `yourdomain.com` → oma verkkotunnuksesi
- `Your Company Name` → yrityksesi nimi
- Palvelunimet, kuvaukset, hinnoittelu → omat palvelusi

Katso täydellinen [Toteutussuunnitelma](../../docs/implementation-roadmap.md) vaiheittaiseen oppaaseen.
