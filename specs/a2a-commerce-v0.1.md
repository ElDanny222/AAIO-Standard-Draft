# A2A Commerce Protocol Profile

**Version:** 0.1-draft  
**Status:** Draft  
**Date:** 2026-04-09  
**Authors:** Tekoäly-Dani AAIO Working Group  

---

## Abstract

This document defines a commerce profile for the Agent-to-Agent (A2A)
protocol (Linux Foundation, v1.0). It specifies how buyer and seller agents
use the A2A protocol to discover each other, negotiate terms, execute
purchases, and manage post-transaction workflows. The profile layers
commerce-specific conventions — Agent Card extensions, negotiation task
flows, and artifact schemas — onto the base A2A specification.

This specification does not modify the A2A protocol. It defines a
constrained usage profile within the AAIO optimization layer, ensuring
interoperability between autonomous commerce agents built on different
platforms.

## Status of This Document

This is a draft specification (v0.1) published for community review. It is
not yet suitable for production implementation without additional validation.
Feedback should be directed to the AAIO-Standard-Draft repository.

## Table of Contents

1. [Terminology](#1-terminology)
2. [Overview](#2-overview)
3. [Agent Card for Commerce](#3-agent-card-for-commerce)
4. [Negotiation Protocol](#4-negotiation-protocol)
5. [Task Lifecycle for Commerce](#5-task-lifecycle-for-commerce)
6. [Message and Artifact Schemas](#6-message-and-artifact-schemas)
7. [Multi-Turn Negotiation](#7-multi-turn-negotiation)
8. [AAIO Integration Requirements](#8-aaio-integration-requirements)
9. [Security Considerations](#9-security-considerations)
10. [Conformance](#10-conformance)
11. [References](#11-references)

---

## 1. Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

| Term | Definition |
|------|------------|
| **A2A** | Agent-to-Agent protocol — Linux Foundation's open standard for agent interoperability (v1.0). |
| **AAIO** | Agentic AI Optimization — the optimization layer for autonomous AI agent interactions with websites. |
| **Buyer Agent** | An AI agent acting on behalf of a human or organization to procure goods or services. |
| **Seller Agent** | An AI agent representing a merchant, capable of providing quotes, negotiating terms, and processing orders. |
| **AgentCard** | A2A's public metadata document (`.well-known/agent.json`) describing agent capabilities, extended here for commerce. |
| **Negotiation Session** | A `context_id`-grouped sequence of A2A tasks representing a multi-turn commerce negotiation. |
| **Commerce Artifact** | A task artifact containing structured commerce data (quote, order, invoice). |
| **RFQ** | Request for Quote — an initial buyer message requesting pricing and terms. |

## 2. Overview

### 2.1 Problem Statement

The A2A protocol provides general-purpose agent-to-agent communication:
task creation, message exchange, and artifact delivery. However, commerce
interactions require specific conventions: how does a buyer agent discover
that a seller agent offers products? How are prices negotiated? How does an
order confirmation artifact look? Without a commerce profile, each
implementation invents its own conventions, breaking interoperability.

### 2.2 Architecture

```
┌────────────────┐                                ┌────────────────┐
│  Buyer Agent   │                                │  Seller Agent  │
│  (AI agent)    │                                │  (AI agent)    │
│                │   A2A Protocol (HTTP+JSON)     │                │
│  Discovers via │───────────────────────────────>│  Exposes       │
│  AgentCard     │   SendMessage (RFQ)            │  AgentCard     │
│                │<───────────────────────────────│  at .well-known│
│  Evaluates     │   Task artifact (Quote)        │                │
│  quote         │───────────────────────────────>│  Processes     │
│                │   SendMessage (PurchaseOrder)  │  order         │
│  Receives      │<───────────────────────────────│                │
│  confirmation  │   Task artifact (Confirmation) │  Triggers ACP  │
└────────────────┘                                └────────────────┘
         │                                                │
         │              ┌──────────────┐                  │
         └─────────────>│  ACP Payment │<─────────────────┘
                        │  (Stripe)    │
                        └──────────────┘
```

### 2.3 Relationship to A2A Base Specification

This profile uses the following A2A v1.0 primitives:

| A2A Primitive | Commerce Usage |
|---------------|----------------|
| `SendMessage` | Buyer sends RFQ, purchase order; seller sends quotes, confirmations. |
| `GetTask` | Check status of an order or negotiation. |
| `SubscribeToTask` | Real-time updates on order processing. |
| `context_id` | Groups all messages in a negotiation session. |
| `artifacts` | Carry structured commerce data (quotes, orders, invoices). |
| `AgentCard` | Advertises commerce capabilities and supported product categories. |
| `AgentExtension` | Declares the `aaio-commerce` extension. |

## 3. Agent Card for Commerce

### 3.1 Seller Agent Card

A seller agent's AgentCard MUST include the `aaio-commerce` extension and
at least one commerce-related skill:

```json
{
  "name": "ShopBot",
  "description": "AI sales agent for WidgetCorp — handles product inquiries, quotes, and orders",
  "url": "https://shop.example.com/.well-known/agent.json",
  "version": "1.0.0",
  "capabilities": {
    "streaming": true,
    "pushNotifications": true
  },
  "skills": [
    {
      "id": "product-catalog",
      "name": "Product Catalog",
      "description": "Browse and search product catalog",
      "tags": ["commerce", "catalog", "search"],
      "examples": [
        "Show me all widgets under 50 EUR",
        "What professional-grade widgets do you have?"
      ]
    },
    {
      "id": "quote",
      "name": "Request Quote",
      "description": "Get pricing and availability for specific products",
      "tags": ["commerce", "quote", "pricing"],
      "examples": [
        "Quote for 100 units of Widget Pro",
        "What's the bulk pricing for Widget Pro?"
      ]
    },
    {
      "id": "purchase",
      "name": "Place Order",
      "description": "Execute a purchase order with payment via ACP",
      "tags": ["commerce", "purchase", "order"],
      "examples": [
        "Order 50 units of Widget Pro, shipping to Helsinki",
        "Purchase with PO number PO-2026-001"
      ]
    },
    {
      "id": "order-status",
      "name": "Order Status",
      "description": "Check the status of an existing order",
      "tags": ["commerce", "status", "tracking"],
      "examples": [
        "What's the status of order ORD-12345?",
        "Track my shipment"
      ]
    }
  ],
  "defaultInputModes": ["application/json", "text/plain"],
  "defaultOutputModes": ["application/json", "text/plain"],
  "security": [
    {
      "type": "oauth2",
      "flows": {
        "clientCredentials": {
          "tokenUrl": "https://shop.example.com/oauth/token",
          "scopes": {
            "catalog:read": "Browse product catalog",
            "quote:create": "Request price quotes",
            "order:create": "Place purchase orders",
            "order:read": "Check order status"
          }
        }
      }
    }
  ],
  "extensions": {
    "aaio-commerce": {
      "version": "0.1",
      "role": "seller",
      "supported_protocols": ["acp", "ucp"],
      "categories": ["electronics/widgets", "electronics/accessories"],
      "currencies": ["eur", "usd"],
      "regions": ["FI", "SE", "NO", "DK", "EE", "DE"],
      "ucp_endpoint": "/ucp/v0.1/products",
      "acp_endpoint": "/acp/v0.1/transactions"
    }
  }
}
```

### 3.2 Buyer Agent Card

A buyer agent's AgentCard advertises purchasing capabilities:

```json
{
  "name": "ProcureBot",
  "description": "AI procurement agent — finds, compares, and purchases products on behalf of clients",
  "url": "https://buyer.example.com/.well-known/agent.json",
  "skills": [
    {
      "id": "sourcing",
      "name": "Product Sourcing",
      "description": "Find and compare products across multiple sellers",
      "tags": ["commerce", "sourcing", "comparison"]
    },
    {
      "id": "negotiation",
      "name": "Price Negotiation",
      "description": "Negotiate pricing and terms with seller agents",
      "tags": ["commerce", "negotiation", "pricing"]
    }
  ],
  "extensions": {
    "aaio-commerce": {
      "version": "0.1",
      "role": "buyer",
      "max_budget": {
        "currency": "EUR",
        "amount": 1000000
      },
      "preferred_payment": "acp"
    }
  }
}
```

### 3.3 Extension Schema

The `aaio-commerce` extension fields:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `version` | String | REQUIRED | Commerce profile version (e.g., `"0.1"`). |
| `role` | Enum | REQUIRED | `"buyer"` or `"seller"`. |
| `supported_protocols` | Array | REQUIRED (seller) | Payment/data protocols: `["acp", "ucp"]`. |
| `categories` | Array | RECOMMENDED (seller) | Product/service categories offered. |
| `currencies` | Array | REQUIRED (seller) | Supported currencies (ISO 4217). |
| `regions` | Array | RECOMMENDED | Geographic regions served/operating in (ISO 3166-1). |
| `ucp_endpoint` | String | RECOMMENDED (seller) | Path to UCP catalog endpoint. |
| `acp_endpoint` | String | RECOMMENDED (seller) | Path to ACP transaction endpoint. |
| `max_budget` | Object | OPTIONAL (buyer) | Maximum transaction budget. |
| `preferred_payment` | String | OPTIONAL (buyer) | Preferred payment protocol. |

## 4. Negotiation Protocol

### 4.1 Message Types

Commerce A2A messages use structured JSON parts with the MIME type
`application/vnd.aaio.commerce.v0.1+json`. The message `type` field
determines the commerce action:

| Type | Direction | Description |
|------|-----------|-------------|
| `rfq` | Buyer → Seller | Request for Quote — specify items and desired terms. |
| `quote` | Seller → Buyer | Price quote with terms, validity, and conditions. |
| `counter_offer` | Either → Either | Modified terms in response to a quote/offer. |
| `purchase_order` | Buyer → Seller | Confirmed order with payment details. |
| `order_confirmation` | Seller → Buyer | Accepted order with fulfillment details. |
| `order_rejection` | Seller → Buyer | Rejected order with reason. |
| `invoice` | Seller → Buyer | Payment invoice for the transaction. |
| `shipping_update` | Seller → Buyer | Fulfillment and tracking information. |
| `cancellation` | Either → Either | Request to cancel an order or negotiation. |

### 4.2 RFQ (Request for Quote)

```json
{
  "role": "user",
  "parts": [
    {
      "type": "data",
      "mimeType": "application/vnd.aaio.commerce.v0.1+json",
      "data": {
        "type": "rfq",
        "rfq_id": "RFQ-2026-001",
        "items": [
          {
            "product_id": "prod_widget_pro_2026",
            "quantity": 100,
            "required_by": "2026-05-01"
          }
        ],
        "shipping": {
          "country": "FI",
          "postal_code": "00100",
          "method": "standard"
        },
        "payment_terms": "net_30",
        "valid_until": "2026-04-16T23:59:59Z"
      }
    }
  ]
}
```

### 4.3 Quote Response

```json
{
  "role": "agent",
  "parts": [
    {
      "type": "data",
      "mimeType": "application/vnd.aaio.commerce.v0.1+json",
      "data": {
        "type": "quote",
        "quote_id": "QUO-2026-001",
        "rfq_reference": "RFQ-2026-001",
        "items": [
          {
            "product_id": "prod_widget_pro_2026",
            "quantity": 100,
            "unit_price": {
              "amount": 3999,
              "currency": "EUR"
            },
            "total_price": {
              "amount": 399900,
              "currency": "EUR"
            },
            "availability": "in_stock",
            "lead_time_days": 3
          }
        ],
        "shipping_cost": {
          "amount": 2500,
          "currency": "EUR"
        },
        "total": {
          "amount": 402400,
          "currency": "EUR"
        },
        "payment_terms": "net_30",
        "valid_until": "2026-04-16T23:59:59Z",
        "conditions": [
          "Prices subject to stock availability at time of order",
          "Bulk discount applied for 100+ units"
        ]
      }
    }
  ]
}
```

### 4.4 Purchase Order

```json
{
  "role": "user",
  "parts": [
    {
      "type": "data",
      "mimeType": "application/vnd.aaio.commerce.v0.1+json",
      "data": {
        "type": "purchase_order",
        "po_number": "PO-2026-001",
        "quote_reference": "QUO-2026-001",
        "acp_transaction_id": "550e8400-e29b-41d4-a716-446655440001",
        "items": [
          {
            "product_id": "prod_widget_pro_2026",
            "quantity": 100,
            "agreed_unit_price": {
              "amount": 3999,
              "currency": "EUR"
            }
          }
        ],
        "shipping": {
          "country": "FI",
          "postal_code": "00100",
          "address_line1": "Mannerheimintie 1",
          "city": "Helsinki",
          "method": "standard"
        },
        "billing": {
          "company": "BuyerCorp Oy",
          "vat_id": "FI12345678",
          "address": "Aleksanterinkatu 10, 00100 Helsinki"
        }
      }
    }
  ]
}
```

## 5. Task Lifecycle for Commerce

### 5.1 Mapping to A2A Task States

| Commerce Phase | A2A Task State | Description |
|----------------|----------------|-------------|
| RFQ sent | `SUBMITTED` | Buyer has sent a request for quote. |
| Quote being prepared | `WORKING` | Seller is generating pricing. |
| Quote sent, awaiting buyer | `INPUT_REQUIRED` | Seller awaits buyer's decision. |
| Purchase order sent | `WORKING` | Seller is processing the order. |
| Payment required | `AUTH_REQUIRED` | ACP payment needs to be executed. |
| Order confirmed | `COMPLETED` | Transaction successfully completed. |
| Order rejected | `REJECTED` | Seller rejected the order. |
| Cancellation | `CANCELED` | Either party canceled. |
| Error | `FAILED` | Unrecoverable error during processing. |

### 5.2 Context Grouping

All messages within a single negotiation MUST share the same `context_id`.
This allows both agents to:

- Retrieve the full negotiation history via `ListTasks` filtered by `context_id`.
- Resume interrupted negotiations.
- Reference prior quotes and counter-offers.

Example context flow:

```
context_id: "negotiation-2026-04-09-buyer001-seller001"

Task 1: RFQ (SUBMITTED → WORKING → INPUT_REQUIRED)
  ├── Message: RFQ from buyer
  ├── Message: Quote from seller
  └── Artifact: quote-document

Task 2: Counter-offer (SUBMITTED → WORKING → INPUT_REQUIRED)
  ├── Message: Counter-offer from buyer
  └── Message: Revised quote from seller

Task 3: Purchase Order (SUBMITTED → WORKING → COMPLETED)
  ├── Message: PO from buyer
  ├── Message: Order confirmation from seller
  └── Artifact: order-confirmation
```

### 5.3 Artifacts

Commerce artifacts are structured data objects attached to tasks:

| Artifact Type | MIME Type | Description |
|---------------|-----------|-------------|
| `quote` | `application/vnd.aaio.commerce.quote.v0.1+json` | Formal price quote. |
| `order-confirmation` | `application/vnd.aaio.commerce.order.v0.1+json` | Confirmed order details. |
| `invoice` | `application/vnd.aaio.commerce.invoice.v0.1+json` | Payment invoice. |
| `shipping-label` | `application/pdf` | Shipping label (if applicable). |

## 6. Message and Artifact Schemas

### 6.1 Quote Artifact Schema

```json
{
  "type": "quote",
  "quote_id": "QUO-2026-001",
  "seller": {
    "agent_id": "seller-agent-001",
    "company": "WidgetCorp",
    "vat_id": "FI98765432"
  },
  "buyer": {
    "agent_id": "buyer-agent-001",
    "company": "BuyerCorp Oy"
  },
  "items": [
    {
      "product_id": "prod_widget_pro_2026",
      "name": "Widget Pro 2026",
      "quantity": 100,
      "unit_price": {"amount": 3999, "currency": "EUR"},
      "total": {"amount": 399900, "currency": "EUR"},
      "aaio_schema_ref": "aaio-product/v0.1"
    }
  ],
  "subtotal": {"amount": 399900, "currency": "EUR"},
  "shipping": {"amount": 2500, "currency": "EUR"},
  "tax": {"amount": 96576, "currency": "EUR", "rate": 0.24},
  "total": {"amount": 498976, "currency": "EUR"},
  "payment_terms": "net_30",
  "valid_until": "2026-04-16T23:59:59Z",
  "created_at": "2026-04-09T12:00:00Z"
}
```

### 6.2 Order Confirmation Artifact Schema

```json
{
  "type": "order_confirmation",
  "order_id": "ORD-2026-001",
  "po_reference": "PO-2026-001",
  "quote_reference": "QUO-2026-001",
  "acp_transaction_id": "550e8400-e29b-41d4-a716-446655440001",
  "acp_payment_id": "pi_3ABC123",
  "status": "confirmed",
  "items": [
    {
      "product_id": "prod_widget_pro_2026",
      "quantity": 100,
      "unit_price": {"amount": 3999, "currency": "EUR"}
    }
  ],
  "total": {"amount": 498976, "currency": "EUR"},
  "estimated_delivery": "2026-04-12",
  "shipping_method": "standard",
  "tracking_url": null,
  "created_at": "2026-04-09T12:30:00Z"
}
```

## 7. Multi-Turn Negotiation

### 7.1 Counter-Offer Flow

When a buyer agent wants to negotiate terms:

1. Buyer receives a quote (Task enters `INPUT_REQUIRED`).
2. Buyer sends a `counter_offer` message with modified terms.
3. Seller evaluates and responds with either:
   - A revised `quote` (negotiation continues).
   - An `order_rejection` with the reason (negotiation fails).
   - Acceptance of the counter-offer terms (buyer proceeds to PO).

### 7.2 Counter-Offer Message

```json
{
  "type": "counter_offer",
  "quote_reference": "QUO-2026-001",
  "proposed_changes": {
    "items": [
      {
        "product_id": "prod_widget_pro_2026",
        "requested_unit_price": {"amount": 3500, "currency": "EUR"},
        "justification": "Competitor quote at 3600 EUR/unit for equivalent product"
      }
    ],
    "requested_payment_terms": "net_60",
    "requested_shipping": "express"
  }
}
```

### 7.3 Negotiation Limits

- Agents SHOULD limit negotiation to a maximum of 5 counter-offer rounds.
- After the limit, the seller agent SHOULD present a final "take it or leave it"
  quote.
- Buyer agents MUST respect `valid_until` timestamps on quotes. Expired quotes
  require a new RFQ.

### 7.4 Push Notifications for Async Negotiations

For asynchronous negotiations (where agents may not be constantly polling):

1. Buyer registers a push notification endpoint for the task:
   ```
   POST /tasks/{taskId}/pushNotifications
   {
     "url": "https://buyer.example.com/webhooks/a2a",
     "events": ["task_state_changed", "message_received"]
   }
   ```
2. Seller sends task updates via the registered webhook.
3. Buyer processes updates and responds when ready.

## 8. AAIO Integration Requirements

### 8.1 Discovery

Seller agents MUST be discoverable via:

1. **AgentCard** at `/.well-known/agent.json` with the `aaio-commerce` extension.
2. **AAIO Manifest** at `/.well-known/aaio-manifest.json` listing A2A support:

```json
{
  "aaioVersion": "0.1",
  "protocols": {
    "a2a": {
      "version": "1.0",
      "agent_card_url": "/.well-known/agent.json",
      "role": "seller",
      "commerce_profile": "0.1",
      "categories": ["electronics/widgets"],
      "supported_message_types": ["rfq", "quote", "purchase_order", "counter_offer"]
    }
  }
}
```

### 8.2 Cross-Protocol Flow

The complete AAIO commerce flow using all three protocols:

```
1. Discovery:     Buyer finds Seller via AgentCard (A2A)
2. Catalog:       Buyer browses products via UCP endpoints
3. Negotiation:   Buyer and Seller negotiate via A2A messages
4. Payment:       Buyer pays via ACP (Stripe)
5. Confirmation:  Seller confirms via A2A artifact
6. Fulfillment:   Seller sends shipping updates via A2A
```

### 8.3 Data Consistency

- Product references in A2A commerce messages MUST use the same `product_id`
  as the UCP catalog.
- Pricing in quotes MUST be consistent with current UCP data (within the
  quote's validity period).
- ACP `Transaction-Id` referenced in purchase orders MUST match the actual
  ACP transaction.

## 9. Security Considerations

### 9.1 Agent Authentication

- Buyer and seller agents MUST authenticate via one of the schemes declared
  in the seller's AgentCard `security` section.
- OAuth2 Client Credentials flow is RECOMMENDED for B2B commerce.

### 9.2 Message Integrity

- Agents SHOULD use `AgentCardSignature` (JWS) to verify the authenticity
  of each other's AgentCards.
- Commerce messages containing financial data SHOULD be signed by the
  sending agent.

### 9.3 Transaction Binding

- The `acp_transaction_id` in a purchase order MUST be generated by the
  buyer agent and used consistently across the A2A negotiation and the
  ACP payment.
- Seller agents MUST verify that the ACP payment matches the agreed terms
  before confirming the order.

### 9.4 Rate Limiting

- Seller agents SHOULD implement rate limiting on RFQ submissions
  (RECOMMENDED: 10 RFQs per agent per hour).
- Negotiation rounds SHOULD be time-limited (RECOMMENDED: 24-hour response
  window per round).

### 9.5 Privacy

- Agent-to-agent messages MUST NOT contain unencrypted PII beyond what
  is necessary for the transaction (shipping address, billing details).
- Agents SHOULD support end-to-end encryption for messages containing
  payment details.

### 9.6 Dispute Resolution

- Both agents MUST retain the complete negotiation history (all tasks and
  messages within the `context_id`) for a minimum of 2 years.
- Order confirmation artifacts serve as the binding agreement between parties.

## 10. Conformance

An implementation is conformant with this specification if it:

1. Publishes an AgentCard with the `aaio-commerce` extension (Section 3).
2. Supports at minimum `rfq`, `quote`, and `purchase_order` message types (Section 4).
3. Maps commerce phases to A2A task states per Section 5.1.
4. Groups negotiation messages under a shared `context_id` (Section 5.2).
5. Uses the defined artifact MIME types (Section 5.3).
6. Advertises commerce capabilities in the AAIO manifest (Section 8.1).
7. Meets all security requirements in Section 9.

## 11. References

### Normative References

- [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) — Key words for use in RFCs
- [A2A Protocol Specification v1.0](https://github.com/a2aproject/A2A/blob/main/specification/a2a.proto) — Agent-to-Agent Protocol (Linux Foundation)
- [RFC 7519](https://www.rfc-editor.org/rfc/rfc7519) — JSON Web Token (JWT)
- [RFC 7515](https://www.rfc-editor.org/rfc/rfc7515) — JSON Web Signature (JWS)
- [AAIO Core Specification](aaio-core-v0.1.md) — Agentic AI Optimization Core
- [ACP Integration Specification](acp-integration-v0.1.md) — Agent Commerce Protocol
- [UCP Integration Specification](ucp-integration-v0.1.md) — Universal Commerce Protocol
- [AAIO Product Schema](../schemas/aaio-product.schema.json) — Product Data Schema
- [AAIO Service Schema](../schemas/aaio-service.schema.json) — Service Data Schema

### Informative References

- [A2A GitHub Repository](https://github.com/a2aproject/A2A) — Reference implementations and examples
- [Schema.org Product](https://schema.org/Product) — Schema.org Product type
- [ISO 3166-1](https://www.iso.org/iso-3166-country-codes.html) — Country codes
- [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) — Currency codes

---

*Copyright 2026 Tekoäly-Dani. Licensed under Apache 2.0.*
