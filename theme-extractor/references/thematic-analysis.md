# Thematic Analysis for VoC Synthesis

Reference methodology adapted from Braun & Clarke (2006) reflexive thematic analysis, modified for product Voice-of-Customer contexts where speed and actionability matter more than academic rigor.

## The 6 Phases (Adapted)

### Phase 1: Familiarization
Read the input documents. Note initial impressions, recurring words, emotional intensity. Do not assign themes yet.

In VoC context: read all unprocessed inputs in a single pass before making any theme assignments. This prevents anchoring on the first few documents.

### Phase 2: Initial Code Generation
Mark segments of text that capture a distinct idea, complaint, request, or experience. A single input may generate multiple codes.

**Code = a verbatim or near-verbatim segment tied to a user need, pain point, or experience.**

Examples:
- "I just want to know if it's covered before I go" → code: pre-visit coverage certainty
- "I waited 20 minutes on hold" → code: excessive hold time
- "The app crashed when I tried to view claims" → code: mobile app stability

### Phase 3: Theme Construction
Group related codes into candidate themes. A theme captures a pattern of shared meaning across multiple inputs.

**Theme ≠ topic.** A topic is a subject area ("urgent care"). A theme is a pattern of meaning ("members lack confidence in coverage information, leading to care avoidance or surprise bills").

Good themes:
- Describe a user experience pattern, not just a feature area
- Are supported by multiple codes from different inputs
- Have a clear "so what" — they connect to a product or business decision

Bad themes:
- Too broad: "patients are unhappy" (no actionable signal)
- Too narrow: "one patient couldn't find the search bar" (single data point)
- Topic-only: "medication side effects" (no pattern of meaning)

### Phase 4: Theme Review
Check each candidate theme against the evidence:
- Does the theme have support from at least 3 inputs? (Below 3 = emerging signal, not a confirmed theme)
- Are the grouped codes actually about the same underlying issue?
- Should any theme be split (it's actually two distinct issues)?
- Should any themes merge (they're the same issue from different angles)?

### Phase 5: Theme Definition
Write a canonical name and 2-3 sentence summary for each theme. The name should be specific enough to distinguish from related themes.

**Naming convention:** `{subject} {problem pattern}`
- Good: "Urgent care coverage confusion"
- Good: "Surprise billing anxiety"
- Bad: "Coverage issues" (too vague)
- Bad: "Member called about urgent care on April 15" (too specific, that's an event not a theme)

### Phase 6: Registry Update
Map confirmed themes to the persistent registry. This is where VoC synthesis diverges from academic thematic analysis — themes persist across analysis cycles.

---

## Deduplication Heuristics

When matching a new code against existing themes, check:

1. **Same root cause?** Two complaints that stem from the same system/process failure belong to the same theme, even if the surface symptoms differ.
   - "I got different answers about coverage" + "The app shows different info than the phone agent" → same theme (inconsistent coverage information)

2. **Same user need?** Two complaints that express the same underlying need belong to the same theme.
   - "I want to know before I go" + "I need to check coverage in advance" → same theme (pre-visit coverage certainty)

3. **Same product surface area?** This is the weakest heuristic — use only as a tiebreaker. Two complaints about the same feature may be different themes if the root cause or user need differs.
   - "The app is slow" vs. "The app shows wrong info" → different themes despite same surface area

**When in doubt, keep separate.** It's easier to merge themes later than to split them. Premature merging loses signal.

## Merge Criteria

Propose a merge when:
- Two themes have >70% code overlap (most quotes could belong to either theme)
- The canonical names are near-synonyms when you strip the specifics
- Addressing one theme would necessarily address the other

Do NOT merge when:
- Themes share a topic but differ in root cause
- Themes affect different personas (even if the complaint sounds similar)
- One theme is a subset of another but has distinct actionability (keep the subset as a related theme)

**Merges are always proposals.** Set the merge proposal in the extraction report and let the human confirm.

## Quote Selection Criteria

When selecting representative quotes for a theme (max 10 per theme):

1. **Diversity first:** Prefer quotes from different clients, personas, and channels over multiple quotes from the same source
2. **Specificity:** Prefer quotes that are specific ("I waited 20 minutes") over vague ("the service is bad")
3. **Emotional resonance:** Include at least one quote that conveys the emotional impact (frustration, anxiety, confusion)
4. **Recency:** When all else is equal, prefer more recent quotes
5. **Attribution:** Every quote must include: input file path, line number, persona, client, channel, date

## Semantic vs. Latent Themes

- **Semantic themes** are explicitly stated: "I'm confused about my coverage" → theme about coverage confusion
- **Latent themes** are inferred from patterns: Multiple members avoid care due to cost uncertainty → theme about care avoidance (even if nobody says "I'm avoiding care")

For VoC synthesis, prioritize semantic themes. Latent themes require higher evidence bars (5+ inputs showing the pattern) and should be flagged as interpretive in the theme summary.
