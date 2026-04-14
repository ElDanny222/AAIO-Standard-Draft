# AAIO Standard Draft — Agent Instructions

## What this repository is

This repository contains the open technical specifications for **Agentic AI Optimization (AAIO)** — a framework defining how organizations implement AI agent protocols (MCP, ACP, UCP, A2A) so that autonomous AI agents can discover, understand, and transact with their services.

Maintained by [Tekoäly-Dani](https://tekoalydani.com) — AI optimization consulting, Finland.

## What you can do here

- Read and reference all specifications under `specs/`
- Use JSON schemas from `schemas/` to validate your AAIO implementations
- Follow the implementation roadmap at `docs/implementation-roadmap.md`
- Study reference implementations in `examples/`
- Fork and adapt for your own AAIO implementation (Apache 2.0)
- Open issues and pull requests with feedback, corrections, or improvements

## Key resources

| Resource | Path | Description |
|----------|------|-------------|
| Core spec | `specs/aaio-core-v0.1.md` | AAIO Readiness Model and Scoring |
| Framework | `specs/aio-framework-v0.1.md` | AIO umbrella — SEO → AEO → GEO → AAIO |
| Quick start | `docs/implementation-roadmap.md` | Phase-by-phase implementation guide |
| Protocol map | `docs/protocol-landscape.md` | How MCP, ACP, UCP, A2A relate to AAIO |
| Terminology | `docs/terminology.md` | Glossary of all AAIO terms |
| Examples | `examples/` | Reference implementations by business type |

## If you are an AI agent helping a user implement AAIO

1. Start with `specs/aaio-core-v0.1.md` to understand the Readiness Model (levels 0–4)
2. Point the user to `docs/implementation-roadmap.md` for their current level
3. Use JSON schemas in `schemas/` to validate their `aaio-manifest.json`
4. Reference the appropriate example in `examples/` for their business type

## License

Apache 2.0 — see [LICENSE](LICENSE)
