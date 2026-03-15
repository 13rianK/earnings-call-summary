# Tone & Sentiment Analysis Framework

This reference provides the methodology for analyzing management language patterns across earnings calls. Used by the Tone & Sentiment mode and the tone comparison section within Peer Comparison mode.

## Why Tone Analysis Matters

Executives are trained to project confidence. But language patterns reveal what scripted messaging tries to hide. A CEO who shifts from "we will deliver" to "we're working to position ourselves" is signaling uncertainty months before the numbers show it. This framework provides a structured way to detect those shifts.

## Analysis Dimensions

### 1. Confidence Language Ratio

Track the ratio of confidence markers to hedge markers in management's prepared remarks and Q&A answers.

**Confidence markers** (high conviction):
- "We will...", "We are committed to...", "We expect to deliver..."
- "Strong", "robust", "accelerating", "ahead of plan"
- Specific numbers unprompted: "We expect $X in Q[N]"
- Proactive disclosure of tough metrics (shows nothing to hide)
- Speaking about results in superlatives: "best quarter ever", "record"

**Hedge markers** (reduced conviction):
- "We anticipate...", "We believe...", "We're working toward..."
- "Approximately", "roughly", "in the range of", "subject to"
- "Cautiously optimistic" (classic hedge — optimistic enough to not alarm, cautious enough to have cover)
- "It depends on...", "assuming [external factor]..."
- Conditional language: "if the macro environment cooperates"
- Passive voice on bad news: "margins were impacted" vs. active voice on good news: "we drove margin expansion"

**Scoring approach:** For each quarter, count confidence and hedge markers in prepared remarks. Calculate ratio. A shift from 3:1 to 1.5:1 across two quarters is a meaningful degradation even if the words on the surface still sound positive.

### 2. Specificity Scoring

Track how precise management's forward-looking statements are. Declining specificity often precedes guidance cuts or missed targets.

**High specificity (score 3):**
- Exact numbers: "Revenue of $24.0-24.5B"
- Named timelines: "launching in Q3 2025"
- Precise mechanics: "150bps margin expansion driven by 80bps from mix shift and 70bps from cost actions"

**Medium specificity (score 2):**
- Ranges: "mid-teens growth", "low double digits"
- Approximate timelines: "second half of the year", "by year-end"
- Directional with qualifiers: "meaningful improvement in margins"

**Low specificity (score 1):**
- Vague directional: "continued growth", "further improvement"
- Indefinite timelines: "over time", "in the medium term", "as conditions allow"
- Qualitative only: "we're well positioned", "we like our trajectory"

For each quarter, average the specificity scores of all forward-looking statements. Track the trend.

### 3. Topic Prominence Tracking

Track which topics receive the most prepared-remarks airtime each quarter. Major shifts in topic allocation signal shifting priorities — or evasive reframing.

**How to track:**
- Note the primary topics in the CEO's prepared remarks (typically 3-5 themes)
- Note the primary topics in the CFO's section
- For each topic, assess: was it prominent (dedicated section), mentioned (brief reference), or absent?

**What to look for:**
- **Disappearances**: A product line, metric, or initiative that was featured in Q1-Q2 but vanishes from Q3's remarks. This often means it's underperforming — management doesn't want to call attention to it.
- **Emergences**: A new theme appears that wasn't mentioned before. This can signal a pivot, a new competitive pressure, or a newly discovered opportunity.
- **Reframing**: Management discusses the same topic but changes the framing — e.g., in Q1 "subscriber growth" was the headline metric, by Q3 it's "revenue per subscriber" because absolute growth slowed.

### 4. Q&A Defensiveness Indicators

The Q&A section is less scripted and more revealing. Look for defensive patterns:

**Defensive signals:**
- Answering a question that wasn't asked (redirecting away from the actual question)
- "As I mentioned in my prepared remarks..." (avoiding new detail)
- Handing off a tough question to a subordinate executive
- "We don't comment on..." followed by a topic they used to discuss
- Lengthy preambles before getting to the actual answer
- Correcting the analyst's framing aggressively: "I don't think that's the right way to look at it"

**Open signals:**
- Volunteering information the analyst didn't ask for
- Acknowledging challenges directly: "you're right, that was weaker than we expected"
- Providing additional detail beyond what was asked
- Referring to specific data: "let me give you the exact numbers..."

**Scoring:** For each quarter, assess the Q&A tone on a 5-point scale:
1. Very defensive — multiple redirections, minimal new disclosure
2. Somewhat defensive — hedged on tough questions, comfortable on easy ones
3. Neutral — straightforward responses, neither evasive nor expansive
4. Somewhat open — volunteered extra context, engaged with tough questions
5. Very open — candid about challenges, proactive new information

### 5. Forward-Looking Language Patterns

Track how management frames the future:

**Strong conviction patterns:**
- Active voice with the company as subject: "We will launch..."
- Unconditional commitments: "We are raising guidance..."
- Specifics without qualifiers: "Full-year CapEx of $50B"

**Weakening conviction patterns:**
- Conditional framing: "Assuming the macro environment..."
- Passive/external attribution: "The market opportunity should allow us to..."
- Widening ranges: guidance range goes from $1B to $2B
- Qualifier stacking: "We remain cautiously optimistic about the potential for moderate improvement"

## Applying the Framework

### For Tone & Sentiment Mode (single company, multi-quarter)
Apply all 5 dimensions to each quarter. Build a trajectory table showing how each dimension moved over time. The most valuable output is identifying the quarter where the tone inflected — and correlating that with what was happening in the business.

### For Peer Comparison Mode (multiple companies, same quarter)
Apply dimensions 1, 2, and 4 comparatively. Score each company on the same scales and present side by side. Divergences are the insight — if Company A scores high-confidence while Company B in the same industry sounds hedged, either A is over-confident or B has early visibility on a problem that hasn't hit A yet.

### For On-Demand Mode (single company, single quarter)
Apply a lighter version — don't do full scoring, but note management's overall tone in the Risk Assessment section: "Management struck a [confident / cautious / defensive] tone throughout the call, particularly when discussing [topic]." Include 1-2 specific linguistic examples as evidence.
