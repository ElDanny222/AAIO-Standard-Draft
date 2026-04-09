# Agent Commerce Protocol (ACP) Integration Specification

**Version:** 0.1-draft  
**Status:** Draft  
**Date:** 2026-04-09  
**Authors:** Tekoaly-Dani AAIO Working Group  

---

## Abstract

This document specifies how Agentic AI Optimization (AAIO)-compliant websites
implement the Agent Commerce Protocol (ACP) to enable secure, autonomous
machine-to-machine transactions. ACP provides the transport-layer conventions —
HTTP headers, authentication flows, and transaction lifecycle management — that
allow AI purchasing agents to discover, negotiate, and complete payments on
behalf of human principals.

This specification does not define a new protocol. It profiles the existing
Stripe ACP framework within the AAIO optimization layer, prescribing how
e-commerce and service platforms expose ACP endpoints so that autonomous agents
can transact reliably and securely.

## Status of This Document

This is a draft specification (v0.1) published for community review. It is
not yet suitable for production implementation without additional validation.
Feedback should be directed to the AAIO-Standard-Draft repository.

## Table of Contents

1. [Terminology](#1-terminology)
2. [Overview](#2-overview)
3. [ACP Header Specification](#3-acp-header-specification)
4. [Transaction Lifecycle](#4-transaction-lifecycle)
5. [Authentication and Authorization](#5-authentication-and-authorization)
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
| **ACP** | Agent Commerce Protocol — Stripe's framework for machine-to-machine payment transactions. |
| **AAIO** | Agentic AI Optimization — the optimization layer ensuring websites are discoverable, understandable, and transactable by autonomous AI agents. |
| **Purchasing Agent** | An AI agent acting on behalf of a human principal to discover, evaluate, and purchase goods or services. |
| **Merchant Agent** | An AI agent or ACP-compliant endpoint representing a seller, capable of processing agent-initiated transactions. |
| **Human Principal** | The human user who has delegated purchasing authority to a Purchasing Agent. |
| **Transaction Envelope** | The complete set of ACP headers and payload constituting a single atomic transaction request. |
| **Agent Credential** | A cryptographic token (typically a scoped API key or OAuth2 bearer token) authorizing an agent to act on behalf of its principal. |

## 2. Overview

### 2.1 Problem Statement

Traditional e-commerce checkout flows are designed for human interaction:
multi-step forms, CAPTCHA challenges, visual confirmations. These are
impassable barriers for autonomous AI agents. ACP addresses this by defining
a machine-readable transaction protocol that operates alongside (not replacing)
human-facing checkout.

### 2.2 Architecture

```
┌─────────────────┐         ┌──────────────────┐         ┌─────────────────┐
│  Human Principal│         │ Purchasing Agent  │         │ Merchant (AAIO) │
│  (delegates)    │────────>│ (AI agent)        │────────>│ ACP Endpoint    │
│                 │         │                   │<────────│                 │
└─────────────────┘         └──────────────────┘         └─────────────────┘
                                    │                            │
                                    │     ACP Headers            │
                                    │     + Stripe API           │
                                    └────────────────────────────┘
```

### 2.3 Relationship to AAIO

ACP is one of three commerce protocol integrations defined within the AAIO
framework:

- **ACP** (this document) — Payment execution via Stripe
- **UCP** — Product/service data standardization via Google/Shopify
- **A2A** — Agent-to-agent negotiation via the A2A Protocol

An AAIO-compliant site MAY implement any combination of these protocols.
Sites implementing ACP MUST also expose AAIO-compliant product/service
schemas (see `aaio-product.schema.json` and `aaio-service.schema.json`).

## 3. ACP Header Specification

### 3.1 Request Headers

All ACP transaction requests MUST include the following HTTP headers:

| Header | Type | Required | Description |
|--------|------|----------|-------------|
| `ACP-Version` | String | REQUIRED | Protocol version. Current: `"0.1"`. |
| `ACP-Agent-Id` | String | REQUIRED | Unique identifier of the Purchasing Agent. |
| `ACP-Principal-Id` | String | REQUIRED | Identifier of the Human Principal on whose behalf the agent acts. |
| `ACP-Transaction-Id` | UUID | REQUIRED | Idempotency key for the transaction. Generated by the Purchasing Agent. |
| `ACP-Intent` | Enum | REQUIRED | Transaction intent: `purchase`, `quote`, `hold`, `cancel`. |
| `ACP-Delegation-Token` | String | REQUIRED | Cryptographic proof of delegation from Principal to Agent. |
| `ACP-Callback-Url` | URL | OPTIONAL | Webhook URL for asynchronous transaction status updates. |
| `ACP-Max-Amount` | Object | OPTIONAL | Maximum authorized amount (`{"amount": 5000, "currency": "EUR"}`). |
| `ACP-Metadata` | JSON | OPTIONAL | Arbitrary key-value metadata for the transaction. |

### 3.2 Response Headers

Merchant ACP endpoints MUST return the following headers:

| Header | Type | Description |
|--------|------|-------------|
| `ACP-Version` | String | Protocol version supported by the merchant. |
| `ACP-Transaction-Id` | UUID | Echo of the request Transaction-Id. |
| `ACP-Status` | Enum | Transaction status: `accepted`, `pending`, `rejected`, `failed`. |
| `ACP-Payment-Id` | String | Stripe Payment Intent ID (when `ACP-Status` is `accepted` or `pending`). |
| `ACP-Receipt-Url` | URL | Machine-readable receipt URL. |
| `ACP-Retry-After` | Integer | Seconds before retrying (when `ACP-Status` is `pending`). |

### 3.3 Content Types

- Request body: `application/json` with an ACP Transaction Envelope.
- Response body: `application/json` with an ACP Transaction Result.

## 4. Transaction Lifecycle

### 4.1 State Machine

```
  ┌──────────┐
  │  QUOTE   │ ◄── ACP-Intent: quote
  └────┬─────┘
       │ (agent confirms)
       ▼
  ┌──────────┐
  │   HOLD   │ ◄── ACP-Intent: hold (optional pre-authorization)
  └────┬─────┘
       │ (agent confirms)
       ▼
  ┌──────────┐     ┌──────────┐
  │ PURCHASE │────>│ ACCEPTED │
  └────┬─────┘     └──────────┘
       │
       ├──────────>┌──────────┐
       │           │ PENDING  │──> (async confirmation via callback)
       │           └──────────┘
       │
       ├──────────>┌──────────┐
       │           │ REJECTED │
       │           └──────────┘
       │
       └──────────>┌──────────┐
                   │  FAILED  │
                   └──────────┘

  At any point:
  ┌──────────┐
  │  CANCEL  │ ◄── ACP-Intent: cancel (with original ACP-Transaction-Id)
  └──────────┘
```

### 4.2 Quote Flow

A Purchasing Agent SHOULD request a quote before committing to a purchase.
The quote response includes the current price, availability, and terms.

```http
POST /acp/v0.1/transactions HTTP/1.1
Host: shop.example.com
ACP-Version: 0.1
ACP-Agent-Id: agent-buyer-001
ACP-Principal-Id: user-12345
ACP-Transaction-Id: 550e8400-e29b-41d4-a716-446655440000
ACP-Intent: quote
ACP-Delegation-Token: eyJhbGciOi...
Content-Type: application/json

{
  "items": [
    {
      "sku": "WIDGET-PRO-2026",
      "quantity": 2,
      "schema_ref": "aaio-product/v0.1"
    }
  ],
  "shipping": {
    "country": "FI",
    "postal_code": "00100"
  }
}
```

### 4.3 Purchase Flow

```http
POST /acp/v0.1/transactions HTTP/1.1
Host: shop.example.com
ACP-Version: 0.1
ACP-Agent-Id: agent-buyer-001
ACP-Principal-Id: user-12345
ACP-Transaction-Id: 550e8400-e29b-41d4-a716-446655440001
ACP-Intent: purchase
ACP-Delegation-Token: eyJhbGciOi...
ACP-Max-Amount: {"amount": 10000, "currency": "EUR"}
Content-Type: application/json

{
  "items": [
    {
      "sku": "WIDGET-PRO-2026",
      "quantity": 2
    }
  ],
  "payment_method": "pm_card_visa",
  "shipping": {
    "country": "FI",
    "postal_code": "00100",
    "address_line1": "Mannerheimintie 1"
  }
}
```

### 4.4 Idempotency

`ACP-Transaction-Id` serves as an idempotency key. Merchants MUST return
the same response for duplicate requests with the same Transaction-Id.
The idempotency window MUST be at least 24 hours.

## 5. Authentication and Authorization

### 5.1 Agent Authentication

Purchasing Agents authenticate to merchant ACP endpoints using one of the
following methods (in order of preference):

1. **OAuth2 Client Credentials** — The agent obtains a bearer token from the
   merchant's OAuth2 authorization server. RECOMMENDED for B2B agent
   interactions.

2. **API Key** — A pre-shared API key issued to the agent. Transmitted via
   `Authorization: Bearer <api-key>`. Suitable for trusted agent
   registrations.

3. **mTLS** — Mutual TLS for high-value or regulated transactions. The
   agent presents a client certificate during the TLS handshake.

### 5.2 Delegation Proof

The `ACP-Delegation-Token` MUST be a signed JWT containing:

```json
{
  "iss": "principal-identity-provider",
  "sub": "user-12345",
  "aud": "agent-buyer-001",
  "scope": "purchase",
  "max_amount": {
    "amount": 50000,
    "currency": "EUR"
  },
  "categories": ["electronics", "software"],
  "exp": 1735689600,
  "iat": 1735603200,
  "jti": "delegation-uuid-here"
}
```

Fields:
- `scope`: MUST be one of `purchase`, `quote`, `hold`.
- `max_amount`: Maximum single-transaction amount the agent is authorized to spend.
- `categories`: OPTIONAL product category restrictions.
- `exp`: Delegation expiration. MUST NOT exceed 30 days from `iat`.

### 5.3 Stripe Integration

ACP transactions are settled via the Stripe Payments API. The merchant's
ACP endpoint:

1. Validates the ACP headers and delegation token.
2. Creates a Stripe PaymentIntent with the transaction details.
3. Confirms the PaymentIntent using the provided payment method.
4. Returns the `ACP-Payment-Id` (Stripe PaymentIntent ID) in the response.

The merchant MUST store the mapping between `ACP-Transaction-Id` and the
Stripe PaymentIntent ID for audit and reconciliation purposes.

## 6. AAIO Integration Requirements

### 6.1 Discovery

AAIO-compliant merchants MUST advertise ACP support in their AAIO manifest
(`/.well-known/aaio-manifest.json`):

```json
{
  "aaioVersion": "0.1",
  "protocols": {
    "acp": {
      "version": "0.1",
      "endpoint": "/acp/v0.1/transactions",
      "authentication": ["oauth2_client_credentials", "api_key"],
      "supported_intents": ["quote", "purchase", "hold", "cancel"],
      "supported_currencies": ["eur", "usd", "gbp"],
      "max_transaction_amount": {
        "eur": 100000
      }
    }
  }
}
```

### 6.2 Product Data

ACP transaction items MUST reference products described by the
`aaio-product.schema.json` or `aaio-service.schema.json` schemas. This
ensures the Purchasing Agent can programmatically verify product attributes
before committing to a transaction.

### 6.3 Agent Card Integration

When the merchant also implements the A2A protocol, the AgentCard SHOULD
include ACP capabilities:

```json
{
  "name": "MerchantBot",
  "url": "https://shop.example.com/.well-known/agent.json",
  "skills": [
    {
      "id": "commerce",
      "name": "Product Commerce",
      "description": "Purchase products via ACP",
      "tags": ["commerce", "acp", "payments"]
    }
  ],
  "extensions": {
    "acp": {
      "endpoint": "/acp/v0.1/transactions",
      "version": "0.1"
    }
  }
}
```

## 7. Error Handling

### 7.1 Error Response Format

```json
{
  "error": {
    "code": "ACP_INSUFFICIENT_DELEGATION",
    "message": "Delegation token does not authorize this amount",
    "details": {
      "requested_amount": 15000,
      "max_authorized": 10000,
      "currency": "EUR"
    }
  }
}
```

### 7.2 Error Codes

| Code | HTTP Status | Description |
|------|-------------|-------------|
| `ACP_INVALID_HEADER` | 400 | Missing or malformed ACP header. |
| `ACP_INVALID_VERSION` | 400 | Unsupported ACP-Version. |
| `ACP_INVALID_DELEGATION` | 401 | Delegation token is invalid, expired, or revoked. |
| `ACP_INSUFFICIENT_DELEGATION` | 403 | Delegation scope does not cover the requested action. |
| `ACP_AGENT_NOT_AUTHORIZED` | 403 | Agent is not registered or authorized with this merchant. |
| `ACP_DUPLICATE_TRANSACTION` | 409 | Transaction-Id already processed with different parameters. |
| `ACP_ITEM_UNAVAILABLE` | 422 | Requested item is out of stock or discontinued. |
| `ACP_AMOUNT_EXCEEDED` | 422 | Transaction amount exceeds ACP-Max-Amount or delegation limit. |
| `ACP_PAYMENT_FAILED` | 502 | Stripe payment processing failed. |
| `ACP_MERCHANT_UNAVAILABLE` | 503 | Merchant ACP endpoint temporarily unavailable. |

## 8. Security Considerations

### 8.1 Delegation Token Security

- Delegation tokens MUST be short-lived (maximum 30 days).
- Tokens MUST be scoped to specific categories and maximum amounts.
- The merchant MUST validate the token signature against the issuer's
  public key (fetched via OIDC discovery or pre-configured JWKS endpoint).
- Tokens MUST NOT be reusable across different merchants.

### 8.2 Transaction Security

- All ACP communication MUST occur over TLS 1.2 or higher.
- `ACP-Transaction-Id` MUST be a cryptographically random UUID v4.
- Merchants MUST implement rate limiting per `ACP-Agent-Id` (RECOMMENDED:
  100 transactions per hour per agent).
- Merchants SHOULD implement velocity checks: flag unusual transaction
  patterns (e.g., rapid successive purchases, amounts near delegation limits).

### 8.3 Audit Trail

- Merchants MUST log all ACP transactions with full headers for a minimum
  of 7 years (per PCI DSS requirements).
- Logs MUST include: timestamp, ACP-Agent-Id, ACP-Principal-Id,
  ACP-Transaction-Id, ACP-Intent, amount, and ACP-Status.

### 8.4 Fraud Prevention

- Merchants SHOULD integrate with Stripe Radar for automated fraud
  detection on agent-initiated transactions.
- Merchants MAY require additional verification for first-time agents
  (e.g., a probationary period with lower transaction limits).
- Human Principals MUST have the ability to revoke agent delegation
  at any time, invalidating all outstanding delegation tokens.

### 8.5 Privacy

- `ACP-Principal-Id` SHOULD be a pseudonymous identifier, not a
  personally identifiable value.
- Merchants MUST NOT share Principal identity across unrelated transactions
  or with third parties beyond what is necessary for payment processing.

## 9. Conformance

An implementation is conformant with this specification if it:

1. Implements all REQUIRED ACP request and response headers (Section 3).
2. Supports the `quote` and `purchase` intents at minimum (Section 4).
3. Validates delegation tokens per Section 5.2.
4. Advertises ACP support in the AAIO manifest (Section 6.1).
5. References AAIO product/service schemas for transaction items (Section 6.2).
6. Implements all error codes defined in Section 7.2.
7. Meets all security requirements in Section 8.

## 10. References

### Normative References

- [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119) — Key words for use in RFCs
- [RFC 7519](https://www.rfc-editor.org/rfc/rfc7519) — JSON Web Token (JWT)
- [RFC 6749](https://www.rfc-editor.org/rfc/rfc6749) — OAuth 2.0 Authorization Framework
- [RFC 8705](https://www.rfc-editor.org/rfc/rfc8705) — OAuth 2.0 Mutual-TLS Client Authentication
- [Stripe Payments API](https://docs.stripe.com/api/payment_intents) — PaymentIntent API Reference
- [AAIO Core Specification](aaio-core-v0.1.md) — Agentic AI Optimization Core
- [AAIO Product Schema](../schemas/aaio-product.schema.json) — Product Data Schema
- [AAIO Service Schema](../schemas/aaio-service.schema.json) — Service Data Schema

### Informative References

- [A2A Commerce Protocol Profile](a2a-commerce-v0.1.md) — Agent-to-Agent Commerce
- [UCP Integration Specification](ucp-integration-v0.1.md) — Universal Commerce Protocol
- [PCI DSS v4.0](https://www.pcisecuritystandards.org/) — Payment Card Industry Data Security Standard

---

*Copyright 2026 Tekoaly-Dani. Licensed under Apache 2.0.*
