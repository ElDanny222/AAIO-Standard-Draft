# Changelog

All notable changes to the AAIO Standard Draft will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

### Added
- Repository scaffolding: `specs/`, `schemas/`, `examples/`, `docs/` directories
- Apache 2.0 License
- Contributing guidelines (`CONTRIBUTING.md`)
- This changelog
- **AIO Framework** (`specs/aio-framework-v0.1.md`) — umbrella framework unifying all AI optimization layers
- **SEO Foundations** (`specs/seo-foundations-v0.1.md`) — SEO requirements underpinning AI optimization
- **AEO Guidelines** (`specs/aeo-guidelines-v0.1.md`) — Answer Engine Optimization best practices
- **GEO Guidelines** (`specs/geo-guidelines-v0.1.md`) — Generative Engine Optimization guidelines
- **AAIO Core Specification** (`specs/aaio-core-v0.1.md`) — core agent-readiness requirements and scoring
- **AXO Framework** (`specs/axo-framework-v0.1.md`) — Agent Experience Optimization (UX perspective)
- **ACP Integration** (`specs/acp-integration-v0.1.md`) — Agent Commerce Protocol integration
- **UCP Integration** (`specs/ucp-integration-v0.1.md`) — Universal Commerce Protocol integration
- **A2A Commerce** (`specs/a2a-commerce-v0.1.md`) — Agent-to-Agent negotiation protocol profile
- JSON schemas: `aaio-manifest`, `aaio-product`, `aaio-service`, `aaio-scoring`
- Terminology glossary (`docs/terminology.md`)
- Protocol landscape overview (`docs/protocol-landscape.md`)
- Implementation roadmap (`docs/implementation-roadmap.md`)

### Fixed
- Schema field name consistency: `aaioVersion` (camelCase) used everywhere
- Currency codes follow ISO 4217 uppercase format (`EUR`, not `eur`)
- ACP header names aligned across specs and roadmap
- Schema `$id` domains unified to `aaio-standard.org`
- Service schema `billing_period` null handling corrected
