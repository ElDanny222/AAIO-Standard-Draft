# Protocol Landscape

> **Status:** Draft v0.1 | Maintained by [Tekoäly-Dani](https://tekoalydani.com)

This document maps the agent protocol ecosystem and explains how each protocol relates to AAIO (Agentic AI Optimization).

---

## The Core Insight

There is no single "agentic web protocol." Instead, a stack of complementary protocols is emerging — each solving a distinct layer of the agent interaction problem. AAIO is not another protocol in this stack. It is the **implementation framework** that tells organizations how to adopt and combine these protocols correctly.

---

## Protocol Overview

### MCP — Model Context Protocol

| Attribute | Detail |
|-----------|--------|
| **Origin** | Anthropic (open standard) |
| **Purpose** | Connects AI models to external tools, data sources, and APIs |
| **Layer** | Context / tool access |
| **Status** | Active, widely adopted |

MCP defines how AI models (LLMs) discover and call external tools. A business that exposes an MCP server gives AI agents a structured way to query inventory, check availability, retrieve documents, or trigger actions — without requiring the agent to scrape HTML.

**AAIO relationship:** MCP server exposure is a core AAIO requirement. Without an MCP-compatible interface, AI agents fall back to unstructured web scraping, which is slow, brittle, and inaccessible to many agent architectures.

---

### ACP — Agent Commerce Protocol

| Attribute | Detail |
|-----------|--------|
| **Origin** | Emerging open standard |
| **Purpose** | Defines HTTP headers and signatures for machine-to-machine transactions |
| **Layer** | Payment / transaction authorization |
| **Status** | Draft |

ACP specifies how AI agents authenticate, authorize, and execute financial transactions without human approval at every step. It covers agent identity headers, transaction signing, and settlement hooks.

**AAIO relationship:** ACP is required for any AAIO implementation that supports autonomous purchasing (Level 3+ in the AAIO Readiness Score). Organizations that only need agent discovery and quoting can defer ACP implementation.

---

### UCP — Universal Commerce Protocol

| Attribute | Detail |
|-----------|--------|
| **Origin** | Emerging open standard |
| **Purpose** | Unified schema for service and product data accessible to AI agents |
| **Layer** | Data / structured content |
| **Status** | Draft |

UCP defines what fields a product or service listing must include to be fully machine-readable by agents. It extends and formalizes what schema.org started — but adds agent-specific fields such as negotiability flags, agent-readable SLAs, and machine-compatible pricing structures.

**AAIO relationship:** UCP compliance is required for AAIO Level 2+. It ensures that when an agent queries a product, it receives a complete, unambiguous, structured response rather than a human-readable webpage.

---

### A2A — Agent-to-Agent Protocol

| Attribute | Detail |
|-----------|--------|
| **Origin** | Google (open standard) |
| **Purpose** | Communication and negotiation protocol between autonomous agents |
| **Layer** | Agent coordination / multi-agent orchestration |
| **Status** | Active |

A2A defines how one agent talks to another — including capability discovery, task delegation, and result passing. In a commerce context, A2A enables buyer agents to query seller agents directly, negotiate terms, and confirm transactions through structured message exchange.

**AAIO relationship:** A2A is relevant for AAIO Level 4 (full agent commerce). Organizations that expose A2A-compatible agent endpoints allow buyer agents to interact without any human-facing interface at all.

---

### AGENTS.md

| Attribute | Detail |
|-----------|--------|
| **Origin** | Community convention (no formal standards body) |
| **Purpose** | Instructions file telling AI agents how to navigate and use a codebase or service |
| **Layer** | Discovery / context |
| **Status** | Convention |

`AGENTS.md` is a plain-text file placed in the root of a repository or website that tells AI agents what the system does, how it is structured, and what the agent is permitted to do. It is the agent equivalent of `robots.txt` — except descriptive rather than restrictive.

**AAIO relationship:** An `AGENTS.md` file (or equivalent `ai-instructions.txt` at the web root) is recommended for all AAIO Level 1+ implementations. It is the fastest, lowest-cost way to make a system agent-readable.

---

## How the Protocols Stack

```
┌─────────────────────────────────────────────────────────┐
│                        AAIO                              │
│         (Optimization framework — not a protocol)        │
│                                                           │
│  Defines WHEN and HOW to implement the layers below      │
└─────────────────────────────────────────────────────────┘
         │              │              │              │
         ▼              ▼              ▼              ▼
   ┌──────────┐   ┌──────────┐  ┌──────────┐  ┌──────────┐
   │  MCP     │   │   UCP    │  │   ACP    │  │   A2A    │
   │          │   │          │  │          │  │          │
   │ Tool     │   │ Data     │  │ Payment  │  │ Agent    │
   │ access   │   │ schema   │  │ headers  │  │ comms    │
   └──────────┘   └──────────┘  └──────────┘  └──────────┘
         │              │              │              │
         └──────────────┴──────────────┴──────────────┘
                                │
                         ┌──────────────┐
                         │  AGENTS.md   │
                         │  (discovery) │
                         └──────────────┘
```

---

## AAIO Readiness Levels

| Level | Name | Required Protocols |
|-------|------|-------------------|
| **0** | Not agent-ready | None |
| **1** | Discoverable | AGENTS.md (or equivalent) |
| **2** | Readable | MCP server + UCP-compliant data |
| **3** | Transactable | + ACP headers + pricing API |
| **4** | Fully autonomous | + A2A endpoint |

Organizations do not need to reach Level 4 to benefit from AAIO. Each level delivers independent value. Level 1 alone can significantly increase AI citation frequency in answer engines.

---

## What AAIO Does NOT Define

AAIO does not compete with or replace:

- **SEO** — still essential for human search traffic
- **AEO/GEO** — still essential for AI answer engine citation
- **MCP, ACP, UCP, A2A** — AAIO implements them, does not replace them
- **Schema.org structured data** — remains a foundational dependency

AAIO sits above all of these. It answers the question: *"Given that all these protocols exist, how does an organization adopt them in the right order, at the right depth, for their specific use case?"*

---

## Suomeksi / In Finnish

Tämä dokumentti kuvaa AI-agenttien protokollaekosysteemin:

- **MCP** — AI-mallien yhteys ulkoisiin työkaluihin ja datalähteisiin (Anthropic)
- **ACP** — Koneiden välisten maksujen ja transaktioiden otsakkeet
- **UCP** — Yhtenäinen palvelu- ja tuotedatastandardi AI-agenteille
- **A2A** — Agenttien välinen neuvottelu- ja koordinaatioprotokolla (Google)
- **AGENTS.md** — Tiedosto, joka kertoo AI-agenteille miten sivusto/repo toimii

**AAIO** ei ole uusi protokolla — se on optimointikehys, joka määrittelee miten organisaatiot implementoivat nämä protokollat oikeassa järjestyksessä ja oikealla syvyydellä.

Käytännön käyttöönotto-opas: [implementation-roadmap.md](implementation-roadmap.md)
