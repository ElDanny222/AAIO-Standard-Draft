# AAIO Standard Draft

![Status](https://img.shields.io/badge/status-draft-yellow)
![Version](https://img.shields.io/badge/version-0.1-blue)
![License](https://img.shields.io/badge/license-Apache%202.0-green)

**Agentic AI Optimization (AAIO)** — open technical specifications for making websites discoverable, readable, and transactable by autonomous AI agents.

Drafted and maintained by [Tekoäly-Dani](https://tekoalydani.com) as a local implementation reference and standard draft for the Finnish market — published openly so other implementers can build on the same baseline.

The framework's academic anchor is **Floridi et al., *Minds & Machines*, Springer Nature 2026** (DOI: [10.1007/s11023-026-09779-8](https://doi.org/10.1007/s11023-026-09779-8)) — a peer-reviewed article that defines the Agentic AI Optimization concept and its GELSI lens (Governance, Ethics, Legal, Social Implications). This repository is the practitioner-side draft that operationalizes that frame; the academic source is what enterprise procurement can ground decisions on.

---

## What is AAIO?

AAIO is not a new protocol. It is an **optimization layer** that defines how organizations implement existing agent protocols — MCP, ACP, UCP, A2A — so that autonomous AI agents can:

1. **Discover** the business and its services
2. **Understand** structured product and service data
3. **Transact** without human intervention

AAIO sits above SEO, AEO, and GEO. It addresses the emerging reality where AI agents — not humans — are the primary buyers, researchers, and decision-makers.

```
Human search (SEO) → AI answer engines (AEO/GEO) → Autonomous agents (AAIO)
```

---

## Repository Structure

```
AAIO-Standard-Draft/
├── README.md                        # This file
├── CONTRIBUTING.md                  # How to contribute
├── GOVERNANCE.md                    # Maintainer roles, decision process, release cadence
├── LICENSE                          # Apache 2.0
│
├── specs/                           # Technical specifications
│   ├── aio-framework-v0.1.md        # AIO Umbrella Framework
│   ├── seo-foundations-v0.1.md      # SEO Foundations for AAIO
│   ├── aeo-guidelines-v0.1.md       # AEO Best Practices
│   ├── geo-guidelines-v0.1.md       # GEO Guidelines
│   ├── aaio-core-v0.1.md            # AAIO Core Specification
│   ├── axo-framework-v0.1.md        # AXO Framework (UX perspective)
│   ├── acp-integration-v0.1.md      # ACP Integration Guide
│   ├── ucp-integration-v0.1.md      # UCP Integration Guide
│   └── a2a-commerce-v0.1.md         # A2A Commerce Protocol Profile
│
├── schemas/                         # Machine-readable schema definitions
│   ├── aaio-manifest.schema.json    # Site-level AAIO manifest
│   ├── aaio-product.schema.json     # Agent-optimized product data
│   ├── aaio-service.schema.json     # Agent-optimized service data
│   └── aaio-scoring.schema.json     # AAIO Readiness Score
│
├── examples/                        # Reference implementations
│   ├── ecommerce/
│   ├── service-provider/
│   └── saas-platform/
│
└── docs/                            # Supporting documentation
    ├── protocol-landscape.md        # How MCP, ACP, UCP, A2A relate to AAIO
    ├── implementation-roadmap.md    # Step-by-step implementation guide
    └── terminology.md               # Glossary
```

---

## Specifications

### AIO Stack (Cumulative Layers)

| Layer | Document | Status | Description |
|-------|----------|--------|-------------|
| Framework | [AIO Framework v0.1](specs/aio-framework-v0.1.md) | Draft | Umbrella framework unifying all AI optimization layers |
| L1 | [SEO Foundations v0.1](specs/seo-foundations-v0.1.md) | Draft | SEO requirements that underpin all AI optimization |
| L2 | [AEO Guidelines v0.1](specs/aeo-guidelines-v0.1.md) | Draft | Answer Engine Optimization best practices |
| L3 | [GEO Guidelines v0.1](specs/geo-guidelines-v0.1.md) | Draft | Generative Engine Optimization guidelines |
| L4 | [AAIO Core v0.1](specs/aaio-core-v0.1.md) | Draft | Core optimization requirements and agent-readiness criteria |
| L4 (UX) | [AXO Framework v0.1](specs/axo-framework-v0.1.md) | Draft | Agent Experience Optimization framework |

### Protocol Integration Specs

| Document | Status | Description |
|----------|--------|-------------|
| [ACP Integration v0.1](specs/acp-integration-v0.1.md) | Draft | Agent Commerce Protocol integration guide |
| [UCP Integration v0.1](specs/ucp-integration-v0.1.md) | Draft | Universal Commerce Protocol integration guide |
| [A2A Commerce v0.1](specs/a2a-commerce-v0.1.md) | Draft | Agent-to-Agent negotiation protocol profile |

---

## Quick Start

**Are you an executive or strategist?**

Start with the [AIO Framework](specs/aio-framework-v0.1.md) for the big picture — it explains the cumulative layer model and maturity path from SEO to full AAIO.

**Are you an organization that wants to become agent-ready?**

Start with the [SEO Foundations](specs/seo-foundations-v0.1.md) checklist, then follow the [Implementation Roadmap](docs/implementation-roadmap.md) for a phase-by-phase path to full AAIO compliance.

**Are you a developer building agent-facing infrastructure?**

Read the [AAIO Core Specification](specs/aaio-core-v0.1.md) and the [Protocol Landscape](docs/protocol-landscape.md) first.

**Are you a content strategist or marketer?**

The [AEO Guidelines](specs/aeo-guidelines-v0.1.md) and [GEO Guidelines](specs/geo-guidelines-v0.1.md) cover how to optimize content for AI answer engines and generative AI inclusion.

**Are you an AI researcher or journalist?**

The [Terminology glossary](docs/terminology.md) defines all terms precisely. The [Protocol Landscape](docs/protocol-landscape.md) situates AAIO relative to MCP, ACP, UCP, and A2A.

---

## Terminology

| Term | Full Name | Role in AAIO |
|------|-----------|--------------|
| **AIO** | AI Optimization | Umbrella term covering all AI optimization layers |
| **AEO** | Answer Engine Optimization | Getting cited in AI answer engines (ChatGPT, Perplexity) |
| **GEO** | Generative Engine Optimization | Appearing in AI-generated synthesized answers |
| **AAIO** | Agentic AI Optimization | Enabling autonomous agents to discover, understand, and transact |
| **AXO** | Agent Experience Optimization | UX/CX perspective on AAIO — how agents experience a site |
| **MCP** | Model Context Protocol | Anthropic's protocol for connecting AI models to tools and data |
| **ACP** | Agent Commerce Protocol | Machine-to-machine payment transactions (Stripe & OpenAI, Apache 2.0) |
| **UCP** | Universal Commerce Protocol | Unified service data standard for AI agents |
| **A2A** | Agent-to-Agent | Agent negotiation protocol (Google, now Linux Foundation) |

---

## Status

This repository is in **active draft** status. All specifications are v0.1 and subject to change. Feedback and contributions are welcome — see [CONTRIBUTING.md](CONTRIBUTING.md). Maintainer roles, decision process, and release cadence are documented in [GOVERNANCE.md](GOVERNANCE.md).

These specifications are developed based on real-world AAIO implementation work at [tekoalydani.com](https://tekoalydani.com) and are designed to be vendor-neutral and openly extensible. The conceptual frame is anchored in Floridi et al., *Minds & Machines*, Springer Nature 2026 (DOI: [10.1007/s11023-026-09779-8](https://doi.org/10.1007/s11023-026-09779-8)); the work in this repository is the local, practitioner-driven draft on top of that frame, not a separate or competing definition of AAIO.

---

## Suomeksi / In Finnish

Tämä repository sisältää avoimet tekniset spesifikaatiot **Agentic AI Optimization (AAIO)** -standardille — paikallisena toteutuksena ja standardiluonnoksena, jonka [Tekoäly-Dani](https://tekoalydani.com) on kirjoittanut Suomen markkinatarpeeseen ja julkaissut avoimena, jotta muut toteuttajat voivat käyttää samaa pohjaa.

**AAIO tarkoittaa:** Optimointikerros, joka määrittelee miten organisaatiot implementoivat agenttityökalut (MCP, ACP, UCP, A2A) niin, että autonomiset AI-agentit löytävät, ymmärtävät ja voivat asioida niiden kanssa ilman ihmisvälikättä.

**Akateeminen ankkuri:** Floridi et al., *Minds & Machines*, Springer Nature 2026 (DOI: [10.1007/s11023-026-09779-8](https://doi.org/10.1007/s11023-026-09779-8)) — vertaisarvioitu artikkeli, joka täsmentää AAIO-käsitteen ja sen GELSI-näkökulman (Governance, Ethics, Legal, Social Implications). Tämä repository on käytännön toteuttajan luonnos kyseisen kehyksen päälle, ei erillinen tai kilpaileva määritelmä AAIO:sta.

**[Kaikki spesifikaatiot suomeksi: fi/README.md](fi/README.md)**

Käytännön käyttöönotto-opas: [fi/docs/implementation-roadmap.md](fi/docs/implementation-roadmap.md)  
Protokollakartta: [fi/docs/protocol-landscape.md](fi/docs/protocol-landscape.md)  
Termistö: [fi/docs/terminology.md](fi/docs/terminology.md)

---

## Author

[Tekoäly-Dani](https://tekoalydani.com)  
[dani@tekoalydani.com](mailto:dani@tekoalydani.com)

---

## License

Apache 2.0 — see [LICENSE](LICENSE)
