# AAIO Implementation Roadmap

> **Status:** Draft v0.1 | Maintained by [RAD Intelligence](https://tekoalydani.com)

A practical, phase-by-phase guide for organizations implementing Agentic AI Optimization (AAIO).

---

## Before You Start

AAIO implementation is not an all-or-nothing project. Each phase delivers standalone value. A business at Phase 2 is significantly better positioned than one at Phase 0 — even if it never reaches Phase 4.

Start with the [AAIO Audit](#getting-an-aaio-audit) to understand your current baseline before committing to a roadmap.

---

## Phase 0 — Assessment

**Goal:** Understand where you are today.

### Actions

1. **Audit your current agent-readiness**
   - Can AI agents currently access your product/service data in structured form?
   - Do you have an `AGENTS.md` or `ai-instructions.txt` at your web root?
   - Is your schema.org structured data complete and accurate?
   - Do you have an API or MCP server?

2. **Define your target use case**
   - Do you need agents to discover you? (Level 1 target)
   - Do you need agents to read and compare your services? (Level 2 target)
   - Do you need agents to place orders autonomously? (Level 3–4 target)

3. **Inventory your existing infrastructure**
   - What APIs do you already expose?
   - What CMS or e-commerce platform do you use?
   - What is your current schema.org implementation?

**Deliverable:** A clear picture of your current AAIO level (0–4) and your target level.

---

## Phase 1 — Discovery Layer

**Goal:** Make your business discoverable by AI agents. (AAIO Level 1)

**Estimated effort:** 1–3 days

### Actions

1. **Create `AGENTS.md`** at your web root (`yourdomain.com/AGENTS.md`)

   Minimum required content:
   ```markdown
   # Agent Instructions

   ## What this site is
   [One paragraph describing your business and what you offer]

   ## What agents can do here
   - [List actions agents are permitted to take]

   ## Key endpoints
   - Products/services: [URL]
   - Pricing: [URL]
   - Contact/booking: [URL]

   ## Data formats available
   - [JSON-LD / XML / API / etc.]
   ```

2. **Update your `robots.txt`**

   Ensure legitimate AI crawlers are not blocked:
   ```
   User-agent: GPTBot
   Allow: /

   User-agent: ClaudeBot
   Allow: /

   User-agent: PerplexityBot
   Allow: /
   ```

3. **Verify and complete schema.org structured data**
   - `Organization` with all fields
   - `Product` or `Service` for all key offerings
   - `FAQPage` for common questions
   - `ContactPoint` for agent-accessible contact

4. **Submit to AI directories and citation sources**
   - Ensure Wikipedia, Wikidata, and LinkedIn are accurate
   - Submit to relevant industry directories

**Verification:** Ask ChatGPT, Claude, or Perplexity to describe your business. Compare the response against your actual offerings. Gaps indicate missing structured data or poor citation coverage.

---

## Phase 2 — Readability Layer

**Goal:** Enable AI agents to read, parse, and compare your offerings programmatically. (AAIO Level 2)

**Estimated effort:** 1–4 weeks

### Actions

1. **Expose a machine-readable product/service API**

   Your data must be accessible at a stable endpoint in JSON or JSON-LD format. Minimum fields for a service offering:
   - Name, description, category
   - Pricing (amount, currency, billing period)
   - Availability / capacity
   - Delivery method (remote, on-site, etc.)
   - Contact or booking endpoint

2. **Implement UCP-compliant data structure**

   Follow the [UCP Integration Guide](../specs/ucp-integration-v0.1.md) to ensure your data fields match the agent-readable standard.

3. **Deploy an MCP server** (recommended)

   An MCP server gives AI agents a structured, tool-based interface to your data. It replaces web scraping with clean API calls.

   Basic MCP server capabilities to expose:
   - `list_products` or `list_services`
   - `get_product_details` (by ID or name)
   - `check_availability`
   - `get_pricing`

4. **Test with actual AI agents**

   Use Claude, GPT-4, or Perplexity API to query your MCP server or API directly. Verify that responses are complete, accurate, and parseable.

**Verification:** An AI agent should be able to produce an accurate product comparison sheet using only your machine-readable data, without visiting your website.

---

## Phase 3 — Transactable Layer

**Goal:** Enable AI agents to initiate and complete transactions on behalf of human principals. (AAIO Level 3)

**Estimated effort:** 2–8 weeks (depends heavily on existing payment infrastructure)

### Actions

1. **Implement ACP headers on your transaction API**

   Follow the [ACP Integration Guide](../specs/acp-integration-v0.1.md). Key requirements:
   - Agent identity header (`X-Agent-Id`)
   - Transaction authorization header (`X-Agent-Auth`)
   - Idempotency key support
   - Machine-readable error responses

2. **Create an agent-accessible checkout flow**

   Your existing checkout flow is almost certainly designed for humans (HTML forms, redirects, CAPTCHA). Agents need:
   - A purely API-based order creation endpoint
   - Clear confirmation and receipt data in JSON
   - Status polling or webhook for async confirmation

3. **Define agent transaction policies**

   Document and enforce:
   - Maximum transaction amount an agent can authorize without human confirmation
   - Permitted product/service categories for autonomous purchase
   - Refund and cancellation APIs (agents need to undo purchases too)

4. **Add agent authentication**

   Agents must be identifiable. Implement:
   - API key issuance for agent clients
   - Rate limiting per agent identity
   - Audit log of all agent-initiated transactions

**Verification:** A test agent should be able to browse, select, and purchase a product or service end-to-end through API calls only — with no human-facing web interface involved.

---

## Phase 4 — Full Agent Commerce

**Goal:** Allow autonomous agents to discover, evaluate, negotiate, and transact directly with your agent infrastructure. (AAIO Level 4)

**Estimated effort:** 4–12 weeks

### Actions

1. **Deploy an A2A-compatible agent endpoint**

   Follow the [A2A Commerce Protocol Profile](../specs/a2a-commerce-v0.1.md). Your agent endpoint must support:
   - Capability advertisement (what your agent can do)
   - Task reception and processing
   - Structured result return
   - Agent-to-agent negotiation for pricing/terms (if applicable)

2. **Register with A2A agent directories** (when available)

   As A2A infrastructure matures, agent discovery directories will emerge. Ensure your agent endpoint is registered and its capabilities are correctly described.

3. **Implement agent session management**

   Multi-turn agent conversations require:
   - Session identifiers
   - State persistence across calls
   - Timeout and cleanup handling

4. **Test with buyer agents in a sandbox**

   Before production deployment, test with realistic buyer agent workloads:
   - Discovery → query → compare → purchase sequences
   - Negotiation sequences (if applicable)
   - Error and exception paths

**Verification:** An autonomous buyer agent — given only your domain name — should be able to discover your offerings, compare them against competitors, negotiate if needed, and complete a transaction without any human intervention.

---

## Getting an AAIO Audit

Not sure where to start? An AAIO Audit gives you:

- Your current AAIO Readiness Score (0–100)
- Gap analysis against Level 1–4 requirements
- Prioritized implementation plan specific to your tech stack
- Estimated effort per phase

**AAIO Audit — 990 EUR**  
Delivered by RAD Intelligence in 5 business days.

Contact: [dani@tekoalydani.com](mailto:dani@tekoalydani.com) | [tekoalydani.com](https://tekoalydani.com)

---

## Common Mistakes

| Mistake | Why it fails | What to do instead |
|---------|-------------|-------------------|
| Blocking all AI crawlers in robots.txt | Agents cannot discover you | Whitelist legitimate agent crawlers by name |
| CAPTCHA on all key endpoints | Agents cannot proceed | Add a separate, CAPTCHA-free API path |
| Pricing hidden behind login | Agents cannot compare | Expose at least baseline pricing publicly |
| Schema.org data incomplete | AI cites wrong information | Validate with Google Rich Results Test |
| Treating MCP as optional | You miss most agent traffic | Agents prefer MCP over scraping |
| Ignoring agent error responses | Agents fail silently | Return structured JSON errors with clear messages |

---

## Suomeksi / In Finnish

Tämä dokumentti on käytännönläheinen käyttöönotto-opas AAIO:n implementointiin.

**Neljä vaihetta:**

1. **Arviointi** — Selvitä nykyinen AAIO-tasosi ja tavoitetaso
2. **Löydettävyys (taso 1)** — `AGENTS.md`, robots.txt, schema.org — 1–3 päivässä
3. **Luettavuus (taso 2)** — Koneluettava API tai MCP-palvelin — 1–4 viikkoa
4. **Transaktiot (taso 3–4)** — Agenttimaksut ja A2A-integraatio — 2–20 viikkoa

Aloitussuositus: **AAIO Audit (990 EUR)** — RAD Intelligence tekee analyysin nykytilastasi ja antaa priorisoidun toimenpidesuunnitelman. [tekoalydani.com](https://tekoalydani.com)

Protokollakartta: [protocol-landscape.md](protocol-landscape.md)
