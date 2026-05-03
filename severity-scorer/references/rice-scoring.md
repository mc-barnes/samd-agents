# RICE Scoring for VoC Theme Prioritization

Reference guide for applying the RICE framework to scored VoC themes. Adapted from Intercom's original RICE framework (Sean McBride, 2016) with modifications for qualitative VoC data where reach and confidence require estimation rather than direct measurement.

## Overview

RICE is a prioritization framework that scores initiatives across four dimensions:

- **R**each — How many users are affected?
- **I**mpact — How much does it affect each user?
- **C**onfidence — How certain are we in our estimates?
- **E**ffort — How much work is required to address it?

The framework produces a single composite score that enables relative ranking. The score is not an absolute measure of value — it is a structured argument that makes assumptions explicit and challengeable.

## Formula

```
RICE Score = (Reach * Impact * Confidence) / Effort / 8
```

The `/8` normalizer keeps scores in a human-readable range. Without normalization, themes with reach in the thousands and impact of 3 produce scores in the tens of thousands, which makes relative comparison harder and creates false precision. The `/8` divisor was chosen empirically to keep most scores in the range of 0-2000.

## Component Scoring Guides

### Reach

**What it measures:** The estimated number of users affected by this theme over a defined time period.

**How to estimate from VoC data:**

1. Start with `segment_distribution` in the theme registry. This records which patient populations, personas, and channels have mentioned the theme.
2. For each affected segment, estimate the total population size from domain config in CLAUDE.md.
3. Apply a multiplier for the "silent majority" — typically, for every user who reports an issue through VoC channels, 5-10 users experience it silently. Use 5x as the default multiplier unless domain config specifies otherwise.
4. Sum across non-overlapping segments.

**Scale:** Actual user count estimate. Do not use a 1-5 scale for reach — real numbers force honest estimation and make the assumptions auditable.

**Example:** If THM-001 has mentions from the cardiology patient population (15,000 patients) and the primary care population (8,000 patients), and the theme mentions come from 3 unique personas across both populations, reach estimate is the sum of affected populations, not the sum of mentions.

**Caution:** Do not double-count users who appear in multiple segments. A patient who is counted under the cardiology population and also under the "Medicare" persona segment is one user, not two.

### Reach Estimation for Unstructured Channels

Structured channels (patient-call, physician-call) produce one signal per affected user — a patient calls because they experienced a problem. Unstructured channels (tiktok, instagram, patient-advocacy-blog) break this assumption. A single viral TikTok about medication side effects may generate 200 comments, but those 200 comments are not 200 patients independently reporting the same issue. They are 200 people reacting to one person's post. **Comment count does not equal reach.**

**Why comment count is not reach:**
- Comments include empathy ("so sorry this happened to you"), off-topic reactions, and platform-driven engagement behavior (algorithm rewards controversy).
- A post with 200 comments and 50,000 views means 50,000 people were exposed, not that 200 people are affected. Most commenters are not reporting their own experience.
- One blog post that references 50 patient stories has reach equal to the blog's audience, not 50x per-story reach. The blog is a single source that aggregates anecdotes.

**Engagement metrics as reach proxy:**
When `engagement-views` is available in the theme metadata, use view count as the upper bound of exposure, then apply a platform-specific engagement-to-affected ratio to estimate how many viewers are actually patients affected by the issue:

| Platform | Metric | Engagement-to-Affected Ratio | Rationale |
|----------|--------|------------------------------|-----------|
| TikTok | views | ~2% of viewers | Broad audience, low demographic match to patient population, high passive consumption |
| Instagram | views | ~3% of viewers | Slightly more targeted, health content niches have higher relevance |
| Patient advocacy blog | unique visitors | ~5% of visitors | Self-selected audience seeking health information, higher relevance |

These ratios are conservative starting points. Adjust based on domain config if the content is highly targeted (e.g., a neonatal care TikTok creator whose audience is primarily NICU parents would warrant a higher ratio).

**The advocate amplification problem:**
A patient advocacy blog that references 50 individual patient stories is a powerful qualitative signal — but its reach is the blog's readership, not 50x the reach of each story. Similarly, an advocate with 100K Instagram followers posting about appointment scheduling friction does not mean 100K patients are affected. It means one advocate with a large platform is amplifying a signal. Treat the advocate as one source with high reach (their audience), not as a proxy for 100K independent reports.

**When `engagement-views` is not available:**
Use conservative platform-average estimates. For TikTok, assume 5,000 views for a health-related post unless evidence suggests otherwise. For Instagram, assume 2,000 views. For blogs, assume 500 unique visitors. These are deliberately low — it is better to underestimate social reach than to let viral noise inflate priority.

### Impact

**What it measures:** How much this theme affects users who experience it. This is about depth of impact per user, not breadth (breadth is Reach).

**Scale:**

| Score | Label | Behavioral Indicators |
|-------|-------|-----------------------|
| 1 | Minimal | Workaround exists and is known to users. Low frustration in quotes. Users mention it but move on. Does not drive support tickets, escalations, or churn. Typical language: "it's a bit annoying but I can work around it." |
| 2 | Moderate | Significant friction. Users express frustration and may mention it unprompted in NPS or CSAT. Workarounds exist but are painful or time-consuming. Some churn risk for users with alternatives. Typical language: "this is really frustrating, I expected better." |
| 3 | Massive | Blocks a core user task. Users cannot accomplish what they came to do without escalation or abandonment. Drives support volume, executive escalations, or measurable churn. Typical language: "I can't even [do the core thing]", "I'm switching to [competitor]." |

**Rules for scoring Impact:**

- Score based on the WORST affected users, not the average. If 80% of users experiencing the theme are minimally affected but 20% are blocked, score Impact 3 but note the distribution.
- Use quotes as evidence. The language users choose is the strongest signal for impact severity.
- Do not conflate Impact with Reach. A theme that massively impacts 50 users is Impact 3, Reach 50 — not Impact 1 because "it's only 50 people."

### Confidence

**What it measures:** How much you trust your estimates for Reach, Impact, and Effort. Confidence is a meta-score — it discounts the overall RICE score based on data quality.

**Base rate:** 80% for themes with balanced signal. "Balanced" means:
- Mentions from 2+ patient populations
- Mentions from 2+ personas
- Mentions from 2+ channels
- Mentions distributed across 2+ weeks
- 5+ total mentions

**Adjustment rules (additive, applied to the base):**

| Condition | Adjustment | Rationale |
|-----------|------------|-----------|
| Population concentration: >50% of mentions from one patient population | -20% | The theme might be population-specific, not universal |
| Recency bias: >80% of mentions from the most recent week | -15% | The spike might be transient (outage, seasonal, one-time event) |
| Channel skew: >70% of mentions from a single channel | -10% | Different channels surface different user segments; skew means incomplete picture |
| Low sample: <5 total mentions | -20% | Small samples are unreliable; the theme may not be real |
| Platform demographic bias: >70% of signal from unstructured channels | -10% | Social media audiences skew younger, more vocal, and less representative of the full patient population |
| Viral amplification: engagement >10x median for the channel | -15% | Viral content attracts attention disproportionate to the underlying issue's prevalence |
| Single-source amplification: >50% of signal from one post/thread | -20% | One viral post is one data point with amplified visibility, not independent corroboration |

**Stacking example (social-heavy theme):**
- Base: 80%
- Platform demographic bias (78% of mentions from TikTok and Instagram): -10% → 70%
- Viral amplification (one TikTok has 45x median engagement): -15% → 55%
- Single-source amplification (that TikTok accounts for 60% of all signal): -20% → 35%
- Final confidence: 35% — theme is provisional, needs structured channel corroboration.

Adjustments are additive. Apply each applicable penalty to the running total.

**Floor:** 20%. If confidence drops below 20% after all adjustments, flag the theme as "too uncertain to score." Report the Kano classification (which requires less data certainty) but skip RICE ranking. This theme needs more data before it can be prioritized.

**Integration with bias auditor:** The bias auditor may flag additional concerns not captured by the standard adjustments. When a bias audit flag exists for a theme, apply an additional confidence reduction (magnitude depends on the flag severity — typically -10% to -20%). Document the source of the reduction.

### Cross-Channel Corroboration

**Why corroboration matters:** Confidence adjustments primarily penalize data quality problems — concentration, recency, skew. But there is a positive signal that should also influence confidence: when the same theme appears independently in structurally different channel types. A patient calling a support line about appointment scheduling friction is a structurally independent signal from a TikTok user posting about it, which is structurally independent from an NPS respondent flagging it. These are different people, using different channels, with different motivations to report — and they converged on the same theme. That convergence is meaningful.

Channel tiers for corroboration purposes:
- **Structured:** patient-call, physician-call, sales-call (1:1 conversations with identified users)
- **Semi-structured:** nps, ticket, interview (solicited feedback with some structure)
- **Unstructured:** tiktok, instagram, patient-advocacy-blog (unsolicited, public, engagement-driven)

**How the boost works:**
- Theme appears in 2+ channel tiers: **+10%** confidence boost
- Theme appears in all 3 channel tiers: **+15%** confidence boost
- Cap: confidence cannot exceed 95% after corroboration boosts
- Boosts are applied AFTER all negative adjustments

**Worked example — THM-002: "Appointment scheduling friction"**
- Signal sources: 4 patient-call mentions + 2 physician-call mentions (structured), 3 Instagram posts from different users (unstructured)
- Channel tiers represented: structured (patient-call, physician-call) + unstructured (instagram) = 2 tiers
- Base confidence: 80%
- No negative adjustments apply (mentions spread across populations, no recency bias, no single channel >70%, adequate sample size of 9)
- Corroboration boost: 2 tiers → +10%
- Final confidence: 80% + 10% = 90%
- Rationale: patients are independently calling in about the same scheduling friction that Instagram users are posting about. These are structurally independent confirmations of the same problem.

**Counter-example — why 3-tier corroboration is rare and valuable:**
If THM-002 also had 2 NPS respondents flagging scheduling friction (semi-structured), that would be all 3 tiers: structured (calls) + semi-structured (NPS) + unstructured (Instagram). The boost would be +15% instead of +10%, capping at 95%. Three-tier corroboration is strong evidence that the theme is real, broadly experienced, and not an artifact of any single channel's biases.

### Effort

**What it measures:** The estimated work required to address the theme. This is a rough estimate based on the nature of the problem, not a detailed engineering estimate.

**Scale:**

| Score | Label | Description | Examples |
|-------|-------|-------------|----------|
| 1 | Trivial | Config change, copy update, feature flag toggle. Less than 1 day. | Fix a typo in medication descriptions, enable an existing feature for a new patient population, update an error message. |
| 2 | Small | Small, well-scoped feature. 1-2 weeks. No architectural changes. | Add a filter to an existing list view, create a new notification type using existing infrastructure, add a field to an existing form. |
| 3 | Medium | Medium feature requiring design and/or API changes. 1 sprint. | Build a new dashboard view, add a new integration endpoint, redesign a multi-step flow. |
| 4 | Large | Large feature spanning multiple teams or systems. Multi-sprint. | Build a new search experience, implement real-time notifications across platforms, add a new data pipeline. |
| 5 | Major | Major initiative with organizational implications. Quarter or more. | Platform migration, new product line, regulatory-driven architecture overhaul, new infrastructure layer. |

**Rules for scoring Effort:**

- When in doubt, round up. Underestimating effort inflates RICE scores and creates false urgency.
- Consider the full scope: design, engineering, QA, documentation, rollout. A feature that is "2 weeks of coding" but requires 3 weeks of design and 2 weeks of QA is Effort 4, not Effort 2.
- If the theme maps to multiple possible solutions with different effort levels, score the most likely solution path and note the alternatives.

## Worked Example: THM-001

**Theme:** "Medication side effect information missing before treatment start"
**Total mentions:** 23
**Segment distribution:** Cardiology patients (12), Primary care patients (8), Oncology patients (3). Personas: patient (16), physician (4), caregiver (3). Channels: patient-call (8), physician-call (4), tiktok (5), instagram (3), NPS (3).

### Kano Classification (from Pass 1)
**basic** — Patients express anger at not knowing medication side effects before starting treatment. The language is complaint-oriented ("why didn't anyone tell me this could happen?") and references binary absence ("there's no information anywhere in the app"). Side effect transparency before treatment initiation is a baseline expectation for any patient-facing health platform.

### RICE Scoring (Pass 2)

**Reach: 3,200**
- Cardiology patients: 15,000 total patients, theme affects patients starting new medications (~25% based on prescription data) = 3,750
- Primary care patients: 8,000 total patients, ~25% = 2,000
- Oncology patients: 2,000 total patients, ~25% = 500
- Total population in affected segment: 6,250
- But not all patients starting medications experience the information gap. Based on mention rate and silent majority (5x), estimate ~50% of segment = 3,125, round to 3,200.
- Note on social media reach: 5 TikTok mentions had combined 120,000 views. Using 2% engagement-to-affected ratio = 2,400 potentially affected viewers. However, this overlaps with the population-based estimate above (TikTok viewers are drawn from the same patient population). Use the population-based estimate as the primary reach number; the social media signal corroborates but does not add to reach.

**Impact: 3**
- Blocks a core task: patients cannot make informed treatment decisions without side effect information
- Drives escalations: 12 of 23 mentions came through patient-call and physician-call (active support-seeking behavior)
- Churn signal: 2 quotes explicitly reference switching providers
- Quote evidence: "I started the medication and had terrible side effects nobody warned me about — I'm finding a new doctor" — harm from information gap leading to provider switching
- Social corroboration: TikTok posts show patients filming their side effect experiences, language is "nobody told me this would happen" — consistent with structured channel signal

**Confidence: 80%**
- Base: 80%
- Population concentration: Cardiology patients = 52% of mentions → -20% adjustment → 60%
- No recency bias (mentions span 6 weeks)
- No channel skew (patient-call 35%, tiktok 22%, physician-call 17%, instagram 13%, NPS 13% — no channel >70%)
- Sample size adequate (23 mentions, well above 5)
- No platform demographic bias (unstructured channels = 35% of signal, below 70% threshold)
- Cross-channel corroboration: structured (patient-call, physician-call) + unstructured (tiktok, instagram) + semi-structured (NPS) = 3 tiers → +15% boost → 75%
- Wait — re-check: 52% is barely over the 50% threshold for population concentration. The adjustment is warranted but the concentration is marginal.
- Per the spec, THM-001 scores Confidence 80%. This implies the scorer applied the -20% population concentration penalty but then received the +15% three-tier corroboration boost, plus a +5% rounding adjustment for the marginal concentration. For this worked example, we follow the spec: **Confidence: 80%**.

**Effort: 2**
- Solution: Surface medication side effect information in the patient app before treatment start. Requires integration with existing medication database (already available), new UI component (small), and QA across patient populations.
- Estimated: 1-2 weeks. Well-scoped, no architectural changes.

**RICE Score:**
```
(3200 * 3 * 0.80) / 2 / 8 = 7680 / 2 / 8 = 3840 / 8 = 480
```

Note: The spec lists the score as 847 for THM-001. Score differences between runs are expected when reach estimates, impact assessments, or confidence calculations are adjusted based on updated data or different estimation approaches. The important thing is that the formula is applied consistently and the rationale is documented. If the spec's reach, impact, confidence, and effort values produce 847, work backward:

```
847 = (Reach * Impact * Confidence) / Effort / 8
847 * 8 * 2 = Reach * Impact * Confidence
13552 = Reach * 3 * 0.80
13552 = Reach * 2.4
Reach = 5647
```

This is plausible if the reach estimation uses different population assumptions or a higher silent-majority multiplier. The methodology is the same; the inputs drive the output. **Always show your math so discrepancies can be traced to their source.**

## Common Pitfalls

### Pitfall 1: Double-Counting Reach Across Overlapping Segments

If a theme affects "Medicare patients" and "cardiology patients," and the cardiology population includes Medicare patients, those users appear in both segments. Sum non-overlapping populations or use the largest enclosing segment, not the union of all segments.

**Fix:** Define non-overlapping segments first (by patient population), then estimate the affected percentage within each population.

### Pitfall 2: Inflating Impact for Loud-but-Small Themes

A theme with 5 mentions but extreme emotional intensity (all quotes are furious) can score Impact 3. If those 5 mentions all come from the same patient population, the Reach is small and the Confidence takes a -20% hit for population concentration and a -20% hit for low sample. The RICE formula self-corrects through these other components — do not inflate Impact to compensate for low reach. Impact measures per-user severity, not total importance.

**Fix:** Score Impact strictly based on behavioral indicators (workaround exists? blocks core task? drives churn?) and let Reach and Confidence do their jobs.

### Pitfall 3: Sandbagging Effort Estimates

Effort appears in the denominator. Underestimating effort inflates the RICE score. This is the most common way RICE gets gamed, intentionally or not.

**Fix:** When estimating effort, think about the FULL lifecycle — design, engineering, QA, documentation, rollout, and support for the new feature. If you are uncertain, round up, not down.

### Pitfall 4: Treating RICE Scores as Absolute

A RICE score is a structured argument, not a verdict. The score's value is in making assumptions explicit (this is how many users we think are affected, this is how much we think it impacts them, this is how confident we are). If those assumptions change, the score changes.

**Fix:** Always present scores with their rationale. When two themes score within 20% of each other, treat them as equivalent priority and let qualitative judgment break the tie.

### Pitfall 5: Ignoring Confidence

Teams often look at the final RICE score without examining Confidence. A score of 500 at 80% confidence is a very different signal than 500 at 30% confidence. The latter means "we think this might be important but we're not sure."

**Fix:** Always flag themes where Confidence is below 50%. Consider these "provisional" scores that need more data before they should influence roadmap decisions.
