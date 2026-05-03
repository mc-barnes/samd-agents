# Changelog

## v2.1.0 — 2026-05-02

### Removed
- **VoC synthesizer agents** (theme-extractor, severity-scorer, bias-auditor) moved to [voc-synthesizer](https://github.com/mc-barnes/voc-synthesizer) where they belong — tightly coupled to that project's directory structure and schema

### Changed
- README rewritten as reviewers-only — cleaner scope, focused narrative
- Repo description updated to reflect reviewer-only focus

## v2.0.0 — 2026-05-02

### Added
- VoC synthesizer agents (later removed in v2.1.0)
- Example outputs in `examples/`
- Retrospective mode for all 5 reviewers
- CHANGELOG.md

### Changed
- README restructured with quick start section

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
