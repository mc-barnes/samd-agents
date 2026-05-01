# SaMD Agents

Specialist reviewer agents for Claude Code, built for Software as a Medical Device (SaMD) teams.

Each agent is a deep-knowledge persona grounded in FDA guidance, ISO standards, and real submission experience. They review your artifacts and tell you what an FDA reviewer, auditor, or clinical safety expert would flag — before they do.

> **Jurisdiction:** FDA only. EU MDR support planned for a future release.

## Agents

| Agent | Version | Domain | Standards |
|-------|---------|--------|-----------|
| [regulatory-reviewer](regulatory-reviewer/SKILL.md) | 1.1.0 | FDA submission readiness (9 review dimensions) | IEC 62304:2006+A1:2015, ISO 14971:2019, ISO 13485:2016, IEC 62366-1:2015+A1:2020, FDA PCCP |
| [clinical-reviewer](clinical-reviewer/SKILL.md) | 1.0.0 | Neonatal SpO2 clinical logic (6 review dimensions) | Published literature (Bonafide et al., AAP guidelines) |
| [qa-reviewer](qa-reviewer/SKILL.md) | 1.0.0 | ISO 13485 QMS compliance (8 review dimensions) | ISO 13485:2016, 21 CFR 820, ISO 19011 |
| [safety-reviewer](safety-reviewer/SKILL.md) | 1.0.0 | Patient safety & human factors (7 review dimensions) | ISO 14971:2019, IEC 62366-1:2015+A1:2020 |
| [cybersecurity-reviewer](cybersecurity-reviewer/SKILL.md) | 1.0.0 | Medical device cybersecurity (8 review dimensions) | FDA Premarket Cyber Guidance (June 2025), Section 524B, AAMI TIR57, IEC 81001-5-1:2021 |

> **Note:** The clinical-reviewer is specifically a neonatal pulse oximetry expert (SpO2 thresholds, alarm fatigue, SatSeconds, Owlet validation studies). It does not cover general clinical domains.

### Scope boundaries

Where agents share standards coverage, one agent owns the deep review and the other performs structural checks:

| Standard | Canonical owner | Other agents |
|----------|----------------|--------------|
| ISO 14971:2019 (risk management) | **safety-reviewer** — clinical adequacy of risk judgments, AFAP rationale, cumulative risk | regulatory-reviewer — structural presence check; cybersecurity-reviewer — security risk integration with 14971 |
| IEC 62366-1:2015+A1:2020 (usability) | **safety-reviewer** — use-related risk, foreseeable misuse, human factors | regulatory-reviewer — checks usability records exist in traceability |
| ISO 13485:2016 (QMS) | **qa-reviewer** — CAPA, document control, audit readiness | regulatory-reviewer — checks QMS artifacts referenced in submission |

### Artifact routing

Use this table to decide which agent to send a document to:

| Artifact | Primary reviewer | Secondary |
|----------|-----------------|-----------|
| PRD / intended use | regulatory-reviewer | clinical-reviewer (if SpO2 domain) |
| Design controls / traceability matrix | regulatory-reviewer | — |
| Risk analysis / FMEA | safety-reviewer | regulatory-reviewer (structural) |
| Usability engineering file | safety-reviewer | — |
| CAPA record | qa-reviewer | — |
| Complaint file | qa-reviewer | — |
| Audit prep / internal audit | qa-reviewer | — |
| Threat model | cybersecurity-reviewer | — |
| SBOM | cybersecurity-reviewer | — |
| Security architecture | cybersecurity-reviewer | — |
| SpO2 algorithm / alarm logic | clinical-reviewer | safety-reviewer |
| Change request | regulatory-reviewer | safety-reviewer (if safety-related) |
| 510(k) / De Novo submission | regulatory-reviewer | cybersecurity-reviewer (Section 524B) |

## Usage

### Install as Claude Code skills

Add this repo as a submodule or copy the agent directories into your project's `.claude/skills/agents/`:

```bash
# Option 1: Git submodule (recommended for shared repos)
git submodule add https://github.com/mc-barnes/samd-agents.git .claude/skills/agents

# Option 2: Direct copy
cp -r regulatory-reviewer clinical-reviewer qa-reviewer safety-reviewer cybersecurity-reviewer \
  your-project/.claude/skills/agents/
```

### Invoke in Claude Code

Ask Claude to use a specific reviewer persona:

- "Run a regulatory review on this PRD"
- "Do a safety review of this risk analysis"
- "Review this CAPA as the QA reviewer"
- "Cybersecurity review of our threat model"
- "Clinical review of the SpO2 triage logic"

Each agent produces structured findings with verdicts, citations, and specific fix recommendations.

### Panel review

For thorough coverage, run multiple agents against the same artifact. Example for a risk analysis file:

- "Run safety-reviewer and regulatory-reviewer on this risk analysis"
- "Review this submission package with regulatory-reviewer and cybersecurity-reviewer"

The safety-reviewer provides clinical adequacy of risk judgments while the regulatory-reviewer checks structural completeness — both perspectives are needed for submission readiness.

## Output format

Every agent produces structured output with a verdict, classified findings, and a disclaimer. The specific sections and verdict levels vary by domain:

| Agent | Verdict levels | Finding sections |
|-------|---------------|-----------------|
| regulatory-reviewer | ACCEPTABLE / NEEDS REVISION / NOT SUBMITTABLE | BLOCKERS, WARNINGS, SUGGESTIONS |
| clinical-reviewer | ACCEPTABLE / NEEDS REVISION / CLINICALLY UNSAFE | Clinical Concerns, Threshold & Accuracy Issues, Handoff Assessment, Recommendations |
| qa-reviewer | AUDIT-READY / NEEDS REMEDIATION / NOT AUDIT-READY | FINDINGS, OBSERVATIONS, NOTES |
| safety-reviewer | ACCEPTABLE / NEEDS REVISION / SAFETY CONCERN | SAFETY FINDINGS, GAPS, RECOMMENDATIONS |
| cybersecurity-reviewer | ACCEPTABLE / NEEDS REVISION / SECURITY CONCERN | SECURITY FINDINGS, GAPS, RECOMMENDATIONS |

All findings cite specific standard clauses or FDA guidance sections. All output includes a disclaimer that results are AI-generated and require human validation.

## License

MIT
