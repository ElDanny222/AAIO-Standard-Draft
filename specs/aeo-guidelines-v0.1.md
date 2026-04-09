# AEO Best Practices v0.1

**Status:** Draft  
**Version:** 0.1.0  
**Date:** 2026-04-09  
**Authors:** Tekoaly-Dani / RAD Intelligence  
**License:** Apache 2.0  
**Parent Spec:** [AAIO Core Specification v0.1](aaio-core-v0.1.md)  

---

## Abstract

Answer Engine Optimization (AEO) is the practice of optimizing web content so that AI answer engines (ChatGPT, Perplexity, Gemini, Copilot) cite it as an authoritative source. AEO is the second layer in the AIO stack, building on SEO foundations and enabling the higher layers of GEO and AAIO.

This document provides actionable guidelines for achieving strong AEO performance.

---

## 1. Introduction

### 1.1 What Is AEO?

AEO optimizes content for a new class of search: **AI answer engines** that synthesize responses from multiple sources. Unlike traditional search engines that return links, answer engines return direct answers — and cite their sources. Being cited means traffic, authority, and trust.

### 1.2 Why AEO Matters

- **AI answer engines are growing**: ChatGPT, Perplexity, Gemini, and Copilot serve hundreds of millions of queries monthly
- **Citation = authority**: Being cited positions a brand as the definitive source on a topic
- **Foundation for AAIO**: AI purchase agents use the same knowledge sources — AEO visibility feeds directly into agent discovery

### 1.3 AEO vs. SEO vs. GEO

| Aspect | SEO | AEO | GEO |
|--------|-----|-----|-----|
| **Target** | Search engine crawlers | AI answer engines | AI-generated synthesized answers |
| **Goal** | Rank in search results | Be cited as a source | Appear in generated responses |
| **Content format** | Keywords, links, meta tags | Structured, factual, authoritative | Comprehensive, well-structured |
| **Measurement** | Rankings, CTR | Citation frequency | Inclusion in generated content |

---

## 2. Content Strategy for LLM Visibility

### 2.1 Core Principles

1. **Be the definitive source**: LLMs prefer content that is comprehensive, specific, and authoritative
2. **Answer questions directly**: Structure content around questions your audience asks
3. **State facts, not opinions**: LLMs cite factual, verifiable claims over subjective content
4. **Be current**: Freshness signals matter — regularly update content with current data
5. **Be specific**: Concrete numbers, dates, and examples are more citable than vague statements

### 2.2 Content Formats That LLMs Prefer

| Format | Why LLMs Prefer It | Example |
|--------|-------------------|---------|
| **Definition paragraphs** | Clear, citable answer to "what is X?" | "AAIO (Agentic AI Optimization) is an optimization layer that..." |
| **Comparison tables** | Structured, easy to extract | Feature comparison tables with clear headers |
| **Step-by-step lists** | Procedural knowledge is highly valued | "How to implement Schema.org: 1. Choose your markup type..." |
| **FAQ sections** | Direct question-answer mapping | Q&A pairs with Schema.org FAQPage markup |
| **Statistics with sources** | Verifiable data points | "The AI optimization market is worth $7.3B (2026, Gartner)" |
| **Expert quotes** | Authority signals | Named expert + credentials + quote |

### 2.3 Content Anti-Patterns

Avoid these patterns that reduce LLM citability:

- **Clickbait titles**: "You Won't Believe..." — LLMs don't click
- **Thin content**: Pages with fewer than 300 words of substantive content
- **Duplicate content**: Same information across multiple pages
- **Gated content**: LLM crawlers cannot log in — critical information behind paywalls is invisible
- **Image-only information**: Text in images is not extractable by most LLM crawlers
- **Dynamic-only content**: JavaScript-rendered content may not be crawled

---

## 3. Structured Data for AEO

### 3.1 Essential Schema.org Types

These Schema.org types directly support AEO by making content machine-parseable:

#### 3.1.1 FAQPage

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What is AAIO?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "AAIO (Agentic AI Optimization) is an optimization layer that defines how websites should be structured so that autonomous AI agents can discover, understand, navigate, and transact with them."
      }
    }
  ]
}
```

#### 3.1.2 Article / TechArticle

```json
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "headline": "AAIO Core Specification v0.1",
  "author": {
    "@type": "Organization",
    "name": "Tekoaly-Dani"
  },
  "datePublished": "2026-04-09",
  "dateModified": "2026-04-09",
  "description": "Technical specification for Agentic AI Optimization",
  "proficiencyLevel": "Expert"
}
```

#### 3.1.3 HowTo

```json
{
  "@context": "https://schema.org",
  "@type": "HowTo",
  "name": "How to Implement AAIO on Your E-Commerce Site",
  "step": [
    {
      "@type": "HowToStep",
      "name": "Add Schema.org markup",
      "text": "Add JSON-LD Product and Offer markup to all product pages"
    },
    {
      "@type": "HowToStep",
      "name": "Create llms.txt",
      "text": "Create an LLM-readable summary of your site at /llms.txt"
    }
  ]
}
```

#### 3.1.4 Organization with Expert Claims

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Tekoaly-Dani",
  "description": "Finnish AI optimization consultancy specializing in AAIO",
  "knowsAbout": ["AAIO", "AEO", "GEO", "AI Optimization", "Agent Commerce"],
  "founder": {
    "@type": "Person",
    "name": "Dani Forsberg",
    "jobTitle": "Head of AI Strategy"
  }
}
```

### 3.2 Schema.org Validation

- Validate all markup using [Google Rich Results Test](https://search.google.com/test/rich-results)
- Ensure no errors or warnings in structured data
- Test that all required fields are populated
- Verify JSON-LD is present in the page source (not just dynamically rendered)

---

## 4. Technical AEO Requirements

### 4.1 Crawlability for AI Agents

| Requirement | Implementation |
|-------------|----------------|
| Allow AI crawlers in `robots.txt` | `User-agent: GPTBot`, `User-agent: ClaudeBot`, etc. with appropriate `Allow` rules |
| Serve static HTML | Server-side rendering or pre-rendering for critical content |
| Fast response times | Target < 500ms TTFB for content pages |
| `llms.txt` | LLM-readable site summary following [llmstxt.org](https://llmstxt.org/) specification |
| `ai.txt` | AI policy declaration stating permitted AI usage |
| Canonical URLs | `rel="canonical"` on all content pages |

### 4.2 llms.txt Structure

The `llms.txt` file SHOULD contain:

```markdown
# Site Name

> Brief site description (1-2 sentences)

## Key Topics
- Topic 1: Brief description
- Topic 2: Brief description

## Important Pages
- [Page Title](URL): Description
- [Page Title](URL): Description

## Contact
- Name, role, email
```

### 4.3 Content Freshness Signals

LLMs consider freshness when selecting sources:

1. **`dateModified` in Schema.org**: Update this when content changes
2. **Last-Modified HTTP header**: Set correctly for all content pages
3. **Sitemap `<lastmod>`**: Accurate modification dates in sitemap
4. **Visible dates on page**: "Last updated: YYYY-MM-DD" in visible content

---

## 5. AEO Measurement

### 5.1 Key Metrics

| Metric | Description | How to Measure |
|--------|-------------|----------------|
| **Citation frequency** | How often your content is cited by AI engines | Monitor brand mentions in ChatGPT, Perplexity, Gemini responses |
| **Citation accuracy** | Whether cited information is correct | Verify AI-generated citations match your content |
| **Source authority** | Your site's perceived authority in AI models | Track citation ranking vs. competitors |
| **Crawler access rate** | How often AI crawlers visit | Analyze server logs for AI agent user-agents |
| **Structured data coverage** | % of pages with valid Schema.org | Automated Schema.org validation |

### 5.2 Monitoring Tools

- **Server log analysis**: Track GPTBot, ClaudeBot, PerplexityBot visits
- **Brand monitoring**: Search your brand/domain in AI answer engines
- **Schema.org validators**: Automated weekly validation
- **Content freshness audits**: Track `dateModified` accuracy

---

## 6. AEO Checklist

### 6.1 Quick Start (Achievable in 1 Week)

- [ ] Audit and update `robots.txt` for AI crawlers
- [ ] Add Schema.org `Organization` and `WebSite` JSON-LD to homepage
- [ ] Create `llms.txt` with site summary
- [ ] Ensure all key pages have `dateModified` in Schema.org
- [ ] Add `FAQPage` markup to FAQ/knowledge base pages

### 6.2 Foundation (Achievable in 1 Month)

- [ ] Add Schema.org markup to all product/service pages
- [ ] Create comprehensive FAQ content for top 20 questions in your domain
- [ ] Implement server-side rendering for critical content pages
- [ ] Set up AI crawler monitoring in server logs
- [ ] Create `ai.txt` with AI usage policy

### 6.3 Advanced (Ongoing)

- [ ] Establish content update cadence (monthly minimum for key pages)
- [ ] Build topical authority: create comprehensive content clusters
- [ ] Monitor citation frequency across major AI answer engines
- [ ] A/B test content formats for citability
- [ ] Contribute to industry standards and get cited by other authorities

---

## 7. Industry-Specific Guidelines

### 7.1 E-Commerce

- Add `Product`, `Offer`, and `AggregateRating` to all product pages
- Include comparison tables for product categories
- Publish buying guides with structured data
- Ensure pricing is always current in structured data

### 7.2 SaaS / Technology

- Add `SoftwareApplication` Schema.org to product pages
- Create detailed feature comparison pages
- Document API endpoints with OpenAPI specification
- Publish technical documentation with `TechArticle` markup

### 7.3 Professional Services

- Add `Service` and `ProfessionalService` markup
- Create case studies with measurable results
- Publish expert content with `Person` author markup
- Include pricing/rate information in structured data

### 7.4 Local Business

- Add `LocalBusiness` markup with accurate NAP (Name, Address, Phone)
- Publish service area information in structured data
- Include operating hours in Schema.org
- Create location-specific content pages

---

## Appendix A: AI Answer Engine Crawler Reference

| Engine | User-Agent | Documentation |
|--------|------------|---------------|
| OpenAI / ChatGPT | `GPTBot` | [OpenAI GPTBot](https://platform.openai.com/docs/gptbot) |
| Anthropic / Claude | `ClaudeBot` | [Anthropic ClaudeBot](https://docs.anthropic.com/en/docs/claude-bot) |
| Google / Gemini | `Google-Extended` | [Google AI Crawler](https://developers.google.com/search/docs/crawling-indexing/overview-google-crawlers) |
| Perplexity | `PerplexityBot` | [Perplexity Bot](https://docs.perplexity.ai/guides/perplexity-bot) |
| Apple | `Applebot-Extended` | [Apple Bot](https://support.apple.com/en-us/111867) |

---

*This document is part of the [AAIO Standard Draft](../README.md) project by [Tekoaly-Dani](https://tekoalydani.com).*
