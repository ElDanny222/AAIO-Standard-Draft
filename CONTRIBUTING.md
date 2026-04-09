# Contributing to AAIO Standard Draft

Thank you for your interest in contributing to the AAIO Standard Draft. This is an open, community-developed specification. All contributions are welcome — whether that is correcting an error, proposing a new section, or sharing an implementation experience.

---

## What This Repository Is

This repository contains **draft specifications** for Agentic AI Optimization (AAIO). The goal is to produce vendor-neutral, implementable standards that help organizations become agent-ready.

These are working documents. Everything is open for discussion. If something is unclear, incorrect, or missing, that is a valid reason to open an issue or pull request.

---

## Ways to Contribute

### Report an issue

Use GitHub Issues to report:
- Errors or ambiguities in existing specifications
- Missing definitions or terminology
- Broken links or formatting problems
- Protocol details that are outdated

Open an issue and describe what is wrong and where it is. You do not need a proposed fix to open an issue.

### Propose a change

Use a pull request to propose:
- Corrections to existing specifications
- New sections within an existing document
- New reference implementations in `examples/`
- Schema additions or corrections

For significant changes (new protocol profiles, major structural revisions), open an issue first to discuss the approach before writing the PR.

### Share implementation experience

If you have implemented AAIO requirements in a real system and found gaps, edge cases, or better approaches — please share them. Implementation feedback is the most valuable contribution at this stage.

Open an issue with the label `implementation-feedback` or email [dani@tekoalydani.com](mailto:dani@tekoalydani.com).

---

## Pull Request Process

1. **Fork the repository** and create a branch from `main`

   Branch naming:
   - `fix/description` for corrections
   - `feat/description` for new content
   - `docs/description` for documentation improvements

2. **Make your changes**

   Follow the style guide below.

3. **Update the relevant document's status header**

   If your change is substantive, update the version or add a changelog entry.

4. **Open a pull request**

   Your PR description should include:
   - What changed and why
   - Which section(s) are affected
   - Any open questions or alternatives you considered

5. **Review**

   All PRs are reviewed by the repository maintainer ([Tekoäly-Dani](https://tekoalydani.com)). The review process checks for:
   - Technical accuracy
   - Consistency with the overall AAIO framework
   - Clarity and readability
   - Alignment with the existing protocol landscape

6. **Merge**

   Once approved, your contribution will be merged. Significant contributors will be credited in the document they contributed to.

---

## Style Guide

### Document format

All specification documents follow this structure:

```
# Document Title

> **Status:** Draft v0.X | Maintained by [Tekoäly-Dani](https://tekoalydani.com)

[One-sentence description of what this document covers]

---

## [Section]

[Content]

---

## Suomeksi / In Finnish

[Finnish summary of the document]
```

### Language

- **English first.** All specification content is written in English.
- **Finnish summary at the end.** Every specification document includes a Finnish summary section.
- Technical terms (MCP, ACP, UCP, A2A, AAIO) remain in English in both language sections.
- Direct and precise. Avoid marketing language, hedging, and filler.

### Code examples

Use fenced code blocks with language identifiers (json, http, markdown, etc.).

### Tables

Use Markdown tables for structured comparisons. Prefer tables over long lists when there are multiple attributes to compare.

### Status labels

Use these labels consistently:

| Label | Meaning |
|-------|---------|
| `Draft` | Working document, subject to change |
| `RFC` | Request for Comments — seeking community review |
| `Stable` | Finalized, changes require a new version |
| `Deprecated` | Superseded by a newer version |

---

## Scope

This repository is specifically about **AAIO as an optimization framework** — how organizations implement agent protocols to become agent-ready.

Out of scope for this repository:
- Core protocol definitions for MCP, ACP, UCP, or A2A (those have their own repositories)
- General AI or LLM development
- SEO or traditional web marketing techniques

If you are unsure whether a contribution is in scope, open an issue and ask.

---

## Code of Conduct

This is a technical specification project. Contributions are evaluated on technical merit and clarity. Be direct, be precise, and be constructive.

---

## Contact

[Tekoäly-Dani](https://tekoalydani.com)  
[dani@tekoalydani.com](mailto:dani@tekoalydani.com)
