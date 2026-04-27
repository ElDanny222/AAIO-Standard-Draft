# Governance

This document defines how the AAIO Standard Draft is maintained — who decides what, on what timeline, and how versions are cut. Detailed contributor mechanics live in [CONTRIBUTING.md](CONTRIBUTING.md).

---

## Roles

| Role | Holder | Responsibility |
|------|--------|----------------|
| **Steward** | [Tekoäly-Dani](https://tekoalydani.com) | Final say on substantive spec direction, accepts/rejects RFCs, approves Stable promotions. |
| **Protocol Maintainer** | A2A-Alex (`a2a-alex@tekoalydani.com`) | First reviewer on all PRs, owns release cadence, triages issues, merges after lazy consensus. |
| **Contributors** | Anyone | Open issues, submit PRs, share implementation feedback. |

---

## Decision Process

Two paths, depending on change size:

- **Editorial / fixes** (typos, broken links, clarifying wording, examples): lazy consensus. Maintainer reviews and merges. No issue required.
- **Substantive** (new sections, schema additions, semantic changes, new spec documents): open an issue first describing the proposal. If no objections from Steward or maintainer within **7 days**, proceed with PR. PRs touching `Stable` documents always require explicit Steward approval.

If consensus cannot be reached on a substantive change, the Steward decides. Decisions are recorded in the PR thread.

---

## Release Cadence

Versioning follows a simple per-document scheme aligned with the status header in each spec:

- `Draft v0.X` — working document, breaking changes allowed between minor versions
- `RFC v0.X` — feature-frozen for community review, minimum 14-day comment window before promotion
- `Stable v1.X` — semver discipline; breaking changes require a new major version and a deprecation note on the previous one

Releases are cut by tagging `main` (`<doc-key>-v<version>`) and updating [CHANGELOG.md](CHANGELOG.md). No fixed cadence — releases happen when a document reaches a stable state, not on a calendar.

---

## Review SLA

- Editorial PRs: reviewed within **7 days**
- Substantive PRs: first response within **14 days**, decision within **30 days**
- Security or correctness issues that misrepresent protocol behavior: prioritized, no SLA cap

If the maintainer is unavailable, the Steward acts as fallback reviewer.

---

## Scope Boundary

Governance disputes about what belongs in this repository (vs. an upstream protocol repo such as MCP, ACP, UCP, or A2A) are resolved by the Steward. The default answer is "AAIO repository covers the optimization layer; protocol-internal mechanics belong upstream" — see [CONTRIBUTING.md §Scope](CONTRIBUTING.md#scope).

---

## Changing This Document

Governance changes require a PR with at least 7 days open for comment and explicit Steward approval before merge.
