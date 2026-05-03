# Response Bias in Qualitative VoC Research

Reference document for the bias-auditor agent. Covers common biases in qualitative feedback analysis, VoC-specific bias patterns, threshold rationale, and mitigation strategies.

## Overview of Biases in Qualitative Research

### Selection Bias
The sample of people who provide feedback is not representative of the population who experience the product. Feedback comes from people who chose to speak up — and the reasons they chose to speak up are correlated with the content of their feedback.

In VoC contexts, selection bias is pervasive and unavoidable. The goal is not to eliminate it but to understand its direction and magnitude so that findings are interpreted with appropriate confidence.

### Response Bias
Respondents systematically distort their answers in a particular direction. In VoC, this manifests as negativity bias (people are more likely to provide feedback after a negative experience than a positive one), social desirability (people in surveys may soften complaints), and acquiescence bias (people in live calls may agree with the agent's framing of the issue).

### Recency Bias
Recent events are weighted more heavily than past events, both by the people providing feedback (they remember last week's frustration more than last month's) and by the analysts interpreting it (the newest data feels more relevant). In time-series VoC data, recency bias manifests as over-reacting to spikes and under-valuing steady-state patterns.

### Availability Heuristic
Vivid, emotionally intense feedback is more memorable and receives more attention than mundane-but-frequent feedback. A single dramatic escalation story can anchor a team's perception more than 50 routine complaints about the same less-dramatic issue.

### Survivorship Bias
VoC data only captures feedback from people who are still engaged with the product. Users who churned, never activated, or quietly disengaged are absent from the sample. The feedback mix over-represents people who care enough to stay and complain — and under-represents people who left without a word.

### Confirmation Bias
Analysts (and product teams consuming the analysis) are more likely to notice and weight feedback that confirms their existing hypotheses. If the team already suspects that "navigation is confusing," they will see navigation-related quotes in ambiguous feedback where an unbiased reader might not.

---

## VoC-Specific Biases

### Vocal Minority
A small number of users generate a disproportionate volume of feedback. This often manifests at the source level: one patient advocacy blog, one social media account, or one physician practice files 60% of the tickets, generates 50% of the social mentions, and fills out 70% of the surveys. Their issues dominate the theme registry not because their issues are more important, but because their feedback volume is higher.

**Why it matters:** Product teams see "40 mentions of X" and assume it represents broad demand. But if 30 of those mentions come from 5 users responding to one source, the actual breadth is narrow. The theme might be a critical issue for that population and irrelevant to the other 95% of the user base.

**How it distorts prioritization:** Themes driven by vocal minorities score higher on raw frequency metrics, which pushes them up the priority stack. Meanwhile, themes with broad-but-shallow signal (mentioned by many sources, but only once or twice each) look less urgent by the numbers.

### Squeaky Wheel
Escalated complaints receive more organizational attention than quiet dissatisfaction. A patient who calls three times, demands a supervisor, and threatens to file a regulatory complaint generates more data points and more internal visibility than 100 patients who are equally frustrated but just... don't call back.

**Why it matters:** Escalation volume is a function of user assertiveness and channel accessibility, not issue severity. Some populations (older, less digitally literate, higher socioeconomic status) escalate more readily. The feedback mix reflects assertiveness distribution, not severity distribution.

**How it distorts prioritization:** Teams treat escalation count as a proxy for severity. It is not. Severity must be assessed independently of volume.

### Channel Selection
Different feedback channels attract different populations, and the differences are systematic:

- **Phone calls** skew toward older users, less digitally fluent, and urgent/complex issues. Callers tend to have already tried and failed at self-service. Issues surfaced in calls are the tip of the iceberg — the portion of failures that users couldn't resolve on their own.
- **Chat** skews toward younger users, digitally comfortable, and transactional/quick-resolution issues. Chatters often prefer written communication and may understate emotional intensity.
- **Surveys** skew toward engaged, moderate-sentiment users. The extremely satisfied and extremely dissatisfied are under-represented (the satisfied don't bother, the dissatisfied have already churned or escalated). Surveys also suffer from question framing effects.
- **App store reviews** skew toward extreme sentiment (1-star and 5-star), recent experiences, and mobile-specific issues.
- **Support tickets** skew toward technical issues, reproducible bugs, and users who are comfortable with written, structured communication.

**Why it matters:** If 80% of your inputs come from phone calls, your theme registry reflects "things that drive phone calls," not "things that matter to users." The themes you see are filtered through the channel's selection function.

### Escalation Bias
The issues that reach support or customer success are the subset that users couldn't self-serve. The "dark matter" is the larger set of users who struggled, failed, worked around it, or gave up — and never reached out. VoC data is inherently biased toward the visible failures. The invisible failures may be more numerous, more severe, and more consequential for retention.

**Why it matters:** A theme like "patients can't find their test results in the portal" might have 10 mentions in call data. But for every patient who called about it, there may be 50 who tapped around the app for 2 minutes, couldn't find it, and gave up. The 10 callers are the ones who cared enough (and had enough time) to pick up the phone. Product analytics (not VoC) is the right tool to size the dark matter.

**How it distorts prioritization:** Teams size opportunities based on VoC mention counts, dramatically underestimating issues where the user burden is "give up silently" rather than "call and complain."

### Source Concentration
Feedback volume per source is roughly proportional to the source's reach, engagement level, and visibility — not to the breadth or severity of the issues it surfaces. A patient advocacy blog with 50K monthly readers generates more feedback signal than a physician practice with 200 patients, and a viral TikTok post generates more comments than a month of patient call transcripts combined.

**Why it matters:** The theme registry becomes a mirror of the highest-volume sources' concerns. Lower-volume sources — which may represent broader or more clinically relevant populations — are systematically under-represented.

**How it distorts prioritization:** The roadmap optimizes for the sources with the most feedback, which are the sources with the most reach, which creates a reinforcing loop where high-reach sources get more attention, which further increases their weight in the feedback mix. Quieter sources' unaddressed issues compound silently.

### Temporal Clustering
A single event — an outage, a plan design change, a feature release, an external news story — can create a feedback spike that looks like a durable trend in the data. If the VoC analysis window happens to overlap with the spike, the event-driven themes dominate the registry.

**Why it matters:** Spikes are real signal — they tell you that an event caused pain. But they are not the same signal as a steady-state pattern. Building roadmap commitments based on a spike is like buying snow tires because of one blizzard. The right response to a spike is usually operational (incident response, communication, one-time fix), not strategic (roadmap investment).

**How it distorts prioritization:** Spikes inflate weekly_counts for the affected week, which inflates total_mentions, which inflates severity scores. A theme with 15 mentions in one week and 0 in all other weeks looks as important as a theme with 3 mentions per week for 5 weeks — but the latter is a far more durable signal.

---

## Social Media-Specific Biases

### Platform Selection Bias
Each social platform has a demographic filter that shapes who provides feedback before the auditor sees any data. TikTok users skew 18-34 and are more likely to share emotional, dramatic, or visually compelling content — the format rewards brevity and intensity, which selects for acute experiences over chronic ones. Instagram skews 25-44 and female, favoring visual/narrative storytelling that tends toward personal journeys and transformation arcs. Patient advocacy blogs skew toward health-literate, English-speaking patients with chronic conditions who have the ability, motivation, and digital fluency to write publicly about their experiences.

**Why it matters:** Each platform's selection function filters the patient population before you see any data. A theme sourced primarily from TikTok may represent the experience of younger, more digitally active patients — not the broader patient population. A theme sourced from patient advocacy blogs may represent the experience of the most engaged, health-literate subset of chronic-condition patients — not the typical patient. The platform IS a demographic filter, and the auditor must account for it.

**How it distorts prioritization:** Teams treat social media mentions as representative of the patient population. They are not. They are representative of the platform's demographic, filtered through the platform's content incentive structure.

### Engagement Amplification
High-engagement content (viral videos, trending posts) generates disproportionate response volume. One TikTok video with 500K views can produce 200+ comments, all responding to the same stimulus. These 200 comments are not 200 independent data points — they are 200 reactions to 1 stimulus. The original post's framing, emotional tone, and narrative structure prime every response. Comments on a viral post share context, anchoring, and emotional state in a way that independent feedback from separate patients does not.

**Why it matters:** Treating engagement-amplified responses as independent mentions inflates theme counts and creates false urgency. A theme with 200 social mentions that all trace to reactions on 2 viral posts has an effective breadth of 2, not 200. The volume is real — the breadth is an illusion.

**How it distorts prioritization:** Raw mention counts from social media conflate volume (how many people responded) with breadth (how many independent experiences the theme represents). Teams that prioritize by mention count will systematically over-invest in themes that went viral and under-invest in themes with broad but quiet signal.

### Advocate Amplification
Patient advocacy bloggers synthesize and amplify patient experience. One blog post referencing 50 patient stories is fundamentally different from 50 individual patient comments. The blogger's editorial lens selects, frames, and amplifies certain narratives over others. Their synthesis reflects their perspective on what matters — which may be well-informed and valuable, but is not the same as raw patient voice.

**Why it matters:** Advocacy content is a secondary source, not a primary one. The blogger has already applied selection (which stories to include), framing (how to present them), and amplification (reaching an audience that then echoes the narrative). Counting advocacy-sourced mentions alongside direct patient mentions conflates curated signal with raw signal.

**How it distorts prioritization:** A single advocate blog post can generate a cascade of social shares, comments, and follow-up posts that all reference the same curated narrative. The theme registry sees 30 mentions, but the independent primary sources may number 5-10. The advocate's editorial choices — not patient breadth — are driving the theme's score.

### Coordinated Signal / Astroturfing
Social media is susceptible to coordinated campaigns — advocacy groups, pharmaceutical interest groups, or activist organizations can generate coordinated feedback that mimics organic signal. When a theme's social mentions cluster around a single hashtag, campaign, or narrow time window, the signal may reflect organized effort rather than spontaneous patient experience.

**Why it matters:** Coordinated campaigns can create the appearance of broad organic demand where none exists. A hashtag campaign organized by an advocacy group may generate 100 posts in a week — all using the same language, referencing the same talking points, and originating from accounts that share organizational affiliation. The feedback is real (these people do hold these views), but the volume and timing are manufactured.

**How it distorts prioritization:** Teams interpret coordinated volume as organic demand. The theme looks urgent because it appeared suddenly and loudly — but the urgency is manufactured by the campaign's timing, not by a genuine shift in patient experience.

---

## Threshold Rationale

The bias-auditor uses eight default thresholds. Each is a heuristic, not a statistical test. They are designed to be sensitive enough to catch meaningful bias patterns while specific enough to avoid flooding the report with false positives.

### 50% — Source Concentration

No single source should represent more than half of any theme's signal. This threshold is deliberately generous — even in input sets with a dominant source, 50% is a high bar. Below 50%, concentration may exist but there's enough cross-source signal to support the theme's generalizability. Above 50%, the theme is more accurately described as "a thing [source] surfaced" than "a thing our patients experience broadly."

**Why not lower (e.g., 30%)?** In input sets with few sources (3-5), a 30% threshold would flag almost everything. The 50% threshold ensures flags are raised only when a single source truly dominates.

**Why not higher (e.g., 70%)?** At 70%, you've already lost most of the cross-source signal. The theme is effectively source-specific. Waiting until 70% to flag is too late — product decisions may already be underway.

### 80% — Recency Bias

A theme that is 80%+ from the most recent week has insufficient longitudinal evidence. The 80% threshold accounts for the fact that new themes will naturally have high recency (they were just discovered). The flag is not "this theme is wrong" — it's "this theme needs more time before we can trust its durability."

**Why not lower (e.g., 60%)?** New themes in their first 2-3 weeks of tracking will often have 60-70% of mentions from the most recent week simply because they're new. A 60% threshold would flag almost every new theme, creating noise.

**Why not higher (e.g., 95%)?** At 95%, you're only catching themes that literally appeared out of nowhere in one week. 80% catches the more common case: a theme that has a few historical mentions but just received a suspicious spike.

### 70% — Channel Skew

Below 70%, the primary channel dominates but there is enough cross-channel signal to have some confidence that themes aren't purely channel-specific. Above 70%, the channel IS the signal — the themes you see are filtered through the selection function of that channel.

**Why not lower (e.g., 50%)?** In many organizations, one channel (usually phone) is the primary feedback source. A 50% threshold would flag the overall sample in nearly every audit, which defeats the purpose. 70% reserves the flag for cases where the imbalance is severe enough to question whether other channels would surface the same themes.

**Why not higher (e.g., 90%)?** At 90%, you're only catching extreme monocultures. Most organizations with a channel problem are in the 70-85% range — heavily skewed but not completely single-channel.

### 3x — Persona Overrepresentation

With 4 personas at equal expected weight (25% each), the 3x threshold flags any persona above 75%. This is a rough heuristic that scales to different persona counts: with 3 personas (33% expected), the flag triggers at ~100% (effectively never — which is correct, because with 3 personas, one will always dominate somewhat). With 5 personas (20% expected), the flag triggers at 60%.

**Why 3x instead of a fixed percentage?** Fixed percentages don't scale to different persona counts. 3x is a relative measure that adapts: in a 2-persona system, 3x flags at 150% (impossible — correct, since 2 personas can't be balanced and the metric doesn't apply). In a 6-persona system, 3x flags at 50% (appropriate — one persona having 50% of signal in a 6-persona product is a real imbalance).

### 5 Mentions — Minimum Sample Size

Below 5 mentions, any distribution metric is unreliable. At N=4, one data point is 25% of the distribution. A single input from a particular client would represent "25% client concentration" — which is mathematically true but statistically meaningless. The sample size check prevents the auditor from applying concentration, recency, and persona checks to themes where the numbers are too small to support any conclusion.

**Why not lower (e.g., 3)?** At N=3, one data point is 33% of the distribution. You cannot meaningfully assess concentration when one input moves the needle by a third. Even N=5 is marginal — it's a floor, not a comfort zone.

**Why not higher (e.g., 10)?** Many legitimate emerging themes take weeks to accumulate 10 mentions. A threshold of 10 would suppress bias checks for too long, allowing biased themes to grow unchecked during their formative period. 5 is the minimum where distribution checks begin to carry weak signal.

### 70% — Platform Demographic Bias

Below 70%, there is enough cross-tier signal (a mix of structured and unstructured channel evidence) to have reasonable confidence that the theme reflects more than one demographic segment. Above 70%, the theme is primarily informed by one channel tier's demographic profile and the findings need validation against structured channels before roadmap commitment.

**Why not lower (e.g., 50%)?** Many themes will naturally have majority unstructured channel evidence simply because social media generates higher volume per-interaction than structured channels. A 50% threshold would flag nearly every theme with any social media input, creating noise. 70% reserves the flag for themes that are genuinely dominated by unstructured sources.

**Why not higher (e.g., 90%)?** At 90%, you're only catching themes with virtually no structured channel corroboration. By that point, the demographic skew is extreme and the flag is too late to be useful for early prioritization decisions.

### 50% — Single-Source Amplification

Same rationale as source concentration — if >50% of a theme's social mentions trace to one post, the "breadth" is an illusion. The effective sample size is 1 (one post) regardless of how many comments it generated. Below 50%, there is enough diversity across source posts that the theme reflects multiple independent stimuli. Above 50%, the theme is dominated by reactions to a single narrative.

**Why not lower (e.g., 30%)?** In themes with few social mentions (5-8), it's common for one post to account for 30-40% simply because there aren't many posts to distribute across. The 50% threshold avoids flagging themes where a single post has natural plurality but not dominance.

**Why not higher (e.g., 70%)?** At 70%, the theme is so heavily concentrated in one post's comment thread that the signal is effectively a single anecdote with a loud echo chamber. Waiting until 70% to flag misses the window where the distortion is already significant but might still be overlooked.

### 10x Median Engagement — Viral Amplification

Content at 10x median engagement is in the viral territory where organic response patterns break down. Below 10x, engagement-driven response is present but not dominant — the content performed well but didn't trigger the algorithmic amplification feedback loop that converts one post into a mass event. Above 10x, the response volume is driven primarily by algorithmic distribution, not by the number of patients who independently sought to share their experience.

**Why 10x instead of a fixed view count?** Platforms have different baselines. A TikTok video with 500K views is 10x the estimated median (50K); an Instagram post with 100K views is 10x its median (10K). A fixed threshold (e.g., 100K views) would under-flag on TikTok and over-flag on Instagram. The multiplier approach normalizes across platforms.

**Why not lower (e.g., 5x)?** At 5x median, content has above-average reach but is still within the range of moderately successful posts. Flagging at 5x would capture too many posts that performed well organically without triggering true viral dynamics.

---

## Mitigation Strategies by Bias Type

### Source Concentration — Mitigation

1. **Request targeted inputs from non-flagged sources.** Don't just ask for "more data" — ask for data from specific sources. Identify the top 3 sources by relevance (excluding the concentrated source) and request their most recent patient call transcripts, physician feedback, or survey responses.

2. **Weight mentions by source.** If one advocacy blog has 50 mentions and 4 other sources have 10 each, the unweighted total is 90 with that blog at 56%. A source-weighted total (each source gets equal voice regardless of volume) would be 5 source-votes, with the blog at 20%. Present both views.

3. **Check if the concentrated source's issue is structurally unique.** Sometimes concentration is real signal — the source serves a unique population, condition, or clinical context that creates a genuine issue others don't face. In that case, the right action is to tag the theme as source-specific, not to dismiss it.

4. **Establish a "source diversity" requirement for roadmap themes.** Before a theme can be prioritized for roadmap investment, require evidence from at least 2 independent sources (for strategic features) or 3 sources (for major features). This doesn't apply to bug fixes, which should be prioritized on severity regardless of breadth.

### Recency Bias — Mitigation

1. **Implement a "cooling period" for spike-driven themes.** When a theme first appears with >80% recency, tag it as "monitoring" and check again after 2 weeks. If the signal persists at a meaningful level (not necessarily the same level — even 30% of the spike volume is signal), reclassify as durable.

2. **Correlate with operational events.** Check whether the spike coincides with a known event (outage, deployment, plan design change, open enrollment). If it does, the theme is event-driven and the appropriate response is operational, not strategic.

3. **Compare to baseline.** If the theme existed before the spike, compare the spike-week volume to the prior weekly average. A theme that averages 3/week and spikes to 15 is a 5x anomaly. A theme that averages 0/week and spikes to 15 is a new phenomenon. Different response required for each.

4. **Separate event response from roadmap response.** Acknowledge the spike (it's real pain), address it operationally (communication, workaround, hotfix), but do not commit roadmap resources until longitudinal evidence is available.

### Channel Skew — Mitigation

1. **Request inputs from under-represented channels.** Be specific: "We need 20 chat transcripts from the past 2 weeks" is actionable. "We need more diverse inputs" is not.

2. **Establish a channel mix target for each analysis cycle.** For example: 40% calls, 30% chat, 20% survey, 10% other. If the actual mix deviates by more than 20 percentage points from the target, the analysis cycle should be flagged and the deviation noted in the report.

3. **Conduct channel-stratified analysis.** Run theme extraction separately for each channel and compare the resulting theme sets. Themes that appear across all channels are high-confidence. Themes that appear in only one channel may be channel-specific (which is still valuable — but it's a different insight than "all users face this").

4. **Acknowledge the limitation in the report.** When channel skew is present and cannot be mitigated within the current cycle, the audit report should include a standing caveat: "Current themes are primarily informed by [channel] inputs. Themes may under-represent issues that surface through [under-represented channels]."

### Persona Imbalance — Mitigation

1. **Seek targeted inputs from under-represented personas.** Identify the specific persona gap and request data from the appropriate source. For "physician" inputs: request physician call transcripts or clinical advisory board notes. For "caregiver" inputs: request caregiver survey responses or support group feedback. For "advocate" inputs: review patient advocacy blog content.

2. **Create persona-specific feedback mechanisms.** If a persona is chronically under-represented, the issue may be structural (that persona doesn't use the channels where feedback is collected). Design a feedback mechanism for them: a quarterly survey, a monthly check-in call, a feedback widget in their specific tool.

3. **Weight themes by persona representation.** If the theme registry is 90% patient-driven, themes that also appear in the 10% of physician/caregiver/advocate feedback are likely more important than their raw counts suggest — they've broken through the representation barrier.

4. **Flag persona-specific themes separately.** A theme that affects only one persona is still valid — but it should be tagged as persona-specific so that prioritization can account for the persona's relative size and strategic importance.

### Low Sample Size — Mitigation

1. **Do not apply distribution-based bias checks.** At N<5, concentration, recency, and persona checks produce noise, not signal. The only appropriate action is to wait for more data.

2. **Tag as "emerging" and set a review trigger.** When the theme crosses N=5, re-run the bias audit for that theme specifically.

3. **Do not suppress the theme from reports.** Low sample size means low confidence in distribution analysis, not low importance. The theme should still appear in extraction reports and severity scoring — but with an explicit confidence caveat.

4. **Track the theme's growth rate.** A theme that goes from 2 mentions to 4 mentions in one week is growing fast, even if the absolute number is below threshold. Growth rate is a meaningful signal independent of sample size.

### Temporal Clustering — Mitigation

1. **Decompose time series into trend and spike components.** If a theme has a baseline of 3/week and a spike of 20 in one week, the trend is 3/week (durable signal) and the spike is 17 (event-driven signal). Prioritize based on the trend component, respond operationally to the spike component.

2. **Require 3+ weeks of signal for roadmap commitments.** A single week of high volume, no matter how dramatic, is insufficient evidence for strategic investment. Require longitudinal evidence before committing engineering resources beyond a hotfix.

3. **Link spikes to root causes.** When a temporal cluster is identified, investigate the triggering event. Document it in the audit report so future analysts don't re-discover the same spike and mistake it for a new trend.

4. **Use week-over-week change rates, not absolute counts, for trend assessment.** A theme that grows from 3 to 5 to 7 to 9 mentions over 4 weeks is a more reliable signal than a theme that goes 0, 0, 0, 25. The former is a trend; the latter is an event.

### Platform Demographic Bias — Mitigation

1. **Cross-validate with structured channels.** When a theme is >70% sourced from unstructured channels, require corroboration from at least one structured channel (patient calls, physician calls) before committing roadmap resources. If no structured signal exists, the theme may be real but demographically narrow.

2. **Document the demographic skew in the audit report.** State explicitly which platforms contributed and what demographic filters they impose. "This theme is 80% sourced from TikTok and Instagram, which skew 18-44. Signal from patients over 50 is absent." This gives decision-makers the context to apply appropriate confidence.

3. **Establish structured-channel validation as a gate.** For themes that emerge primarily from social media, add a validation step: "Before this theme can move from 'emerging' to 'confirmed,' it must have at least 2 mentions from structured channels (patient calls, physician calls, surveys)."

4. **Adjust severity scoring for platform mix.** Themes with diverse platform representation (e.g., 40% patient calls, 30% social, 30% physician feedback) should receive higher confidence weighting than themes with mono-platform evidence, even if the mono-platform theme has higher raw mention count.

### Viral Amplification — Mitigation

1. **Discount engagement-amplified mentions proportionally.** When social mentions trace to posts with >10x median engagement, apply a discount factor. A reasonable heuristic: count the source post as 1 data point per post, regardless of comment volume. If 150 mentions trace to 3 viral posts, the effective count is 3, not 150.

2. **Separate viral signal from organic signal in the report.** Present two counts: raw mentions (including viral) and effective mentions (with viral-amplified comments collapsed to their source posts). Let decision-makers see both numbers.

3. **Check whether the viral content was organically created or manufactured.** A patient sharing their genuine experience that happened to go viral is different from a content creator manufacturing outrage for engagement. The former is real signal amplified by algorithms; the latter may be manufactured signal.

4. **Monitor for signal persistence after the viral moment fades.** Viral posts have a half-life of days to weeks. If the theme's mention rate returns to baseline after the viral post falls out of algorithmic distribution, the theme was event-driven, not durable. If mentions continue from independent sources, the viral post surfaced a real issue.

### Single-Source Amplification — Mitigation

1. **Collapse comment threads to their source post.** When >50% of social mentions trace to one post, treat the entire thread as 1 data point. The 200 comments on a viral TikTok video are 1 data point with 200 reactions, not 200 independent data points.

2. **Require independent corroboration.** Before acting on a theme dominated by single-source amplification, require mentions from at least 2 other independent posts or sources. Independent means different authors, different platforms, or different time periods — not reshares or quote-tweets of the original.

3. **Assess the source post's representativeness.** Is the source post's experience typical or unusual? A patient describing a common frustration that resonated with hundreds of commenters is different from a patient describing a rare edge case that attracted attention for its drama. The former suggests broad latent demand; the latter suggests novelty.

4. **Flag the source post's author and context.** Is the author a patient, a caregiver, a physician, an advocate, or a content creator? Each has different incentives and representativeness. Document this in the audit so decision-makers can weigh the source appropriately.

### Coordinated Signal / Astroturfing — Mitigation

1. **Check for temporal clustering of social mentions.** If a theme's social mentions cluster in a 24-48 hour window, investigate whether the spike was driven by an organized campaign (shared hashtag, campaign URL, or advocacy group call-to-action).

2. **Check for language similarity.** Coordinated campaigns often use shared talking points, hashtags, or template language. If multiple social mentions use near-identical phrasing, flag as potentially coordinated.

3. **Trace mentions to their origin.** If social mentions share a common upstream source (a campaign email, an advocacy group post, or a coordinated social media action), the effective independent count is 1 (the campaign), not N (the number of participants).

4. **Separate coordinated signal from organic signal in the report.** Present coordinated mentions separately and note the organizing entity. The signal may still be valid (the advocacy group may represent real patient concerns), but the volume is manufactured and should not be treated as organic demand.
