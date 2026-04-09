# AXO Framework v0.1

**Status:** Draft  
**Version:** 0.1.0  
**Date:** 2026-04-09  
**Authors:** [Tekoäly-Dani](https://tekoalydani.com)  
**License:** Apache 2.0  
**Parent Spec:** [AAIO Core Specification v0.1](aaio-core-v0.1.md)  

---

## Abstract

Agent Experience Optimization (AXO) is the UX/CX perspective on AAIO. While AAIO defines the technical requirements for agent-ready websites, AXO frames the same work through the lens of **how AI agents experience a website**. AXO is designed for UX designers, CX managers, product owners, and business decision-makers who need to understand AAIO in terms of user experience and customer journeys.

---

## 1. Introduction

### 1.1 A New User Has Arrived

Your website has a new category of user: the **AI agent**. Unlike human users who browse, scroll, and make emotional decisions, AI agents:

- Parse structured data, not visual layouts
- Follow programmatic paths, not visual hierarchies
- Evaluate data completeness, not aesthetic design
- Make decisions based on specifications, not marketing copy
- Need millisecond response times, not smooth animations

AXO is the discipline of designing web experiences that serve both human users and AI agent users.

### 1.2 AXO vs. Traditional UX

| Dimension | Human UX | Agent Experience (AXO) |
|-----------|----------|------------------------|
| **Input** | Visual, auditory, tactile | Structured data (JSON, XML, HTML) |
| **Navigation** | Click, scroll, search | API calls, link traversal, sitemap parsing |
| **Decision factors** | Brand, design, emotion, reviews | Data completeness, price accuracy, availability |
| **Speed expectation** | 1–3 seconds page load | < 500ms API response |
| **Error handling** | Human-readable error pages | Structured error responses (JSON with error codes) |
| **Authentication** | Login forms, SSO | API keys, OAuth 2.0 tokens |
| **Trust signals** | Brand reputation, design quality | Schema.org compliance, data consistency, HTTPS |
| **Conversion** | Add-to-cart button → checkout form | Cart API → Checkout API → Payment confirmation |

### 1.3 Target Audience

This framework is written for:

- **UX/CX Directors** evaluating digital strategy
- **Product Owners** planning feature roadmaps
- **Digital Strategists** assessing competitive positioning
- **E-commerce Managers** optimizing conversion funnels

For technical implementation details, see the [AAIO Core Specification](aaio-core-v0.1.md).

---

## 2. The Agent Journey

### 2.1 Mapping the Agent Customer Journey

Just as UX professionals map human customer journeys, AXO maps the **agent customer journey** — the steps an AI purchase agent takes from initial query to completed transaction.

```
Human Customer Journey          Agent Customer Journey
━━━━━━━━━━━━━━━━━━━━          ━━━━━━━━━━━━━━━━━━━━━
1. Awareness (ad, search)       1. Discovery (crawl, manifest)
2. Interest (browse, read)      2. Data Extraction (parse structured data)
3. Consideration (compare)      3. Comparison (cross-site data analysis)
4. Intent (add to cart)         4. Selection (best match algorithm)
5. Purchase (checkout)          5. Transaction (API checkout + payment)
6. Post-purchase (support)      6. Confirmation (structured receipt)
```

### 2.2 Agent Journey Stages

#### Stage 1: Discovery

**What happens:** The agent searches for a product/service and finds your website.

**AXO questions:**
- Can the agent find your site through answer engines, search APIs, or direct crawling?
- Does your site declare its capabilities via an AAIO manifest?
- Is there a `llms.txt` or `ai.txt` that helps the agent understand what you offer?

**AXO metrics:**
- Discovery rate: % of agent queries where your site appears as a candidate
- Manifest completeness: % of capabilities declared in AAIO manifest

#### Stage 2: Data Extraction

**What happens:** The agent reads product/service information from your pages.

**AXO questions:**
- Can the agent extract all relevant data without rendering JavaScript?
- Is pricing, availability, and product specification in structured data?
- Are there data conflicts between different representations on the same page?

**AXO metrics:**
- Data extraction success rate: % of data points successfully parsed
- Data completeness score: % of expected fields present in structured data
- Data consistency score: % alignment between structured data and visible content

#### Stage 3: Comparison

**What happens:** The agent compares your offering against competitors.

**AXO questions:**
- Does your structured data include all comparison-relevant fields?
- Are unique identifiers (SKU, GTIN) present for cross-site matching?
- Is your pricing transparent and machine-readable (no hidden fees)?

**AXO metrics:**
- Comparison inclusion rate: % of comparisons where your data is complete enough to include
- Price transparency score: % of total cost visible in structured data

#### Stage 4: Selection

**What happens:** The agent selects your product/service as the best match.

**AXO questions:**
- Does your data clearly state differentiators (warranty, delivery, ratings)?
- Are reviews and ratings in Schema.org format?
- Is delivery/shipping information machine-readable?

**AXO metrics:**
- Selection rate: % of comparisons where your product is selected
- Data advantage score: fields present that competitors lack

#### Stage 5: Transaction

**What happens:** The agent completes the purchase on your site.

**AXO questions:**
- Can the agent add to cart and checkout via API?
- Is the checkout flow accessible without human intervention?
- Does the payment process support agent authentication?

**AXO metrics:**
- Transaction success rate: % of attempted transactions completed
- Transaction time: seconds from selection to confirmation
- Error recovery rate: % of failed transactions successfully retried

#### Stage 6: Confirmation

**What happens:** The agent receives and processes the order confirmation.

**AXO questions:**
- Is the confirmation structured (JSON) or only human-readable (HTML email)?
- Does the confirmation include all order details the agent needs to report?
- Is tracking information machine-readable?

**AXO metrics:**
- Confirmation parsing success: % of confirmations fully parsed by agent
- Post-purchase data completeness: % of expected fields in confirmation

---

## 3. AXO Assessment Framework

### 3.1 The AXO Scorecard

The AXO Scorecard translates the technical AAIO Readiness Score into business-oriented metrics that UX/CX teams understand.

| AXO Dimension | AAIO Pillar | Business Question |
|---------------|-------------|-------------------|
| **Findability** | Discovery | Can AI agents find us? |
| **Understandability** | Machine-Readability | Can AI agents understand our offerings? |
| **Usability** | Navigability | Can AI agents navigate our site efficiently? |
| **Convertibility** | Transactability | Can AI agents buy from us? |
| **Reliability** | Cross-cutting | Can AI agents trust our data? |

### 3.2 AXO Maturity Model

| Level | Name | Description | Business Impact |
|-------|------|-------------|-----------------|
| **Level 0** | Invisible | No AXO optimization | AI agents cannot find or use your site. You lose every agent-mediated sale. |
| **Level 1** | Findable | Basic discovery and some structured data | Agents can find you but may not extract enough data to include you in comparisons. |
| **Level 2** | Comparable | Strong structured data, agents can compare | Agents include you in comparisons. Whether you win depends on your offering. |
| **Level 3** | Transactable | API-based commerce, agents can buy | Agents can complete purchases. You capture agent-mediated revenue. |
| **Level 4** | Optimized | Full AXO with A2A negotiation | Agents prefer your site. Maximum agent-mediated conversion. |

### 3.3 Competitive Implications

```
                    Your AXO Level
                    0    1    2    3    4
Competitor AXO  0 [ =  ] [+  ] [++ ] [+++] [+++]
Level       1 [ - ] [ = ] [+  ] [++ ] [+++]
            2 [ --] [ - ] [ = ] [+  ] [++ ]
            3 [---] [ --] [ - ] [ = ] [+  ]
            4 [---] [---] [ --] [ - ] [ = ]

Legend: +++ = strong advantage, = = parity, --- = strong disadvantage
```

In agent-mediated commerce, the site with the higher AXO level wins disproportionately — agents optimize for data quality and transaction efficiency, not brand loyalty.

---

## 4. AXO Design Principles

### 4.1 Principle 1: Dual-Layer Design

Design every page with two layers:

1. **Human layer**: Visual design, marketing copy, imagery, interactive elements
2. **Agent layer**: Structured data, API endpoints, machine-readable metadata

These layers SHOULD NOT conflict. The agent layer must be a faithful, machine-readable representation of the human layer.

### 4.2 Principle 2: Data First, Presentation Second

For agent users, the structured data IS the experience. Invest in:

- Complete Schema.org markup with all relevant fields
- Accurate, real-time pricing and availability
- Unique identifiers for every entity
- Clear categorization and taxonomy

### 4.3 Principle 3: Fail Gracefully for Agents

When things go wrong, agents need:

- **Structured error responses** (JSON with error code, message, and recovery suggestion)
- **Accurate HTTP status codes** (no soft 404s, correct 301 redirects)
- **Rate limit information** (`429` with `Retry-After` header)
- **Availability alternatives** ("out of stock" with "similar products" endpoint)

### 4.4 Principle 4: Speed Is UX for Agents

Agent experience degrades sharply above 500ms response time:

| Response Time | Agent Perception |
|---------------|-----------------|
| < 200ms | Excellent — preferred source |
| 200–500ms | Good — standard inclusion |
| 500ms–2s | Degraded — may skip in time-constrained tasks |
| > 2s | Poor — excluded from real-time comparisons |

### 4.5 Principle 5: Transparency Builds Trust

Agents evaluate trust through data consistency:

- Price on page = price in Schema.org = price in API response
- Availability stated = availability when checkout is attempted
- Delivery estimate is reliable and machine-readable
- Return policy is clear and structured

---

## 5. AXO for E-Commerce

### 5.1 Product Page AXO Checklist

| Element | Human Layer | Agent Layer |
|---------|-------------|-------------|
| Product name | `<h1>` heading | `schema:name` |
| Price | Visible price display | `schema:price` + `priceCurrency` |
| Availability | "In stock" label | `schema:availability` |
| Description | Marketing copy | `schema:description` (factual) |
| Images | Product gallery | `schema:image` (URLs) |
| Reviews | Star rating + reviews | `schema:aggregateRating` |
| SKU | Often hidden | `schema:sku` (MUST be present) |
| Brand | Logo + name | `schema:brand` |
| Category | Breadcrumb | `schema:category` + `BreadcrumbList` |
| Shipping | Delivery info section | `schema:shippingDetails` |
| Returns | Return policy link | `schema:hasMerchantReturnPolicy` |

### 5.2 Category Page AXO Checklist

- Machine-readable product listing (not just visual grid)
- Filterable via API parameters (price range, brand, attributes)
- Pagination with `rel="next"` / `rel="prev"`
- Category hierarchy in `BreadcrumbList` markup
- Product count and sort options in structured data

### 5.3 Checkout Flow AXO

```
Human Checkout Flow              Agent Checkout Flow
━━━━━━━━━━━━━━━━━━              ━━━━━━━━━━━━━━━━━━━
1. Click "Add to cart"           1. POST /api/cart/add {sku, qty}
2. View cart page                2. GET /api/cart
3. Enter shipping address        3. POST /api/checkout {address, ...}
4. Select payment method         4. POST /api/payment {method, token}
5. Confirm order                 5. POST /api/order/confirm
6. See confirmation page         6. GET /api/order/{id} → JSON receipt
```

---

## 6. AXO Audit Process

### 6.1 How to Conduct an AXO Audit

1. **Agent Simulation**: Navigate the site as an AI agent would — using structured data, APIs, and sitemap
2. **Data Extraction Test**: Attempt to extract all product/service data from structured data alone
3. **Comparison Test**: Can an agent build a complete comparison table from your data?
4. **Transaction Test**: Can an agent complete a purchase through APIs?
5. **Error Handling Test**: How does the site respond to agent errors (wrong SKU, out of stock)?
6. **Speed Test**: Measure API response times under realistic agent load
7. **Consistency Test**: Compare data across human layer, structured data, and API responses

### 6.2 Common AXO Issues by Industry

| Industry | Top AXO Issue | Impact |
|----------|---------------|--------|
| E-Commerce | JavaScript-only product data | Agents cannot extract product information |
| SaaS | Pricing hidden behind "Contact Us" | Agents cannot compare pricing |
| Professional Services | No structured service descriptions | Agents cannot match services to queries |
| Travel | Dynamic pricing without API | Agents get stale prices |
| Real Estate | Image-heavy, data-light listings | Agents cannot compare properties |

---

## 7. Business Case for AXO

### 7.1 Market Drivers

- **AI agent commerce** is projected to reach $7.3B by 2028 (40%+ CAGR)
- **Generational shift**: younger consumers increasingly delegate purchase decisions to AI assistants
- **B2B procurement**: enterprise buyers are deploying AI agents for vendor selection and purchasing
- **First-mover advantage**: AXO optimization today creates a competitive moat as agent commerce grows

### 7.2 ROI Framework

| Investment | Expected Return |
|------------|----------------|
| Schema.org markup (1–2 weeks) | Included in AI comparisons, AEO citations |
| API-based product catalog (2–4 weeks) | Agent can extract and compare all products |
| Checkout API (4–8 weeks) | Agent can complete purchases (new revenue channel) |
| Full AXO optimization (8–16 weeks) | Maximum agent-mediated conversion |

### 7.3 Risk of Inaction

Sites without AXO optimization face:

- **Invisible to agents**: Not included in AI-mediated purchase decisions
- **Data disadvantage**: Competitors with better structured data win agent comparisons
- **Revenue leakage**: Agent-mediated commerce grows while your share stays flat
- **Retroactive catch-up**: Implementing AXO later is harder than doing it now

---

## 8. AXO and Human UX: Synergies

AXO investment is NOT separate from human UX improvement:

| AXO Investment | Human UX Benefit |
|----------------|-----------------|
| Schema.org markup | Rich search results, better SEO |
| Faster API responses | Faster page loads for humans too |
| Structured error handling | Better error pages for human users |
| Complete product data | Better product pages for human browsing |
| API-based checkout | Headless commerce, mobile optimization |
| Data consistency | Fewer customer complaints about wrong prices |

AXO is not a cost center competing with human UX — it is a multiplier that improves both channels simultaneously.

---

## Appendix A: AXO Glossary

| Term | Definition |
|------|-----------|
| **AXO** | Agent Experience Optimization — the UX perspective on AAIO |
| **Agent Journey** | The steps an AI agent takes from discovery to transaction |
| **Dual-Layer Design** | Designing pages with both a human layer and an agent layer |
| **AXO Scorecard** | Business-oriented assessment of agent experience quality |
| **Convertibility** | An agent's ability to complete a transaction on a website |
| **Data Advantage** | Having more complete/accurate structured data than competitors |

---

*This framework is part of the [AAIO Standard Draft](../README.md) project by [Tekoäly-Dani](https://tekoalydani.com).*
