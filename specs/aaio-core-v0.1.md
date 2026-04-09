# AAIO Core Specification v0.1

**Status:** Draft  
**Version:** 0.1.0  
**Date:** 2026-04-09  
**Authors:** Tekoaly-Dani / RAD Intelligence  
**License:** Apache 2.0  

---

## Abstract

Agentic AI Optimization (AAIO) is an optimization layer that defines how websites and digital services should be structured so that autonomous AI agents can **discover**, **understand**, **navigate**, and **transact** with them. AAIO does not introduce a new protocol — it specifies how existing protocols (MCP, ACP, UCP, A2A) and web standards (Schema.org, OpenAPI, robots.txt) should be implemented for optimal agent interoperability.

---

## 1. Introduction

### 1.1 Background

The web is entering a new era where autonomous AI agents act on behalf of users — researching products, comparing services, negotiating prices, and executing purchases. Traditional SEO optimizes for search engine crawlers and human readers. AAIO optimizes for a fundamentally different consumer: **the AI purchase agent**.

### 1.2 Scope

This specification defines:

- The **AAIO Readiness Model**: capabilities a website must have for agent interoperability
- The **AAIO Readiness Score**: a quantitative framework (0–100) for measuring agent-readiness
- Requirements for **machine-readability**, **navigability**, and **transactability**
- Integration points with existing protocols (MCP, ACP, UCP, A2A)

### 1.3 Relationship to SEO, AEO, and GEO

AAIO is the most advanced layer in the **AIO (AI Optimization)** stack. The layers are cumulative — each builds on the previous:

| Layer | Full Name | Target | Optimizes For |
|-------|-----------|--------|---------------|
| **SEO** | Search Engine Optimization | Search engine crawlers | Rankings, organic traffic |
| **AEO** | Answer Engine Optimization | AI answer engines (ChatGPT, Perplexity, Gemini) | Being cited as an authoritative source |
| **GEO** | Generative Engine Optimization | AI-generated synthesized answers | Appearing in LLM-generated responses |
| **AAIO** | Agentic AI Optimization | Autonomous AI purchase agents | Discovery + citation + navigation + transaction |

**Key principle:** AAIO does NOT replace SEO, AEO, or GEO. They stack cumulatively. A site that scores well on AAIO must also have strong SEO, AEO, and GEO foundations.

### 1.4 Terminology

See [terminology.md](../docs/terminology.md) for the full glossary. Key terms:

- **AI Agent**: An autonomous software entity that acts on behalf of a user to accomplish a goal
- **Purchase Agent**: An AI agent specifically tasked with finding, comparing, and buying products/services
- **Agent Manifest**: A machine-readable file declaring a site's agent capabilities (see Section 5)
- **AAIO Readiness Score**: A quantitative measure (0–100) of a site's agent-optimization level

---

## 2. AAIO Readiness Model

The AAIO Readiness Model defines four pillars that a website must address to be fully optimized for autonomous AI agents.

### 2.1 The Four Pillars

```
┌─────────────────────────────────────────────────────┐
│                  AAIO READINESS                      │
├──────────────┬──────────────┬────────────┬───────────┤
│  DISCOVERY   │  READABILITY │ NAVIGATION │ TRANSACT  │
│              │              │            │           │
│  Can agents  │  Can agents  │ Can agents │ Can agents│
│  find you?   │  understand  │ move thru  │ buy/book? │
│              │  your data?  │ your site? │           │
├──────────────┼──────────────┼────────────┼───────────┤
│  robots.txt  │  Schema.org  │ Sitemaps   │ Checkout  │
│  llms.txt    │  JSON-LD     │ Internal   │ APIs      │
│  ai.txt      │  OpenAPI     │ links      │ Payment   │
│  .well-known │  Microdata   │ Breadcrumb │ flows     │
│  Agent       │  Product     │ Search     │ A2A       │
│  manifest    │  feeds       │ endpoints  │ ACP       │
└──────────────┴──────────────┴────────────┴───────────┘
```

### 2.2 Pillar 1: Discovery

Discovery is the ability of AI agents to find and identify a website as relevant to their task.

#### 2.2.1 Requirements

| Requirement | Priority | Description |
|-------------|----------|-------------|
| `robots.txt` agent directives | MUST | Explicit allow/disallow rules for AI agent user-agents |
| `llms.txt` | SHOULD | LLM-readable site summary at `/llms.txt` (see [llms.txt specification](https://llmstxt.org/)) |
| `ai.txt` | SHOULD | AI policy declaration at `/ai.txt` |
| `.well-known/ai-plugin.json` | MAY | OpenAI plugin manifest or equivalent |
| AAIO Agent Manifest | SHOULD | Machine-readable capability declaration (see Section 5) |
| Structured sitemap | MUST | XML sitemap with `<lastmod>` and `<changefreq>` |
| Schema.org `WebSite` | MUST | JSON-LD `WebSite` markup with `potentialAction` for search |

#### 2.2.2 Agent User-Agent Strings

Sites SHOULD recognize and handle the following agent user-agent patterns:

```
# AI Search/Answer Engines
GPTBot
Google-Extended
ClaudeBot
PerplexityBot
Applebot-Extended

# AI Purchase/Commerce Agents
AAIO-Agent/*
MCP-Client/*
A2A-Agent/*
```

### 2.3 Pillar 2: Machine-Readability

Machine-readability ensures that AI agents can extract structured, unambiguous information from a website.

#### 2.3.1 Requirements

| Requirement | Priority | Description |
|-------------|----------|-------------|
| Schema.org JSON-LD | MUST | Product, Service, Organization, Offer markup |
| Pricing in structured data | MUST | `price`, `priceCurrency`, `availability` in Schema.org |
| OpenAPI specification | SHOULD | API endpoints documented in OpenAPI 3.x format |
| Product feeds | SHOULD | Machine-readable product catalog (JSON, XML, or CSV) |
| Consistent data format | MUST | Same entity = same data everywhere (no conflicting prices) |
| Canonical URLs | MUST | `rel="canonical"` to prevent duplicate entity confusion |

#### 2.3.2 Schema.org Minimum Viable Markup

For e-commerce, the following Schema.org types MUST be present:

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Product Name",
  "description": "Clear, factual product description",
  "sku": "UNIQUE-SKU-123",
  "brand": {
    "@type": "Brand",
    "name": "Brand Name"
  },
  "offers": {
    "@type": "Offer",
    "price": 99.99,
    "priceCurrency": "EUR",
    "availability": "https://schema.org/InStock",
    "url": "https://example.com/product/unique-sku-123",
    "priceValidUntil": "2026-12-31",
    "seller": {
      "@type": "Organization",
      "name": "Seller Name"
    }
  },
  "aggregateRating": {
    "@type": "AggregateRating",
    "ratingValue": 4.5,
    "reviewCount": 128
  }
}
```

#### 2.3.3 Data Quality Principles

1. **Single source of truth**: Each entity (product, service, price) MUST have one canonical representation
2. **Temporal accuracy**: Prices, availability, and inventory MUST reflect real-time state (or declare staleness)
3. **Disambiguation**: Every entity MUST have a unique, stable identifier (SKU, GTIN, or URI)
4. **Completeness**: Missing data is worse than approximate data — agents cannot infer what is not stated

### 2.4 Pillar 3: Navigability

Navigability defines how well AI agents can traverse a website to find specific information.

#### 2.4.1 Requirements

| Requirement | Priority | Description |
|-------------|----------|-------------|
| Logical URL structure | MUST | Predictable, hierarchical URL paths |
| XML sitemap | MUST | Complete, up-to-date sitemap at `/sitemap.xml` |
| Breadcrumb markup | SHOULD | `BreadcrumbList` Schema.org markup on all pages |
| Internal search API | SHOULD | Programmatic search endpoint (JSON responses) |
| Pagination with `rel` links | MUST | `rel="next"` / `rel="prev"` for paginated content |
| Category taxonomy | SHOULD | Machine-readable category hierarchy |
| HTTP status codes | MUST | Correct 200/301/404/410 responses (no soft 404s) |

#### 2.4.2 Agent Navigation Patterns

AI agents typically navigate websites using these strategies:

1. **Manifest-first**: Read agent manifest → follow declared endpoints
2. **Sitemap crawl**: Parse sitemap → identify relevant URLs by pattern
3. **Search-based**: Use site search API → navigate to results
4. **Link-following**: Follow internal links from landing page → depth-first exploration

Sites optimized for AAIO SHOULD support all four patterns.

### 2.5 Pillar 4: Transactability

Transactability is the ability of AI agents to complete commercial actions (purchase, book, subscribe) on a website.

#### 2.5.1 Requirements

| Requirement | Priority | Description |
|-------------|----------|-------------|
| Machine-readable checkout | MUST | Checkout flow accessible without JavaScript rendering |
| API-based ordering | SHOULD | REST/GraphQL API for order creation |
| Clear terms of service | MUST | Machine-parseable ToS (or structured summary) |
| Payment protocol support | SHOULD | ACP-compatible payment flow |
| Order confirmation | MUST | Structured order confirmation (JSON or email) |
| Return/refund policy | SHOULD | Machine-readable return policy in Schema.org |
| Authentication | MAY | OAuth 2.0 or API key authentication for agent sessions |

#### 2.5.2 Transaction Maturity Levels

| Level | Name | Description |
|-------|------|-------------|
| L0 | **Information Only** | Agent can read product data but cannot transact |
| L1 | **Cart-Ready** | Agent can add items to cart via API |
| L2 | **Checkout-Ready** | Agent can complete checkout (payment requires human approval) |
| L3 | **Fully Autonomous** | Agent can complete entire transaction including payment (via ACP) |

#### 2.5.3 A2A Commerce Integration

For Level 3 transactability, sites SHOULD implement the [A2A protocol](https://github.com/google/A2A) to enable:

- **Agent-to-agent negotiation**: Buyer agent ↔ Seller agent price/terms negotiation
- **Structured task delegation**: Complex multi-step transactions as A2A tasks
- **Status tracking**: Real-time transaction status via A2A task updates

---

## 3. AAIO Readiness Score

### 3.1 Overview

The AAIO Readiness Score is a quantitative measure (0–100) that evaluates how well a website is optimized for autonomous AI agents. The score is composed of four category scores aligned with the four pillars.

### 3.2 Scoring Framework

| Category | Weight | Max Points | Description |
|----------|--------|------------|-------------|
| Discovery | 20% | 20 | Can agents find and identify the site? |
| Machine-Readability | 35% | 35 | Can agents extract structured data? |
| Navigability | 20% | 20 | Can agents traverse the site effectively? |
| Transactability | 25% | 25 | Can agents complete commercial actions? |
| **Total** | **100%** | **100** | |

### 3.3 Scoring Rubric

#### 3.3.1 Discovery Score (0–20)

| Check | Points | Criteria |
|-------|--------|----------|
| robots.txt with agent rules | 4 | AI agent user-agents explicitly addressed |
| llms.txt present | 3 | Valid llms.txt at site root |
| XML sitemap | 4 | Complete, valid, recently updated |
| Schema.org WebSite | 3 | JSON-LD WebSite with SearchAction |
| AAIO Agent Manifest | 4 | Valid manifest file (see Section 5) |
| ai.txt present | 2 | AI policy declaration |

#### 3.3.2 Machine-Readability Score (0–35)

| Check | Points | Criteria |
|-------|--------|----------|
| Schema.org Product/Service | 8 | Complete JSON-LD for all products/services |
| Pricing in structured data | 6 | Price, currency, availability in markup |
| Data consistency | 5 | No conflicts between structured data and page content |
| OpenAPI specification | 5 | Documented API endpoints |
| Unique identifiers | 4 | SKU/GTIN/URI for all entities |
| Product feeds | 4 | Machine-readable catalog available |
| Temporal accuracy | 3 | Prices/availability reflect current state |

#### 3.3.3 Navigability Score (0–20)

| Check | Points | Criteria |
|-------|--------|----------|
| Logical URL structure | 4 | Predictable, hierarchical paths |
| Breadcrumb markup | 3 | BreadcrumbList on relevant pages |
| Internal search API | 4 | Programmatic search returning structured results |
| Pagination | 3 | Correct rel=next/prev implementation |
| HTTP status codes | 3 | No soft 404s, correct redirects |
| Category taxonomy | 3 | Machine-readable category hierarchy |

#### 3.3.4 Transactability Score (0–25)

| Check | Points | Criteria |
|-------|--------|----------|
| Machine-readable checkout | 6 | Checkout accessible without JS rendering |
| API-based ordering | 5 | REST/GraphQL order creation endpoint |
| Structured ToS | 3 | Machine-parseable terms |
| Payment protocol (ACP) | 4 | ACP-compatible payment flow |
| Order confirmation | 3 | Structured confirmation response |
| Return policy markup | 2 | Schema.org MerchantReturnPolicy |
| A2A integration | 2 | A2A protocol support for agent negotiation |

### 3.4 Score Tiers

| Score | Tier | Label | Description |
|-------|------|-------|-------------|
| 0–19 | F | **Not Ready** | No agent optimization; invisible to AI agents |
| 20–39 | D | **Basic** | Minimal structured data; agents can find but not transact |
| 40–59 | C | **Developing** | Good discovery and readability; limited transactability |
| 60–79 | B | **Agent-Ready** | Strong across all pillars; agents can navigate and transact |
| 80–100 | A | **Agent-Optimized** | Best-in-class; fully autonomous agent commerce |

### 3.5 Scoring Schema

See [`schemas/aaio-scoring.schema.json`](../schemas/aaio-scoring.schema.json) for the machine-readable scoring output format.

---

## 4. Protocol Integration

### 4.1 Protocol Landscape

AAIO operates as an optimization layer on top of existing protocols:

```
┌─────────────────────────────────────────────┐
│              AAIO (Optimization Layer)        │
│   "How to implement protocols for agents"    │
├─────────────┬──────────┬──────────┬──────────┤
│    MCP      │   ACP    │   UCP    │   A2A    │
│  (Context)  │(Commerce)│(Unified) │(Agent)   │
├─────────────┴──────────┴──────────┴──────────┤
│         Web Standards (HTTP, JSON-LD,         │
│         Schema.org, OpenAPI, OAuth)           │
└───────────────────────────────────────────────┘
```

### 4.2 Model Context Protocol (MCP)

**Role in AAIO:** MCP provides context sharing between AI models and external tools/data sources.

**AAIO requirements:**
- Sites SHOULD expose MCP-compatible tool descriptions for their APIs
- Product/service data SHOULD be accessible via MCP resource endpoints
- MCP server implementations SHOULD follow the agent manifest declaration

**Reference:** [Model Context Protocol Specification](https://modelcontextprotocol.io/)

### 4.3 Agent Commerce Protocol (ACP)

**Role in AAIO:** ACP handles secure machine-to-machine payment transactions.

**AAIO requirements:**
- Sites targeting Level 2+ transactability SHOULD support ACP payment headers
- Payment flows MUST include clear confirmation/rejection signals
- Transaction logging MUST be maintained for audit purposes

### 4.4 Universal Commerce Protocol (UCP)

**Role in AAIO:** UCP provides a unified data standard for service and product information.

**AAIO requirements:**
- Product/service data SHOULD conform to UCP schema definitions where applicable
- UCP-compliant feeds enable cross-platform agent comparison shopping

### 4.5 Agent-to-Agent Protocol (A2A)

**Role in AAIO:** A2A enables direct communication between buyer and seller agents.

**AAIO requirements:**
- Sites offering Level 3 transactability SHOULD implement an A2A-compatible agent endpoint
- A2A Agent Cards SHOULD be published at `/.well-known/agent.json`
- Task-based interaction patterns SHOULD follow the A2A task lifecycle

**Reference:** [Google A2A Protocol](https://github.com/google/A2A)

---

## 5. AAIO Agent Manifest

### 5.1 Purpose

The AAIO Agent Manifest is a machine-readable JSON file that declares a website's agent capabilities, supported protocols, and available endpoints. It serves as the entry point for AI agents discovering a site's AAIO features.

### 5.2 Location

The manifest SHOULD be served at:

```
/.well-known/aaio-manifest.json
```

### 5.3 Schema

See [`schemas/aaio-manifest.schema.json`](../schemas/aaio-manifest.schema.json) for the full JSON Schema definition.

### 5.4 Example

```json
{
  "$schema": "https://aaio-standard.org/schemas/aaio-manifest.schema.json",
  "version": "0.1",
  "name": "Example Store",
  "description": "Finnish e-commerce store optimized for AI agents",
  "url": "https://store.example.fi",
  "contact": "ai-support@example.fi",
  "aaioVersion": "0.1",
  "capabilities": {
    "discovery": {
      "robotsTxt": true,
      "llmsTxt": true,
      "aiTxt": true,
      "sitemap": "https://store.example.fi/sitemap.xml",
      "agentManifest": true
    },
    "readability": {
      "schemaOrg": ["Product", "Offer", "Organization", "BreadcrumbList"],
      "openApi": "https://store.example.fi/api/v1/openapi.json",
      "productFeed": "https://store.example.fi/feeds/products.json",
      "dataFormats": ["json-ld", "microdata"]
    },
    "navigation": {
      "searchEndpoint": "https://store.example.fi/api/v1/search",
      "categoryEndpoint": "https://store.example.fi/api/v1/categories",
      "breadcrumbs": true,
      "pagination": true
    },
    "transaction": {
      "level": "L2",
      "checkoutApi": "https://store.example.fi/api/v1/checkout",
      "cartApi": "https://store.example.fi/api/v1/cart",
      "paymentProtocols": ["acp-v1"],
      "authentication": ["oauth2", "api-key"],
      "tosUrl": "https://store.example.fi/terms",
      "returnPolicyUrl": "https://store.example.fi/returns"
    }
  },
  "protocols": {
    "mcp": {
      "supported": true,
      "serverUrl": "https://store.example.fi/mcp"
    },
    "a2a": {
      "supported": true,
      "agentCard": "https://store.example.fi/.well-known/agent.json"
    },
    "acp": {
      "supported": true,
      "version": "1.0"
    }
  },
  "rateLimit": {
    "requestsPerMinute": 60,
    "burstLimit": 10
  },
  "lastUpdated": "2026-04-09T00:00:00Z"
}
```

---

## 6. Implementation Guide

### 6.1 Quick Start Checklist

For sites beginning their AAIO journey, implement in this order:

**Phase 1: Foundation (Score target: 20–40)**
- [ ] Add Schema.org JSON-LD for all products/services
- [ ] Create/update `robots.txt` with AI agent directives
- [ ] Ensure XML sitemap is complete and up-to-date
- [ ] Validate all pricing is in structured data

**Phase 2: Enhancement (Score target: 40–60)**
- [ ] Create `llms.txt` with site summary
- [ ] Implement breadcrumb markup
- [ ] Add internal search API (JSON responses)
- [ ] Publish OpenAPI specification
- [ ] Create AAIO Agent Manifest

**Phase 3: Commerce (Score target: 60–80)**
- [ ] Implement API-based cart/checkout
- [ ] Add machine-readable ToS and return policy
- [ ] Ensure checkout works without JavaScript rendering
- [ ] Implement product feeds

**Phase 4: Autonomy (Score target: 80–100)**
- [ ] Implement ACP payment protocol
- [ ] Deploy A2A agent endpoint
- [ ] Publish MCP tool descriptions
- [ ] Enable fully autonomous transactions

### 6.2 Common Pitfalls

| Pitfall | Impact | Solution |
|---------|--------|----------|
| JavaScript-only rendering | Agents cannot read content | Server-side rendering or static HTML fallback |
| Inconsistent pricing | Agent confusion, trust loss | Single source of truth for all prices |
| Missing `rel=canonical` | Duplicate entity confusion | Canonical URLs on all pages |
| CAPTCHAs blocking agents | Complete agent exclusion | Agent-specific authentication (API keys, OAuth) |
| Stale sitemaps | Agents navigate to 404s | Automated sitemap generation |
| No structured error responses | Agent cannot handle failures | JSON error responses with error codes |

---

## 7. Security Considerations

### 7.1 Agent Authentication

Sites SHOULD implement tiered access:

1. **Public tier**: Unauthenticated read access to product/service information
2. **Registered tier**: API key-based access to search, feeds, and detailed data
3. **Transactional tier**: OAuth 2.0 or equivalent for checkout and payment operations

### 7.2 Rate Limiting

Sites MUST implement rate limiting for agent traffic:

- Declare rate limits in the AAIO Agent Manifest
- Return `429 Too Many Requests` with `Retry-After` header when limits are exceeded
- Consider separate rate limit tiers for authenticated vs. unauthenticated agents

### 7.3 Data Privacy

- Agent access MUST comply with GDPR and applicable privacy regulations
- Personal data MUST NOT be exposed through structured data or APIs without consent
- Transaction data MUST be encrypted in transit (TLS 1.2+)

---

## 8. Conformance

### 8.1 Conformance Levels

| Level | Name | Requirements |
|-------|------|--------------|
| **AAIO Basic** | Discovery + Readability | All MUST requirements from Pillars 1–2 |
| **AAIO Standard** | + Navigability | All MUST requirements from Pillars 1–3 |
| **AAIO Commerce** | + Transactability L1–L2 | All MUST requirements from all Pillars, L2 transaction |
| **AAIO Full** | + Autonomous Commerce | All requirements including L3 transaction and protocol integration |

### 8.2 Validation

Conformance can be validated using:

1. The AAIO Readiness Score assessment (Section 3)
2. Automated schema validation against the AAIO manifest schema
3. The Tekoaly-Dani AAIO Audit service

---

## 9. Future Work

- **v0.2**: Formalized ACP integration requirements
- **v0.3**: Multi-agent transaction patterns (agent swarms)
- **v0.4**: Cross-border commerce considerations (multi-currency, multi-jurisdiction)
- **v1.0**: Stable specification with industry review

---

## Appendix A: References

- [Schema.org](https://schema.org/) — Structured data vocabulary
- [OpenAPI Specification](https://spec.openapis.org/oas/latest.html) — API documentation standard
- [Model Context Protocol](https://modelcontextprotocol.io/) — AI model context sharing
- [Google A2A Protocol](https://github.com/google/A2A) — Agent-to-agent communication
- [llms.txt Specification](https://llmstxt.org/) — LLM-readable site summaries
- [RFC 9110](https://www.rfc-editor.org/rfc/rfc9110) — HTTP Semantics
- [GDPR](https://gdpr-info.eu/) — EU General Data Protection Regulation

## Appendix B: Change Log

| Version | Date | Changes |
|---------|------|---------|
| 0.1.0 | 2026-04-09 | Initial draft |

---

*This specification is maintained by [Tekoaly-Dani](https://tekoalydani.com) as part of the AAIO Standard Draft project.*
