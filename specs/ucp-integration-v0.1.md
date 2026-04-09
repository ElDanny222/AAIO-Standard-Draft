# Universal Commerce Protocol (UCP) Integration Specification

**Version:** 0.1-draft  
**Status:** Draft  
**Date:** 2026-04-09  
**Authors:** Tekoaly-Dani AAIO Working Group  

---

## Abstract

This document specifies how Agentic AI Optimization (AAIO)-compliant websites
implement the Universal Commerce Protocol (UCP) to expose product and service
data in a standardized, machine-readable format. UCP, originating from
Google/Shopify commerce infrastructure, provides a unified data layer that
AI agents can consume for discovery, comparison, and purchasing decisions.

This specification does not define a new protocol. It profiles the existing
UCP framework within the AAIO optimization layer, prescribing how commerce
platforms structure and serve product/service data so that autonomous agents
can efficiently parse, compare, and act on catalog information.

## Status of This Document

This is a draft specification (v0.1) published for community review. It is
not yet suitable for production implementation without additional validation.
Feedback should be directed to the AAIO-Standard-Draft repository.

## Table of Contents

1. [Terminology](#1-terminology)
2. [Overview](#2-overview)
3. [Data Model](#3-data-model)
4. [API Specification](#4-api-specification)
5. [Schema Mappings](#5-schema-mappings)
6. [AAIO Integration Requirements](#6-aaio-integration-requirements)
7. [Error Handling](#7-error-handling)
8. [Security Considerations](#8-security-considerations)
9. [Conformance](#9-conformance)
10. [References](#10-references)

---

## 1. Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

| Term | Definition |
|------|------------|
| **UCP** | Universal Commerce Protocol — a standardized data interchange format for product and service information across commerce platforms (Google/Shopify ecosystem). |
| **AAIO** | Agentic AI Optimization — the optimization layer ensuring websites are discoverable, understandable, and transactable by autonomous AI agents. |
| **Catalog Agent** | An AI agent that crawls, indexes, and compares product/service offerings across multiple UCP-compliant sources. |
| **Merchant Feed** | A structured data export from a merchant's catalog in UCP format. |
| **Product Entity** | A normalized product representation conforming to the AAIO product schema. |
| **Service Entity** | A normalized service representation conforming to the AAIO service schema. |
| **Schema Mapping** | A defined transformation from a platform-specific data format (Shopify, WooCommerce, etc.) to the AAIO canonical schema. |

## 2. Overview

### 2.1 Problem Statement

AI agents comparing products across multiple vendors face a fragmentation
problem: each e-commerce platform uses its own data model, attribute naming
conventions, and API structure. An agent evaluating a laptop must normalize
"RAM", "Memory", "memory_gb", and "ram_size" across different sources. UCP
integration within AAIO solves this by mandating a canonical data format.

### 2.2 Architecture

```
┌─────────────────┐     ┌───────────────────┐     ┌──────────────────┐
│ Commerce Platform│     │  UCP Transform    │     │  AAIO Endpoint   │
│ (Shopify, etc.) │────>│  Layer            │────>│  /ucp/v0.1/      │
│ Native data     │     │  Schema mapping   │     │  Canonical data  │
└─────────────────┘     └───────────────────┘     └──────┬───────────┘
                                                         │
                                                         ▼
                                                  ┌──────────────┐
                                                  │ Catalog Agent│
                                                  │ (AI agent)   │
                                                  └──────────────┘
```

### 2.3 Relationship to AAIO

UCP is the data layer of the AAIO protocol stack:

- **UCP** (this document) — Standardized product/service data
- **ACP** — Payment execution via Stripe
- **A2A** — Agent-to-agent negotiation

UCP provides the data that agents consume before initiating ACP transactions
or A2A negotiations.

## 3. Data Model

### 3.1 Product Entity

Products MUST conform to the `aaio-product.schema.json` schema. The canonical
product representation includes:

```json
{
  "aaio_schema": "aaio-product/v0.1",
  "id": "prod_widget_pro_2026",
  "gtin": "0614141000036",
  "name": "Widget Pro 2026",
  "description": "Professional-grade widget with AI integration",
  "category": {
    "primary": "electronics/widgets",
    "google_product_category": 1234,
    "custom_labels": ["ai-compatible", "professional"]
  },
  "brand": {
    "name": "WidgetCorp",
    "url": "https://widgetcorp.example.com"
  },
  "pricing": {
    "currency": "EUR",
    "amount": 4999,
    "amount_decimal": "49.99",
    "tax_included": true,
    "bulk_pricing": [
      {"min_quantity": 10, "amount": 4499},
      {"min_quantity": 100, "amount": 3999}
    ]
  },
  "availability": {
    "status": "in_stock",
    "quantity": 342,
    "lead_time_days": 1,
    "backorder_allowed": true
  },
  "attributes": {
    "weight_g": 250,
    "dimensions_mm": {"length": 150, "width": 80, "height": 20},
    "color": "midnight_blue",
    "material": "aluminum"
  },
  "agent_metadata": {
    "comparison_attributes": ["weight_g", "dimensions_mm", "color"],
    "decision_factors": ["pricing.amount", "availability.status", "attributes.material"],
    "alternatives": ["prod_widget_standard_2026", "prod_widget_lite_2026"]
  }
}
```

### 3.2 Service Entity

Services MUST conform to the `aaio-service.schema.json` schema:

```json
{
  "aaio_schema": "aaio-service/v0.1",
  "id": "svc_aaio_audit",
  "name": "AAIO Readiness Audit",
  "description": "Comprehensive audit of website readiness for autonomous AI agents",
  "category": {
    "primary": "consulting/ai-optimization",
    "custom_labels": ["aaio", "audit", "ai-readiness"]
  },
  "provider": {
    "name": "Tekoaly-Dani",
    "url": "https://tekoalydani.com"
  },
  "pricing": {
    "model": "fixed",
    "currency": "EUR",
    "amount": 299900,
    "amount_decimal": "2999.00",
    "billing_period": null,
    "tiers": [
      {"name": "basic", "amount": 99900, "features": ["core_audit", "report"]},
      {"name": "professional", "amount": 299900, "features": ["core_audit", "report", "implementation_guide", "follow_up"]},
      {"name": "enterprise", "amount": null, "features": ["everything", "custom_integration", "dedicated_support"], "contact_required": true}
    ]
  },
  "delivery": {
    "model": "project",
    "estimated_duration_days": 14,
    "regions": ["FI", "SE", "NO", "DK", "EE"],
    "remote_available": true
  },
  "availability": {
    "status": "available",
    "next_available_date": "2026-04-15",
    "booking_url": "/acp/v0.1/transactions"
  },
  "agent_metadata": {
    "comparison_attributes": ["pricing.amount", "delivery.estimated_duration_days"],
    "decision_factors": ["pricing.tiers", "delivery.regions", "availability.status"],
    "qualification_questions": [
      "What is the site's current monthly traffic?",
      "Does the site have an existing structured data implementation?",
      "What commerce platform is in use?"
    ]
  }
}
```

### 3.3 Common Fields

All UCP entities share these base fields:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `aaio_schema` | String | REQUIRED | Schema identifier and version (e.g., `"aaio-product/v0.1"`). |
| `id` | String | REQUIRED | Merchant-unique stable identifier. |
| `name` | String | REQUIRED | Human and agent-readable name. |
| `description` | String | REQUIRED | Plain-text description (no HTML). |
| `category` | Object | REQUIRED | Categorization with `primary` field. |
| `pricing` | Object | REQUIRED | Pricing information. |
| `availability` | Object | REQUIRED | Current availability status. |
| `agent_metadata` | Object | RECOMMENDED | Agent-specific optimization hints. |

## 4. API Specification

### 4.1 Endpoints

UCP data is served via a RESTful API:

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/ucp/v0.1/products` | GET | List products with pagination and filtering. |
| `/ucp/v0.1/products/{id}` | GET | Get a single product by ID. |
| `/ucp/v0.1/services` | GET | List services with pagination and filtering. |
| `/ucp/v0.1/services/{id}` | GET | Get a single service by ID. |
| `/ucp/v0.1/categories` | GET | List available categories. |
| `/ucp/v0.1/search` | GET | Full-text search across products and services. |
| `/ucp/v0.1/feed` | GET | Bulk export in NDJSON format. |

### 4.2 Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `page` | Integer | Page number (1-indexed). Default: 1. |
| `per_page` | Integer | Items per page. Default: 50. Max: 200. |
| `category` | String | Filter by primary category path. |
| `min_price` | Integer | Minimum price in smallest currency unit. |
| `max_price` | Integer | Maximum price in smallest currency unit. |
| `currency` | String | ISO 4217 currency code. |
| `availability` | Enum | `in_stock`, `preorder`, `backorder`, `out_of_stock`. |
| `sort` | String | Sort field. Options: `price`, `name`, `updated_at`, `relevance`. |
| `order` | Enum | `asc` or `desc`. Default: `asc`. |
| `q` | String | Search query (for `/search` endpoint). |
| `updated_since` | ISO 8601 | Return items modified after this timestamp. |
| `fields` | String | Comma-separated list of fields to include (sparse fieldset). |

### 4.3 Pagination

Responses use cursor-based pagination:

```json
{
  "data": [...],
  "pagination": {
    "total": 1523,
    "page": 1,
    "per_page": 50,
    "total_pages": 31,
    "next_cursor": "eyJpZCI6InByb2RfMDUwIn0=",
    "next_url": "/ucp/v0.1/products?cursor=eyJpZCI6InByb2RfMDUwIn0="
  }
}
```

### 4.4 Bulk Feed

The `/ucp/v0.1/feed` endpoint serves the complete catalog in
Newline-Delimited JSON (NDJSON) format for efficient bulk ingestion:

```
Content-Type: application/x-ndjson

{"aaio_schema":"aaio-product/v0.1","id":"prod_001","name":"Widget A",...}
{"aaio_schema":"aaio-product/v0.1","id":"prod_002","name":"Widget B",...}
{"aaio_schema":"aaio-service/v0.1","id":"svc_001","name":"Consulting",...}
```

Feed parameters:
- `type`: Filter by entity type (`product`, `service`, `all`). Default: `all`.
- `updated_since`: Incremental feed since timestamp.

### 4.5 Content Negotiation

- Default: `application/json`
- Bulk feed: `application/x-ndjson`
- Agents SHOULD send `Accept: application/json` or `Accept: application/x-ndjson`.

## 5. Schema Mappings

### 5.1 Shopify Mapping

| Shopify Field | UCP/AAIO Field |
|---------------|----------------|
| `product.id` | `id` (prefixed with `shopify_`) |
| `product.title` | `name` |
| `product.body_html` | `description` (stripped of HTML) |
| `product.product_type` | `category.primary` |
| `product.vendor` | `brand.name` |
| `variant.price` | `pricing.amount_decimal` |
| `variant.sku` | `attributes.sku` |
| `variant.barcode` | `gtin` |
| `variant.inventory_quantity` | `availability.quantity` |
| `variant.weight` | `attributes.weight_g` (converted) |

### 5.2 WooCommerce Mapping

| WooCommerce Field | UCP/AAIO Field |
|-------------------|----------------|
| `product.id` | `id` (prefixed with `woo_`) |
| `product.name` | `name` |
| `product.description` | `description` (stripped of HTML) |
| `product.categories[].name` | `category.primary` (joined path) |
| `product.price` | `pricing.amount_decimal` |
| `product.sku` | `attributes.sku` |
| `product.stock_quantity` | `availability.quantity` |
| `product.stock_status` | `availability.status` (mapped) |
| `product.weight` | `attributes.weight_g` (converted) |
| `product.dimensions` | `attributes.dimensions_mm` (converted) |

### 5.3 Google Merchant Center Mapping

| Google MC Field | UCP/AAIO Field |
|-----------------|----------------|
| `offerId` | `id` |
| `title` | `name` |
| `description` | `description` |
| `googleProductCategory` | `category.google_product_category` |
| `brand` | `brand.name` |
| `price.value` | `pricing.amount_decimal` |
| `price.currency` | `pricing.currency` |
| `gtin` | `gtin` |
| `availability` | `availability.status` (mapped) |
| `shippingWeight` | `attributes.weight_g` (converted) |

### 5.4 Custom Mapping Extension

For platforms not listed above, merchants MAY provide a custom mapping
definition in their AAIO manifest:

```json
{
  "protocols": {
    "ucp": {
      "schema_mapping": {
        "source_format": "custom_erp_v3",
        "mapping_url": "/ucp/v0.1/mapping-definition.json"
      }
    }
  }
}
```

## 6. AAIO Integration Requirements

### 6.1 Discovery

AAIO-compliant merchants MUST advertise UCP support in their AAIO manifest
(`/.well-known/aaio-manifest.json`):

```json
{
  "aaioVersion": "0.1",
  "protocols": {
    "ucp": {
      "version": "0.1",
      "catalog_endpoint": "/ucp/v0.1/products",
      "service_endpoint": "/ucp/v0.1/services",
      "feed_endpoint": "/ucp/v0.1/feed",
      "search_endpoint": "/ucp/v0.1/search",
      "total_products": 1523,
      "total_services": 12,
      "supported_currencies": ["eur", "usd"],
      "default_locale": "fi-FI",
      "update_frequency": "hourly"
    }
  }
}
```

### 6.2 Schema Compliance

All product entities returned by UCP endpoints MUST validate against
`aaio-product.schema.json`. All service entities MUST validate against
`aaio-service.schema.json`.

Merchants SHOULD include the `agent_metadata` section to optimize
agent decision-making.

### 6.3 Freshness

- UCP endpoints MUST return data that is no more than 1 hour stale.
- Pricing and availability changes MUST be reflected within 15 minutes.
- The `updated_since` parameter MUST be supported for incremental sync.

### 6.4 Cross-Protocol References

UCP entities that are purchasable via ACP SHOULD include a reference to
the ACP transaction endpoint:

```json
{
  "id": "prod_widget_pro_2026",
  "acp_reference": {
    "endpoint": "/acp/v0.1/transactions",
    "purchasable": true,
    "requires_quote": false
  }
}
```

## 7. Error Handling

### 7.1 Error Response Format

```json
{
  "error": {
    "code": "UCP_ITEM_NOT_FOUND",
    "message": "Product with ID 'prod_nonexistent' was not found",
    "details": {
      "requested_id": "prod_nonexistent",
      "suggestion": "Use /ucp/v0.1/search?q=widget to find similar products"
    }
  }
}
```

### 7.2 Error Codes

| Code | HTTP Status | Description |
|------|-------------|-------------|
| `UCP_INVALID_PARAMETER` | 400 | Invalid query parameter value. |
| `UCP_UNAUTHORIZED` | 401 | Authentication required or token invalid. |
| `UCP_RATE_LIMITED` | 429 | Agent has exceeded request rate limits. |
| `UCP_ITEM_NOT_FOUND` | 404 | Requested product or service not found. |
| `UCP_FEED_UNAVAILABLE` | 503 | Bulk feed temporarily unavailable. |
| `UCP_SCHEMA_ERROR` | 500 | Internal schema mapping failure. |

## 8. Security Considerations

### 8.1 Authentication

UCP endpoints MAY be publicly accessible for product discovery. However:

- Bulk feed endpoints (`/ucp/v0.1/feed`) SHOULD require authentication
  to prevent scraping abuse.
- Rate limiting MUST be applied per agent identifier or IP address.
- RECOMMENDED rate limits: 1000 requests/hour for catalog endpoints,
  10 requests/hour for bulk feed.

### 8.2 Data Privacy

- UCP responses MUST NOT contain personally identifiable information (PII).
- Customer reviews, if included, MUST be aggregated (scores only), not
  individual.
- Pricing data MAY be personalized (e.g., B2B pricing) but only for
  authenticated agents with appropriate authorization.

### 8.3 Transport Security

- All UCP endpoints MUST be served over HTTPS (TLS 1.2+).
- Bulk feed downloads SHOULD support `Accept-Encoding: gzip` for
  bandwidth efficiency.

### 8.4 Competitive Sensitivity

Merchants SHOULD consider that UCP data is designed for agent consumption
and may be aggregated across competitors. Sensitive competitive data
(cost prices, supplier information) MUST NOT be included in UCP responses.

## 9. Conformance

An implementation is conformant with this specification if it:

1. Serves product data conforming to `aaio-product.schema.json` (Section 3.1).
2. Serves service data conforming to `aaio-service.schema.json` (Section 3.2).
3. Implements at minimum the list and get endpoints (Section 4.1).
4. Supports pagination (Section 4.3).
5. Advertises UCP support in the AAIO manifest (Section 6.1).
6. Meets freshness requirements (Section 6.3).
7. Implements error codes defined in Section 7.2.
8. Meets security requirements in Section 8.

## 10. References

### Normative References

- [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) — Key words for use in RFCs
- [RFC 8259](https://www.rfc-editor.org/rfc/rfc8259) — JSON Data Interchange Format
- [JSON Schema](https://json-schema.org/specification) — JSON Schema Specification
- [NDJSON](https://github.com/ndjson/ndjson-spec) — Newline Delimited JSON
- [Google Merchant Center](https://developers.google.com/shopping-content/reference/rest) — Content API for Shopping
- [Shopify Admin API](https://shopify.dev/docs/api/admin-rest) — REST Admin API
- [AAIO Core Specification](aaio-core-v0.1.md) — Agentic AI Optimization Core
- [AAIO Product Schema](../schemas/aaio-product.schema.json) — Product Data Schema
- [AAIO Service Schema](../schemas/aaio-service.schema.json) — Service Data Schema

### Informative References

- [ACP Integration Specification](acp-integration-v0.1.md) — Agent Commerce Protocol
- [A2A Commerce Protocol Profile](a2a-commerce-v0.1.md) — Agent-to-Agent Commerce
- [Schema.org Product](https://schema.org/Product) — Schema.org Product type
- [Schema.org Service](https://schema.org/Service) — Schema.org Service type

---

*Copyright 2026 Tekoaly-Dani. Licensed under Apache 2.0.*
