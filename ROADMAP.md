# AAIO Standard Draft — Roadmap

> **Status:** Draft v0.1 | Maintained by [Tekoäly-Dani](https://tekoalydani.com)

This document outlines the planned evolution of the AAIO Standard specifications. Items are subject to change based on protocol ecosystem developments and community feedback.

---

## Current State: v0.1 (April 2026)

The v0.1 release establishes the foundational layer of AAIO specifications:

- ✅ AIO Framework (umbrella)
- ✅ SEO, AEO, GEO specifications
- ✅ AAIO Core Specification
- ✅ AXO Framework
- ✅ Protocol integration guides (MCP, ACP, UCP, A2A)
- ✅ JSON schemas (manifest, product, service, scoring)
- ✅ Implementation roadmap and terminology
- 🔄 Reference implementations (in progress)

---

## v0.2 — Reference Implementations (Q2 2026)

**Theme:** Show, don't just tell.

- [ ] Complete `examples/service-provider/` — professional services firm (consultant, agency)
- [ ] Complete `examples/ecommerce/` — product-selling business
- [ ] Complete `examples/saas-platform/` — SaaS product
- [ ] Validation tooling: CLI tool to check a URL against AAIO requirements
- [ ] `ai.txt` formal specification alignment (as standard matures)

---

## v0.3 — Ecosystem Updates (Q3 2026)

**Theme:** Track the protocol ecosystem.

- [ ] MCP server implementation guide (updated for latest MCP spec)
- [ ] A2A v1.0 alignment (if spec stabilizes)
- [ ] ACP merchant onboarding guide
- [ ] AAIO Readiness Score calculator (web tool)

---

## v1.0 — Stable Specification (Target: Q4 2026)

**Theme:** Production-ready standard.

- [ ] Community review period (30 days)
- [ ] All specs moved from `draft` to `stable`
- [ ] Version schema (`aaio-manifest`) locked for backwards compatibility
- [ ] At least 3 real-world case studies from live implementations

---

## What's Not in Scope

- AAIO is not a protocol itself — we will not define a new protocol
- AAIO does not replace SEO, AEO, GEO, or any existing protocol
- We do not maintain implementations — only specifications and reference examples

---

## Contributing

Have feedback on the roadmap? Open a [GitHub Discussion](../../discussions) or file an issue. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## Versioning Policy

All specifications follow **Semantic Versioning** within the `specs/` directory:

- **Patch** (0.1.x): Clarifications, typo fixes, non-normative additions
- **Minor** (0.x.0): New normative requirements, expanded scope, new protocol integrations
- **Major** (x.0.0): Breaking changes to required fields, scoring model, or schema structure

The repository version (in `CHANGELOG.md`) tracks the overall collection, not individual specs.
