# Changelog

## v2.0.0 — 2026-05-02

### Added
- **VoC synthesizer agents** — theme-extractor, severity-scorer, bias-auditor (all v2.0.0)
  - Three-phase pipeline: extract themes → Kano + RICE scoring → bias audit
  - 8 bias checks including social media-specific detection (viral amplification, single-source amplification, platform demographic bias)
  - Channel tier model: structured / semi-structured / unstructured
  - Cross-channel corroboration confidence boost (+10-15%)
  - Social reach heuristics for unstructured channel scoring
- **Example outputs** — sample regulatory review and VoC panel output in `examples/`
- **Retrospective mode** for all 5 reviewers — adjusted severity for gap-analysis artifacts
- **CHANGELOG.md**

### Changed
- README restructured: quick start first, reference tables in a dedicated section
- README now documents both agent categories (reviewers + VoC)
- Repo description and GitHub topics updated

## v1.1.0 — 2026-04-25

### Changed
- regulatory-reviewer bumped to v1.1.0 — improved traceability checks, PCCP coverage
- README: added artifact routing tables, scope boundaries, output format reference

## v1.0.0 — 2026-04-20

### Added
- Initial release: 5 regulatory reviewer agents
  - regulatory-reviewer (FDA submission readiness)
  - clinical-reviewer (neonatal SpO2 clinical logic)
  - qa-reviewer (ISO 13485 QMS compliance)
  - safety-reviewer (patient safety & human factors)
  - cybersecurity-reviewer (medical device cybersecurity)
