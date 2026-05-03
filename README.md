# SaMD Agents

Specialist agents for Claude Code, built for Software as a Medical Device (SaMD) teams.

Two categories: **regulatory reviewers** (5) grounded in FDA guidance and ISO standards, and **VoC synthesizers** (3) that turn raw qualitative feedback into defensible, prioritized insight backlogs.

> **Jurisdiction (reviewers):** FDA only. EU MDR support planned for a future release.

## Quick start

### Install

Add this repo as a submodule or copy agent directories into your project's `.claude/skills/agents/`:

```bash
# Option 1: Git submodule (recommended)
git submodule add https://github.com/mc-barnes/samd-agents.git .claude/skills/agents

# Option 2: Direct copy (reviewers only)
cp -r regulatory-reviewer clinical-reviewer qa-reviewer safety-reviewer cybersecurity-reviewer \
  your-project/.claude/skills/agents/

# Option 3: Direct copy (VoC agents only)
cp -r theme-extractor severity-scorer bias-auditor \
  your-project/.claude/skills/agents/
```

### Use

**Reviewers** — point a reviewer at any SaMD artifact:

```
"Run a regulatory review on this PRD"
"Do a safety review of this risk analysis"
"Cybersecurity review of our threat model"
```

**VoC agents** — run individually or as a panel:

```
"Extract themes from the inputs"
"Score themes"
"Run voc panel"                        ← runs all three sequentially
```

### Example output

See [`examples/`](examples/) for sample outputs:
- [Regulatory review output](examples/reviewer-output.md) — regulatory-reviewer on a neonatal SpO2 PRD
- [VoC panel output](examples/voc-panel-output.md) — theme extraction → severity scoring → bias audit

---

## Regulatory Reviewers

Each reviewer is a deep-knowledge persona grounded in real submission experience. They review your artifacts and tell you what an FDA reviewer, auditor, or clinical safety expert would flag — before they do.

| Agent | Version | Domain | Standards |
|-------|---------|--------|-----------|
| [regulatory-reviewer](regulatory-reviewer/SKILL.md) | 1.1.0 | FDA submission readiness (9 review dimensions) | IEC 62304:2006+A1:2015, ISO 14971:2019, ISO 13485:2016, IEC 62366-1:2015+A1:2020, FDA PCCP |
| [clinical-reviewer](clinical-reviewer/SKILL.md) | 1.0.0 | Neonatal SpO2 clinical logic (6 review dimensions) | Published literature (Bonafide et al., AAP guidelines) |
| [qa-reviewer](qa-reviewer/SKILL.md) | 1.0.0 | ISO 13485 QMS compliance (8 review dimensions) | ISO 13485:2016, 21 CFR 820, ISO 19011 |
| [safety-reviewer](safety-reviewer/SKILL.md) | 1.0.0 | Patient safety & human factors (7 review dimensions) | ISO 14971:2019, IEC 62366-1:2015+A1:2020 |
| [cybersecurity-reviewer](cybersecurity-reviewer/SKILL.md) | 1.0.0 | Medical device cybersecurity (8 review dimensions) | FDA Premarket Cyber Guidance (June 2025), Section 524B, AAMI TIR57, IEC 81001-5-1:2021 |

> **Note:** The clinical-reviewer is specifically a neonatal pulse oximetry expert (SpO2 thresholds, alarm fatigue, SatSeconds, Owlet validation studies). It does not cover general clinical domains.

### Panel review

Run multiple reviewers against the same artifact:

- "Run safety-reviewer and regulatory-reviewer on this risk analysis"
- "Review this submission package with regulatory-reviewer and cybersecurity-reviewer"

### Reviewer output format

| Agent | Verdict levels | Finding sections |
|-------|---------------|-----------------|
| regulatory-reviewer | ACCEPTABLE / NEEDS REVISION / NOT SUBMITTABLE | BLOCKERS, WARNINGS, SUGGESTIONS |
| clinical-reviewer | ACCEPTABLE / NEEDS REVISION / CLINICALLY UNSAFE | Clinical Concerns, Threshold & Accuracy Issues, Handoff Assessment, Recommendations |
| qa-reviewer | AUDIT-READY / NEEDS REMEDIATION / NOT AUDIT-READY | FINDINGS, OBSERVATIONS, NOTES |
| safety-reviewer | ACCEPTABLE / NEEDS REVISION / SAFETY CONCERN | SAFETY FINDINGS, GAPS, RECOMMENDATIONS |
| cybersecurity-reviewer | ACCEPTABLE / NEEDS REVISION / SECURITY CONCERN | SECURITY FINDINGS, GAPS, RECOMMENDATIONS |

All findings cite specific standard clauses or FDA guidance sections.

---

## VoC Synthesizer Agents

Three specialist agents that process raw qualitative feedback into a prioritized insight backlog. They run sequentially as a panel: extract → score → audit.

| Agent | Version | Domain | Triggers |
|-------|---------|--------|----------|
| [theme-extractor](theme-extractor/SKILL.md) | 2.0.0 | Qualitative thematic analysis (Braun & Clarke) | "extract themes", "run theme extraction", "process inputs" |
| [severity-scorer](severity-scorer/SKILL.md) | 2.0.0 | Prioritization (Kano classification + RICE scoring) | "score themes", "run severity scoring", "prioritize themes" |
| [bias-auditor](bias-auditor/SKILL.md) | 2.0.0 | Research methodology / bias detection (8 checks) | "audit bias", "run bias audit", "check for bias" |

### Prerequisites

VoC agents expect your project to have this directory structure:

```
your-project/
├── inputs/          ← Raw feedback docs (markdown with YAML frontmatter)
├── themes/          ← Theme registry (_registry.yaml) + individual theme docs (THM-*.md)
├── audits/          ← Bias audit reports (written by bias-auditor)
└── .claude/skills/agents/   ← This repo
```

Each input requires YAML frontmatter with at minimum: `type: input`, `channel`, `persona`, `date`. See the [VoC Synthesizer](https://github.com/mc-barnes/samd-os) companion project for a complete working setup with input templates and example data.

### VoC pipeline

```
1. theme-extractor    Process unprocessed inputs → extract themes with verbatim quotes
         │
         ▼
2. severity-scorer    Classify (Kano) + score (RICE) with social reach heuristics
         │
         ▼
3. bias-auditor       8 bias checks including social media-specific detection
```

Trigger the full panel with: "run voc panel" or "synthesize feedback"

### VoC output format

| Agent | Output | Key sections |
|-------|--------|-------------|
| theme-extractor | Theme Extraction Report | New themes, updated themes, merge proposals, quotes captured, processing summary |
| severity-scorer | Severity Scoring Report | Kano classification table, RICE prioritization table, scoring notes, confidence warnings |
| bias-auditor | Bias Audit Report (verdict: CLEAN / BIAS FLAGS RAISED) | Numbered findings (BA-nnn), systemic patterns, "What Looks Sound", sample composition table |

### Channel tiers

Input channels are organized into tiers that affect reach estimation, confidence scoring, and signal quality:

| Tier | Channels | Characteristics |
|------|----------|----------------|
| **Structured** | patient-call, physician-call, sales-call | Full attribution, rich context, low volume |
| **Semi-structured** | nps, ticket, interview | Some attribution, moderate context |
| **Unstructured** | tiktok, instagram, patient-advocacy-blog | Public, anonymous, high volume, weak attribution |

Cross-channel corroboration (signal appearing in 2+ tiers) boosts confidence by +10-15%.

### Bias checks

The bias-auditor runs 8 checks across two categories:

**Per-theme checks:**
- Source concentration (>50% from one source)
- Recency bias (>80% from most recent week)
- Sample size (<5 mentions)
- Platform demographic bias (>70% from unstructured channels)
- Viral amplification (engagement >10x platform median)
- Single-source amplification (>50% social mentions from one post)

**Overall checks:**
- Channel skew (>70% from a single channel)
- Persona imbalance (any persona >3x overrepresented)

---

## Reference

### Artifact routing

Use this table to decide which agent to send a document to.

**Regulatory artifacts:**

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

**VoC artifacts:**

| Input Type | Primary agent | Notes |
|------------|--------------|-------|
| Patient call transcripts | theme-extractor | After transcript-cleaner skill prepares them |
| Physician call notes | theme-extractor | Requires valid frontmatter |
| TikTok / Instagram posts | theme-extractor | After transcript-cleaner social mode; check `source-post-id` |
| Patient advocacy blog posts | theme-extractor | After transcript-cleaner blog mode; may produce sub-inputs |
| NPS verbatims / tickets | theme-extractor | Requires valid frontmatter |
| Populated theme registry | severity-scorer | After extraction |
| Scored themes | bias-auditor | After scoring |

### Scope boundaries

**Reviewers** — where reviewers share standards coverage, one owns the deep review and the other performs structural checks:

| Standard | Canonical owner | Other agents |
|----------|----------------|--------------|
| ISO 14971:2019 (risk management) | **safety-reviewer** — clinical adequacy of risk judgments, AFAP rationale, cumulative risk | regulatory-reviewer — structural presence check; cybersecurity-reviewer — security risk integration with 14971 |
| IEC 62366-1:2015+A1:2020 (usability) | **safety-reviewer** — use-related risk, foreseeable misuse, human factors | regulatory-reviewer — checks usability records exist in traceability |
| ISO 13485:2016 (QMS) | **qa-reviewer** — CAPA, document control, audit readiness | regulatory-reviewer — checks QMS artifacts referenced in submission |

**VoC agents** — each agent owns a distinct phase, no overlap:

| Phase | Owner | Reads | Writes |
|-------|-------|-------|--------|
| Theme identification & deduplication | **theme-extractor** | `inputs/`, `themes/_registry.yaml` | `themes/_registry.yaml`, `themes/THM-*.md`, input frontmatter |
| Kano classification + RICE scoring | **severity-scorer** | `themes/_registry.yaml`, `themes/THM-*.md` | `themes/_registry.yaml` (scores), `themes/THM-*.md` (score sections) |
| Bias detection & sample analysis | **bias-auditor** | `themes/_registry.yaml`, `inputs/` frontmatter | Read-only. Outputs to `audits/` |

---

All output includes a disclaimer that results are AI-generated and require human validation.

## License

MIT
