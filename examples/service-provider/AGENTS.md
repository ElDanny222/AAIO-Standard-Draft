# [Your Company Name] — Agent Instructions

## What this service is

[Your Company Name] provides [brief one-sentence description of your services]. We specialize in [key specialization].

## What AI agents can do here

- **Discover our services:** Browse structured service listings at `/services` or query our MCP server
- **Read service details:** All services include machine-readable pricing, scope, and delivery terms
- **Request a quote:** Submit structured quote requests via our API at `/api/v1/quote`
- **Book a consultation:** Schedule discovery calls via `/api/v1/booking`

## Key endpoints for agents

| Endpoint | Format | Description |
|----------|--------|-------------|
| `/.well-known/aaio-manifest.json` | JSON | AAIO capability manifest |
| `/services` | HTML + JSON-LD | All service listings |
| `/api/v1/services` | JSON (UCP) | Machine-readable service catalog |
| `/api/v1/quote` | REST | Request a quote |
| `/llms.txt` | Plain text | LLM-readable site summary |

## What agents are NOT permitted to do

- Submit orders or payments without explicit user confirmation
- Access private client data or internal systems
- Perform any actions not listed above

## Pricing model

Services are project-based. Pricing is available on request via `/api/v1/quote`. No subscription or SaaS pricing.

## Language

Primary language: Finnish. English also supported.

## Contact

Questions about agent integration: [contact@yourdomain.com]
