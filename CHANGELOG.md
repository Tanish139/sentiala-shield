# Changelog

All notable changes to Sentiala Shield are documented here.
Format: [Keep a Changelog](https://keepachangelog.com/) —
versioning: [SemVer](https://semver.org/).

## [0.1.0] — 2026-09-28

First working vertical slice: **Phases 1–6 of the product roadmap**
(the Sentiala Intelligence Core), delivered as a tested Python package
with a CLI.

### Added

- **Layer 1 — deterministic URL/domain analyzer**: dangerous schemes
  (data:/javascript:), embedded userinfo, raw IP hosts, IDN homograph
  detection (punycode decode + Cyrillic/Greek/leet confusable folding),
  typosquatting via edit distance against a curated 40+ brand list
  (international: Google, PayPal, DHL, HSBC…; India: HDFC, ICICI, SBI,
  Paytm, PhonePe, IRCTC, Airtel…), brand-in-subdomain detection,
  suspicious-TLD reputation, URL shorteners, deep subdomain chains,
  hyphen stuffing, credential-harvesting keywords, non-standard ports,
  long URLs. Legitimate brand hosts are whitelisted to avoid
  false positives.
- **Layer 2 — threat intelligence providers (SGIN)**: keyless public
  adapters — URLhaus (abuse.ch, Tier 2), RDAP via rdap.org (Tier 1,
  domain age), Cloudflare DNS-over-HTTPS (Tier 1, resolution). All
  behind a `Provider` abstraction with injectable HTTP sessions, TTL
  caching (in-memory + disk), and graceful degradation — providers
  never raise into the pipeline.
- **Layer 4 — AI correlation**: `AIProvider` abstraction with a fully
  deterministic `LocalCorrelator` that explains verdicts by restating
  existing evidence only. Cloud LLM providers plug in via configuration
  (Phase 3).
- **Layer 5 — explainable risk engine**: weighted aggregation with
  impersonation-family suppression (homograph/typosquat/brand-subdomain
  count once), 0–100 score with SAFE/LOW/MEDIUM/HIGH/CRITICAL bands,
  evidence-quality-based confidence (offline ⇒ explicitly lower).
- **Layer 6 — reporting**: structured JSON + Markdown reports with the
  mandatory four-class evidence taxonomy (VERIFIED FACT / OBSERVATION /
  AI INFERENCE / UNVERIFIED CLAIM), source reliability tiers, score
  contributions, possible-false-positive factors, recommended actions,
  and anti-fabrication guarantees (`NO RELEVANT PUBLIC INTELLIGENCE
  FOUND` / `UNVERIFIED — live intelligence unavailable`).
- **Orchestrator**: target classification (url/domain/ip/hashes),
  offline mode with explicit degradation, tool permission system
  (credential/file access denied at architecture level).
- **Local-first storage**: JSONL investigation history, TTL intelligence
  cache — everything under the user's data directory.
- **CLI**: `sentiala scan|history|providers|permissions` with
  `--offline`, `--json`, `--out report.md`; exit code 2 on
  HIGH/CRITICAL.
- **Test suite**: 68 tests across analyzer, risk engine, providers
  (recorded synthetic responses, reserved `.test` domains), cache,
  orchestrator, and anti-fabrication guarantees. Includes false-positive
  scenarios (legit brand login pages, established domains) and
  no-intelligence / conflicting-intelligence scenarios.
- **Repository**: README, architecture docs, SECURITY.md,
  CONTRIBUTING.md, CODE_OF_CONDUCT.md, .env.example, MIT license,
  app scaffolds for Phases 7–9.

### Security

- Providers receive hostnames only — never full URLs, never user data.
- No secrets in code or fixtures; keys read from environment only
  (Phase 4 adapters, documented in `.env.example`).

[0.1.0]: https://github.com/sentiala/sentiala-shield/releases/tag/v0.1.0
