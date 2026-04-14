# Example: Service Provider (AAIO Level 2)

This example shows a complete AAIO Level 2 implementation for a **professional services business** — a consultant, agency, or specialist firm that wants AI agents to discover and understand their services.

**Business type:** AI optimization consulting firm  
**AAIO target level:** Level 2 (Readable)  
**Estimated implementation time:** 1–2 days

---

## What's in this example

| File | Description |
|------|-------------|
| `aaio-manifest.json` | Site-level AAIO manifest (place at `yourdomain.com/.well-known/aaio-manifest.json`) |
| `AGENTS.md` | Agent instructions file (place at `yourdomain.com/AGENTS.md`) |
| `llms.txt` | LLM-readable site summary (place at `yourdomain.com/llms.txt`) |
| `ai.txt` | AI policy declaration (place at `yourdomain.com/ai.txt`) |
| `service.json` | UCP-compliant service listing example |

---

## AAIO Level 2 Requirements

To reach Level 2 (Readable), a service provider needs:

1. **Level 1 (Discoverable):** `AGENTS.md`, `robots.txt` directives, `llms.txt`
2. **Level 2 additions:** Structured service data (UCP-compliant), MCP server or structured API, `aaio-manifest.json`

This example covers both levels in a single implementation package.

---

## Adapting for your business

Replace all placeholder values:

- `yourdomain.com` → your actual domain
- `Your Company Name` → your company name
- Service names, descriptions, pricing → your actual services

See the full [Implementation Roadmap](../../docs/implementation-roadmap.md) for a complete phase-by-phase guide.
