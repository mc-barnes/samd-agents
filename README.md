# SaMD Agents

Specialist reviewer agents for Claude Code, built for Software as a Medical Device (SaMD) teams.

Each agent is a deep-knowledge persona grounded in FDA guidance, ISO standards, and real submission experience. They review your artifacts and tell you what an FDA reviewer, auditor, or clinical safety expert would flag — before they do.

## Agents

| Agent | Domain | Standards |
|-------|--------|-----------|
| [regulatory-reviewer](agents/regulatory-reviewer/SKILL.md) | FDA submission readiness | IEC 62304, ISO 14971, ISO 13485, IEC 62366-1, FDA PCCP |
| [clinical-reviewer](agents/clinical-reviewer/SKILL.md) | Neonatal SpO2 clinical logic | Published literature (Bonafide et al., AAP guidelines) |
| [qa-reviewer](agents/qa-reviewer/SKILL.md) | ISO 13485 QMS compliance | ISO 13485:2016, 21 CFR 820, ISO 19011 |
| [safety-reviewer](agents/safety-reviewer/SKILL.md) | Patient safety & human factors | ISO 14971:2019, IEC 62366-1:2015+A1:2020 |
| [cybersecurity-reviewer](agents/cybersecurity-reviewer/SKILL.md) | Medical device cybersecurity | FDA Premarket Cyber Guidance (2023), Section 524B, AAMI TIR57, IEC 81001-5-1 |

## Usage

### Install as Claude Code skills

Copy or symlink the `agents/` directory into your project's `.claude/skills/agents/`:

```bash
# Option 1: Git submodule (recommended for shared repos)
git submodule add https://github.com/mc-barnes/samd-agents.git .claude/skills/agents

# Option 2: Direct copy
cp -r agents/* .claude/skills/agents/
```

### Invoke in Claude Code

Ask Claude to use a specific reviewer persona:

- "Run a regulatory review on this PRD"
- "Do a safety review of this risk analysis"
- "Review this CAPA as the QA reviewer"
- "Cybersecurity review of our threat model"
- "Clinical review of the SpO2 triage logic"

Each agent produces structured findings with verdicts, citations, and specific fix recommendations.

## Output format

Every agent follows the same pattern:

- **Verdict** — pass/fail/concern at a glance
- **Findings** — must-fix items with standard citations
- **Gaps/Observations** — should-fix items
- **Recommendations** — best practice suggestions
- **What's sound** — acknowledges what's done well
- **Disclaimer** — AI-generated, requires human validation

## License

MIT
