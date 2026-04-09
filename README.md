# AAIO Standard Draft

![Status](https://img.shields.io/badge/status-draft-yellow)
![Version](https://img.shields.io/badge/version-0.1-blue)
![License](https://img.shields.io/badge/license-Apache%202.0-green)

**Agentic AI Optimization (AAIO)** — open technical specifications for making websites discoverable, readable, and transactable by autonomous AI agents.

Maintained by **Dani Forsberg** / [RAD Intelligence](https://tekoalydani.com)

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
├── LICENSE                          # Apache 2.0
│
├── specs/                           # Technical specifications
│   ├── aaio-core-v0.1.md            # AAIO Core Specification
│   ├── aeo-guidelines-v0.1.md       # AEO Best Practices
│   ├── acp-integration-v0.1.md      # ACP Integration Guide
│   ├── ucp-integration-v0.1.md      # UCP Integration Guide
│   ├── a2a-commerce-v0.1.md         # A2A Commerce Protocol Profile
│   └── axo-framework-v0.1.md        # AXO Framework (UX perspective)
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

| Document | Status | Description |
|----------|--------|-------------|
| [AAIO Core v0.1](specs/aaio-core-v0.1.md) | Draft | Core optimization requirements and agent-readiness criteria |
| [AEO Guidelines v0.1](specs/aeo-guidelines-v0.1.md) | Draft | Answer Engine Optimization best practices |
| [ACP Integration v0.1](specs/acp-integration-v0.1.md) | Draft | Agent Commerce Protocol integration guide |
| [UCP Integration v0.1](specs/ucp-integration-v0.1.md) | Draft | Universal Commerce Protocol integration guide |
| [A2A Commerce v0.1](specs/a2a-commerce-v0.1.md) | Draft | Agent-to-Agent negotiation protocol profile |
| [AXO Framework v0.1](specs/axo-framework-v0.1.md) | Draft | Agent Experience Optimization framework |

---

## Quick Start

**Are you an organization that wants to become agent-ready?**

Start with the [Implementation Roadmap](docs/implementation-roadmap.md). It walks through a practical, phase-by-phase path from zero to full AAIO compliance.

**Are you a developer building agent-facing infrastructure?**

Read the [AAIO Core Specification](specs/aaio-core-v0.1.md) and the [Protocol Landscape](docs/protocol-landscape.md) first.

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
| **ACP** | Agent Commerce Protocol | Machine-to-machine payment and transaction headers |
| **UCP** | Universal Commerce Protocol | Unified service data standard for AI agents |
| **A2A** | Agent-to-Agent | Negotiation protocols between buyer and seller agents |

---

## Status

This repository is in **active draft** status. All specifications are v0.1 and subject to change. Feedback and contributions are welcome — see [CONTRIBUTING.md](CONTRIBUTING.md).

These specifications are developed based on real-world AAIO implementation work at [tekoalydani.com](https://tekoalydani.com) and are designed to be vendor-neutral and openly extensible.

---

## Suomeksi / In Finnish

Tämä repository sisältää avoimet tekniset spesifikaatiot **Agentic AI Optimization (AAIO)** -standardille.

**AAIO tarkoittaa:** Optimointikerros, joka määrittelee miten organisaatiot implementoivat agenttityökalut (MCP, ACP, UCP, A2A) niin, että autonomiset AI-agentit löytävät, ymmärtävät ja voivat asioida niiden kanssa ilman ihmisvälikättä.

Käytännön käyttöönotto-opas: [docs/implementation-roadmap.md](docs/implementation-roadmap.md)  
Protokollakartta: [docs/protocol-landscape.md](docs/protocol-landscape.md)

---

## Author

**Dani Forsberg**  
Head of AI Strategy — [RAD Intelligence](https://tekoalydani.com)  
[dani@tekoalydani.com](mailto:dani@tekoalydani.com)

---

## License

Apache 2.0 — see [LICENSE](LICENSE)
