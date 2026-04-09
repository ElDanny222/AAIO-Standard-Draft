# SEO Foundations for AAIO v0.1

**Status:** Draft  
**Version:** 0.1.0  
**Date:** 2026-04-09  
**Authors:** [Tekoäly-Dani](https://tekoalydani.com)  
**License:** Apache 2.0  
**Parent Spec:** [AAIO Core Specification v0.1](aaio-core-v0.1.md)  

---

## Abstract

Search Engine Optimization (SEO) is the foundational layer in the AIO stack. Every subsequent optimization layer — AEO, GEO, AAIO — depends on a solid SEO foundation. This document defines the SEO requirements that must be in place before higher-level AI optimizations can succeed, and specifies how traditional SEO practices evolve when the target audience shifts from human searchers to AI agents.

---

## 1. Introduction

### 1.1 SEO in the AIO Stack

SEO is the foundational layer (Layer 1 in the AIO stack) — the base upon which all AI optimization is built. Without proper SEO:

- AI crawlers cannot discover your content (AEO fails)
- LLMs cannot index your data (GEO fails)
- Autonomous agents cannot find your business (AAIO fails)

```
┌─────────────────────────────────────────┐
│  AAIO  — Autonomous agent transactions  │
├─────────────────────────────────────────┤
│  GEO   — Appear in generated answers    │
├─────────────────────────────────────────┤
│  AEO   — Get cited by answer engines    │
├─────────────────────────────────────────┤
│  SEO   — Be crawlable and indexable     │  ◄── THIS LAYER
└─────────────────────────────────────────┘
```

### 1.2 Scope

This specification covers:

- Traditional SEO requirements that underpin AI optimization
- How SEO practices must evolve for AI-first discovery
- Technical SEO checklist aligned with AAIO readiness
- The boundary between SEO and AEO (where SEO ends and AEO begins)

### 1.3 SEO vs. AEO vs. GEO vs. AAIO

| Aspect | SEO | AEO | GEO | AAIO |
|--------|-----|-----|-----|------|
| **Primary audience** | Search engine crawlers + humans | AI answer engines | LLM-generated content | Autonomous AI agents |
| **Goal** | Rank in search results | Be cited as a source | Appear in generated responses | Enable agent discovery + transaction |
| **Key metric** | Rankings, organic traffic | Citation frequency | Inclusion rate | AAIO Readiness Score |
| **Content format** | Keywords, meta tags, links | Structured facts, Q&A | Comprehensive authority content | Machine-readable data + APIs |
| **Technical focus** | Crawlability, indexability | Schema.org, llms.txt | Topical authority, E-E-A-T | Agent manifest, protocol endpoints |

---

## 2. Core SEO Requirements for AAIO

These are the SEO fundamentals that MUST be in place before implementing higher AIO layers.

### 2.1 Crawlability

The ability of bots — both traditional search engines and AI crawlers — to access and read your content.

| Requirement | Priority | Description |
|-------------|----------|-------------|
| `robots.txt` | MUST | Well-structured, allowing both search engines and AI crawlers |
| Server-side rendering | MUST | Critical content available without JavaScript execution |
| Response time | MUST | TTFB < 500ms for content pages |
| HTTP status codes | MUST | Correct 200/301/404/410 (no soft 404s) |
| Crawl budget optimization | SHOULD | Prevent crawl waste on low-value pages |
| XML sitemap | MUST | Complete, valid, updated automatically |

#### 2.1.1 robots.txt for AI-Ready Sites

```
# Traditional search engines
User-agent: Googlebot
Allow: /

User-agent: Bingbot
Allow: /

# AI answer engines (AEO layer)
User-agent: GPTBot
Allow: /

User-agent: ClaudeBot
Allow: /

User-agent: PerplexityBot
Allow: /

User-agent: Google-Extended
Allow: /

# AI purchase agents (AAIO layer)
User-agent: AAIO-Agent
Allow: /

User-agent: MCP-Client
Allow: /

# Common disallows
User-agent: *
Disallow: /admin/
Disallow: /cart/
Disallow: /checkout/
Disallow: /account/

Sitemap: https://example.com/sitemap.xml
```

### 2.2 Indexability

Content must be indexable — search engines and AI systems must be able to store and retrieve it.

| Requirement | Priority | Description |
|-------------|----------|-------------|
| Canonical URLs | MUST | `rel="canonical"` on every page |
| Meta robots | MUST | Correct `index`/`noindex` directives |
| Hreflang | SHOULD | For multilingual sites |
| Pagination | MUST | `rel="next"` / `rel="prev"` for paginated content |
| Duplicate content elimination | MUST | One canonical URL per content entity |
| Mobile-first content | MUST | Same content served to mobile and desktop |

### 2.3 Site Architecture

| Requirement | Priority | Description |
|-------------|----------|-------------|
| Logical URL hierarchy | MUST | Predictable paths (e.g., `/products/category/item`) |
| Flat architecture | SHOULD | Important pages within 3 clicks from homepage |
| Internal linking | MUST | Contextual links between related content |
| Breadcrumb navigation | SHOULD | `BreadcrumbList` Schema.org markup |
| Category taxonomy | SHOULD | Machine-readable hierarchy |
| URL consistency | MUST | No trailing slash inconsistencies, lowercase URLs |

### 2.4 On-Page SEO

| Requirement | Priority | Description |
|-------------|----------|-------------|
| Unique title tags | MUST | Descriptive, under 60 characters |
| Meta descriptions | SHOULD | Compelling summaries, under 160 characters |
| Heading hierarchy | MUST | Single H1, logical H2–H6 structure |
| Image alt text | MUST | Descriptive alt attributes on all images |
| Structured data | MUST | Schema.org JSON-LD (see Section 3) |
| Content quality | MUST | E-E-A-T signals (Experience, Expertise, Authoritativeness, Trustworthiness) |

---

## 3. Structured Data Foundation

Structured data is where SEO transitions toward AEO and AAIO. It is the shared requirement across all AIO layers.

### 3.1 Required Schema.org Types

Every AAIO-aspiring site MUST implement these baseline Schema.org types:

#### 3.1.1 Organization

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Company Name",
  "url": "https://example.com",
  "logo": "https://example.com/logo.png",
  "description": "Clear, factual company description",
  "contactPoint": {
    "@type": "ContactPoint",
    "telephone": "+358-XX-XXX-XXXX",
    "contactType": "customer service",
    "availableLanguage": ["Finnish", "English"]
  },
  "sameAs": [
    "https://linkedin.com/company/example",
    "https://twitter.com/example"
  ]
}
```

#### 3.1.2 WebSite with SearchAction

```json
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "name": "Example Store",
  "url": "https://example.com",
  "potentialAction": {
    "@type": "SearchAction",
    "target": "https://example.com/search?q={search_term_string}",
    "query-input": "required name=search_term_string"
  }
}
```

#### 3.1.3 BreadcrumbList

```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": "https://example.com/"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "Products",
      "item": "https://example.com/products/"
    }
  ]
}
```

### 3.2 Industry-Specific Schema.org

| Industry | Required Types |
|----------|---------------|
| E-commerce | `Product`, `Offer`, `AggregateRating`, `Review` |
| SaaS | `SoftwareApplication`, `Offer`, `WebApplication` |
| Professional services | `Service`, `ProfessionalService`, `Person` (experts) |
| Local business | `LocalBusiness`, `PostalAddress`, `OpeningHoursSpecification` |
| Media / Publishing | `Article`, `TechArticle`, `NewsArticle`, `Person` (author) |

---

## 4. Technical SEO for AI Readiness

### 4.1 Performance

Site speed directly impacts both search engine rankings and AI crawler efficiency.

| Metric | Target | Why It Matters for AI |
|--------|--------|----------------------|
| TTFB | < 500ms | AI crawlers have timeout limits |
| LCP | < 2.5s | Core Web Vital for search ranking |
| CLS | < 0.1 | Layout stability for content extraction |
| FID/INP | < 200ms | Interaction readiness (less relevant for bots) |

### 4.2 Rendering

| Approach | SEO Impact | AI Impact | Recommendation |
|----------|-----------|-----------|----------------|
| Server-Side Rendering (SSR) | Best | Best | RECOMMENDED for all AAIO sites |
| Static Site Generation (SSG) | Best | Best | RECOMMENDED for content-heavy sites |
| Client-Side Rendering (CSR) | Poor | Worst | NOT RECOMMENDED — AI crawlers rarely execute JS |
| Pre-rendering | Good | Good | Acceptable fallback for SPA frameworks |

### 4.3 Core Web Vitals

Google's Core Web Vitals remain a ranking factor and correlate with crawl efficiency:

1. **Largest Contentful Paint (LCP)**: Measures loading performance. Target: < 2.5 seconds.
2. **Cumulative Layout Shift (CLS)**: Measures visual stability. Target: < 0.1.
3. **Interaction to Next Paint (INP)**: Measures interactivity. Target: < 200ms.

### 4.4 Security

| Requirement | Priority | Description |
|-------------|----------|-------------|
| HTTPS | MUST | TLS 1.2+ on all pages |
| HSTS | SHOULD | HTTP Strict Transport Security header |
| Content Security Policy | SHOULD | CSP headers to prevent injection |
| No mixed content | MUST | All resources loaded over HTTPS |

---

## 5. Content SEO Principles

### 5.1 E-E-A-T for AI

Google's E-E-A-T framework (Experience, Expertise, Authoritativeness, Trustworthiness) is critical for both search rankings and AI citation. AI answer engines heavily weight E-E-A-T signals when selecting sources.

| Signal | SEO Impact | AI Impact | How to Implement |
|--------|-----------|-----------|-----------------|
| **Experience** | Medium | High | First-hand examples, case studies, original data |
| **Expertise** | High | High | Author credentials, `Person` Schema.org, professional history |
| **Authoritativeness** | High | Critical | Industry citations, backlinks, recognized brand |
| **Trustworthiness** | High | Critical | Accurate data, transparent sourcing, HTTPS |

### 5.2 Content Architecture

| Practice | Description | AI Benefit |
|----------|-------------|------------|
| Topic clusters | Hub page + spoke pages around a core topic | Establishes topical authority for LLMs |
| Pillar content | Comprehensive, definitive pages on key topics | Preferred by AI for citation |
| FAQ integration | Q&A format with Schema.org FAQPage | Directly extractable by answer engines |
| Data tables | Structured comparison and data tables | Machine-parseable information |
| Clear definitions | "X is Y" format for key terms | Directly citable by LLMs |

### 5.3 Content Freshness

| Signal | Implementation |
|--------|---------------|
| `datePublished` in Schema.org | Set on initial publication |
| `dateModified` in Schema.org | Update when content changes |
| `Last-Modified` HTTP header | Set correctly on server |
| Sitemap `<lastmod>` | Accurate modification dates |
| Visible date on page | "Last updated: YYYY-MM-DD" |

---

## 6. SEO Measurement for AIO Readiness

### 6.1 Traditional SEO Metrics

| Metric | Tool | Target |
|--------|------|--------|
| Organic traffic | Google Analytics / Search Console | Growing month-over-month |
| Keyword rankings | SEMrush, Ahrefs, or equivalent | Top 10 for target terms |
| Crawl errors | Google Search Console | Zero critical errors |
| Index coverage | Google Search Console | 95%+ of intended pages indexed |
| Core Web Vitals | PageSpeed Insights | All metrics in "Good" range |
| Structured data validity | Rich Results Test | Zero errors |

### 6.2 AI-Ready SEO Metrics (Extended)

| Metric | Description | How to Measure |
|--------|-------------|----------------|
| AI crawler access rate | Frequency of GPTBot, ClaudeBot visits | Server log analysis |
| Schema.org coverage | % of pages with valid structured data | Automated audit tools |
| llms.txt completeness | Whether llms.txt exists and is comprehensive | Manual review |
| robots.txt AI coverage | Whether AI crawlers are explicitly addressed | Manual review |
| SSR coverage | % of pages with server-rendered content | Automated testing |

---

## 7. SEO Checklist for AAIO Readiness

### 7.1 Foundation (Required before any AIO work)

- [ ] HTTPS on all pages with valid TLS certificate
- [ ] `robots.txt` with explicit AI crawler directives
- [ ] XML sitemap at `/sitemap.xml`, auto-generated
- [ ] Canonical URLs on all pages
- [ ] Server-side rendering for all critical content
- [ ] Schema.org `Organization` and `WebSite` on homepage
- [ ] Unique title tags and meta descriptions on all pages
- [ ] Logical heading hierarchy (H1–H6)
- [ ] Image alt text on all images
- [ ] Core Web Vitals in "Good" range

### 7.2 Enhancement (Required for AEO/GEO readiness)

- [ ] Schema.org JSON-LD on all product/service pages
- [ ] `BreadcrumbList` markup on navigation pages
- [ ] `FAQPage` markup on FAQ/knowledge base pages
- [ ] `datePublished` and `dateModified` on all content
- [ ] Internal linking strategy with topic clusters
- [ ] `llms.txt` at site root
- [ ] `ai.txt` AI policy declaration
- [ ] Author `Person` markup with credentials

### 7.3 Advanced (Required for full AAIO stack)

- [ ] OpenAPI specification for site APIs
- [ ] `SearchAction` in WebSite Schema.org
- [ ] Product/service feeds in machine-readable format
- [ ] AAIO Agent Manifest at `/.well-known/aaio-manifest.json`
- [ ] A2A Agent Card at `/.well-known/agent.json`
- [ ] MCP-compatible tool descriptions

---

## 8. Common SEO Anti-Patterns That Break AI Optimization

| Anti-Pattern | Impact on AI | Solution |
|-------------|-------------|----------|
| JavaScript-only rendering | AI crawlers cannot read content | Server-side rendering |
| CAPTCHAs on content pages | Blocks all automated access | Agent-specific auth (API keys) |
| Infinite scroll without pagination | Crawlers miss content below fold | Paginated URLs with `rel` links |
| Dynamic URLs with session IDs | Duplicate content, crawl waste | Clean canonical URLs |
| Cloaking (different content for bots) | Trust destruction | Same content for all user-agents |
| Keyword stuffing | Reduces content quality signals | Natural, factual language |
| Thin doorway pages | Low authority, low trust | Comprehensive pillar content |
| Broken internal links | Navigation failures for agents | Regular link audits |
| Missing structured data | Invisible to AI extraction | Schema.org JSON-LD on all pages |
| Stale content | Reduced freshness signals | Regular content updates with `dateModified` |

---

## 9. Relationship to Higher AIO Layers

### 9.1 SEO → AEO Bridge

When SEO is solid, implementing AEO means:

1. Adding `FAQPage` and `HowTo` Schema.org markup
2. Creating `llms.txt` for LLM-readable site summary
3. Structuring content in Q&A format for answer extraction
4. Optimizing for citation (E-E-A-T signals)

### 9.2 SEO → GEO Bridge

When AEO foundations are in place, GEO requires:

1. Building topical authority through comprehensive content clusters
2. Creating definitive, data-rich pillar content
3. Establishing expert credibility through author markup
4. Publishing original research and statistics

### 9.3 SEO → AAIO Bridge

The full path from SEO to AAIO readiness:

```
SEO Foundation        →  Crawlable, indexable, structured
  + AEO Enhancement   →  Citable by answer engines
    + GEO Authority   →  Included in generated content
      + AAIO Commerce →  Agents can discover and transact
```

Each layer is cumulative. Skipping layers creates a fragile optimization that fails under AI agent scrutiny.

---

## Appendix A: References

- [Google Search Central](https://developers.google.com/search) — Official SEO documentation
- [Schema.org](https://schema.org/) — Structured data vocabulary
- [Web Vitals](https://web.dev/vitals/) — Core Web Vitals documentation
- [Google E-E-A-T Guidelines](https://developers.google.com/search/docs/fundamentals/creating-helpful-content) — Content quality framework
- [llms.txt Specification](https://llmstxt.org/) — LLM-readable site summaries
- [RFC 9110](https://www.rfc-editor.org/rfc/rfc9110) — HTTP Semantics
- [AAIO Core Specification](aaio-core-v0.1.md) — Core AAIO standard

---

*This document is part of the [AAIO Standard Draft](../README.md) project by [Tekoäly-Dani](https://tekoalydani.com).*
