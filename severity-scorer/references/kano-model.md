# Kano Model for VoC Classification

Reference guide for applying the Kano model to qualitative Voice-of-Customer data. Adapted from Noriaki Kano's original 1984 framework for use in product contexts where survey-based classification is not available.

## Overview

The Kano model classifies customer needs into categories based on their relationship to satisfaction. The key insight is that **not all needs behave the same way** — some cause dissatisfaction when absent but not satisfaction when present, while others create delight when present but no dissatisfaction when absent. Understanding the category changes how you respond to the need.

## The Five Categories

### Basic (Must-Be)

**Definition:** Expected functionality. Absence causes dissatisfaction; presence is taken for granted. These are table-stakes requirements — users assume they exist and only notice when they are missing.

**Satisfaction curve:** Asymmetric. Fulfillment brings satisfaction up to neutral (zero), but never above. Under-delivery causes sharp dissatisfaction. Over-delivery has no upside.

**Product implication:** Fix basic gaps before investing in performance or delighters. A basic gap is a hole in the boat — no amount of sail improvement matters while you are sinking.

### Performance (One-Dimensional)

**Definition:** More is better, linearly. Satisfaction scales proportionally with how well the need is met. Users can articulate these needs clearly and compare competitors on them.

**Satisfaction curve:** Linear. Better delivery = higher satisfaction. Worse delivery = lower satisfaction. The relationship is proportional and predictable.

**Product implication:** Performance needs are the core of competitive differentiation. Invest where you can measurably outperform alternatives. These are the needs that show up in feature comparison tables.

### Delighter (Attractive)

**Definition:** Unexpected capabilities. Absence is fine — users do not miss what they never expected. Presence creates disproportionate satisfaction and loyalty.

**Satisfaction curve:** Asymmetric (opposite of basic). Non-delivery is neutral. Delivery creates outsized positive response. But the effect decays — today's delighter becomes tomorrow's performance need and next year's basic expectation.

**Product implication:** Delighters build brand love and word-of-mouth. They are high-risk, high-reward — if users do not discover them, the investment is invisible. Pair delighters with strong onboarding or progressive disclosure.

### Indifferent

**Definition:** No significant impact on satisfaction either way. Users do not care whether the capability exists. Often reflects engineering-driven features or internal stakeholder requests that do not map to real user needs.

**Product implication:** Deprioritize. If a theme classifies as indifferent, it may indicate that the feedback is coming from a non-representative segment or that the theme was miscategorized. Verify before discarding.

### Reverse

**Definition:** Presence causes dissatisfaction. Rare in product contexts, but occurs when a feature creates complexity or friction for a segment that does not want it (e.g., power users annoyed by onboarding tutorials they cannot skip).

**Product implication:** Make reversible. Offer opt-out or configuration. Reverse needs often surface in personas that are not the primary target — acknowledge the tension rather than ignoring it.

## Why Kano Matters for VoC

Classifying the TYPE of need changes how you respond to it:

| Kano Class | Response Strategy |
|------------|-------------------|
| Basic gap | Fix immediately. Do not roadmap — just fix. No blog post, no launch event. Users expect this to work. |
| Performance | Roadmap and invest. Measure improvement. Communicate progress. This is where competitive positioning lives. |
| Delighter | Prototype and test. Validate that the delight is real before committing. Watch for decay — delighters have a shelf life. |
| Indifferent | Deprioritize. Redirect resources to basic gaps and performance needs. |
| Reverse | Make configurable or removable. Do not force on users who do not want it. |

Without Kano classification, a prioritization framework treats all needs as "things users want, ranked by severity." This leads to chronic underinvestment in basic gaps (they do not score as "exciting") and overinvestment in delighters (they generate enthusiastic quotes that inflate perceived importance).

## Classification Heuristics for Qualitative Data

Traditional Kano analysis uses paired functional/dysfunctional survey questions ("How would you feel if this feature existed?" / "How would you feel if it did not?"). In VoC synthesis, you work with organic qualitative data. Use these heuristics to infer classification from the signal you have.

### Heuristic 1: Emotional Valence

**Anger, frustration, exasperation in quotes** → likely basic gap. The user expected this to work and it did not. The emotional intensity comes from violated expectations, not from desire for improvement.

- "Why can't I even see my claims?" — anger at missing baseline = basic
- "This is ridiculous, I've been on hold for 30 minutes" — frustration at broken expectation = basic (if hold time expectation is "reasonable," not zero)

**Measured dissatisfaction, wishing, requesting** → likely performance. The user acknowledges the capability exists but wants it to be better.

- "I wish the app loaded faster" — scalar improvement = performance
- "It would be helpful if I could filter by date" — enhancement request = performance

**Delight, surprise, unsolicited praise** → likely delighter. The user did not expect this and was pleasantly surprised.

- "I was amazed that it suggested a cheaper option" — unsolicited positive surprise = delighter
- "I didn't even ask for this but it's so helpful" — unexpected value = delighter

**Shrug, indifference, no emotional response** → likely indifferent. The user acknowledges the feature but does not care.

- "I guess it has a dark mode? I don't really use it" — indifferent
- "I noticed they added badges, whatever" — indifferent

### Heuristic 2: Complaint vs. Request Framing

- **Complaints** ("why can't I...", "it doesn't even...", "this is broken") lean **basic**
- **Requests** ("it would be great if...", "can you add...", "I'd love to see...") lean **performance**
- **Unsolicited praise** ("I was amazed when...", "the best part is...") signals **delighter**

### Heuristic 3: Absence vs. Improvement Language

- **Absence of capability** ("I can't see...", "there's no way to...") = **basic**
- **Existing capability that could be better** ("it's too slow", "the results aren't accurate enough") = **performance**

### Heuristic 4: Benchmark References

- **"Every other app does this"** = basic (industry-wide expectation)
- **"Competitor X does this better"** = performance (competitive comparison on a scale)
- **"No one else does this but it would be great"** = delighter (novel expectation)

### Heuristic 5: Binary vs. Scalar Satisfaction

- **Binary need** (it works or it doesn't, it exists or it doesn't) → lean **basic**
- **Scalar need** (faster, more accurate, more comprehensive) → lean **performance**

## Examples in Health Benefits Navigation Context

### Basic: Coverage Transparency
**Theme:** "I can see what's covered"
**Evidence:** Members express anger and confusion when they cannot determine whether a service is covered before receiving care. The expectation is binary — coverage information should be accessible. Nobody praises a navigator for showing coverage; they get furious when it is hidden.
**Quotes:** "I shouldn't have to call three times to find out if this is covered" (complaint, frustration, absence of expected capability).

### Performance: Hold Time Reduction
**Theme:** "Shorter hold times when I call"
**Evidence:** Members consistently rate their experience relative to hold time length. 5 minutes is better than 10, 2 is better than 5. Satisfaction scales linearly. Members compare to other service lines ("My insurance company picks up faster").
**Quotes:** "I waited 20 minutes — last time it was only 10, which was fine" (scalar comparison, performance framing).

### Delighter: Proactive Cost Optimization
**Theme:** "It told me there was a cheaper pharmacy nearby"
**Evidence:** Members express surprise and delight when the navigator proactively suggests cost savings they did not ask for. Nobody expects this behavior — when it happens, it generates outsized positive sentiment and loyalty signals.
**Quotes:** "I didn't even know I could save money by going to the other pharmacy — the app just told me!" (unsolicited positive surprise).

### Indifferent: Dark Mode
**Theme:** "The app has a dark mode"
**Evidence:** When mentioned at all, patients acknowledge the feature without positive or negative sentiment. No patient has cited dark mode as a reason for satisfaction or dissatisfaction. It does not connect to the core task of managing their health experience.
**Quotes:** "Oh, I guess there's a dark mode. I haven't tried it" (shrug, no engagement).

## Common Pitfalls

### Pitfall 1: Confusing Basic Gaps with Performance Needs

Basic gaps are binary — the capability exists or it does not. Performance needs are scalar — the capability exists but could be better. This distinction matters because the response is different:

- Basic gap: ship the fix, do not iterate on "how good" the fix is
- Performance need: iterate toward measurable improvement

**Test:** Ask "can this need be partially met, and would partial be okay?" If yes, it is performance. If partial fulfillment is still a failure (e.g., "you can see some of your claims but not all of them" is not acceptable), it is basic.

### Pitfall 2: Treating All Complaints as Basic

Not every complaint signals a basic gap. "This is too slow" is a complaint, but speed is a performance dimension — it can always be faster. Reserve basic classification for complaints about absent or fundamentally broken capabilities, not suboptimal ones.

### Pitfall 3: Assuming Delighters Stay Delighters

Kano categories are not permanent. Today's delighter becomes tomorrow's performance need (competitors copy it, users get used to it) and next year's basic expectation (everyone has it, absence is noticed). When re-scoring, check whether a previously classified delighter has shifted categories based on new evidence.

### Pitfall 4: Classifying Based on Volume Instead of Signal

A theme with 50 mentions is not automatically basic. Volume tells you about reach, not about the type of need. A delighter can have high volume (many users are surprised) and a basic gap can have low volume (few users encountered the broken flow). Use the emotional and linguistic signals in the quotes, not the mention count.
