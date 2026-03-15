---
name: earnings-call-brief
description: "Source and summarize earnings call transcripts for publicly traded companies into concise executive briefs, peer comparisons, tone analyses, and guidance scorecards. Use this skill whenever the user provides a stock ticker and wants an earnings call summary, transcript highlights, quarterly call brief, management commentary summary, or post-earnings quick take. Also trigger for peer or competitor comparisons across earnings calls ('compare AAPL and MSFT calls'), tone and sentiment analysis ('is management getting more confident?'), guidance tracking ('did they deliver on what they promised?'), and audience-specific perspectives ('what should I know as a prospective employee?' or 'give me the short thesis angle'). Trigger for scheduling requests too — 'set up automatic briefs after earnings'. Even casual requests like 'summarize AAPL's last earnings call' or 'what happened on MSFT's call?' should activate this skill."
---

# Earnings Call Brief

Source, analyze, and synthesize earnings call transcripts for publicly traded companies. Outputs are formatted .docx documents written for professional audiences — from strategic investors to prospective employees.

## Mode Selection

This skill supports six modes and one modifier. Select the mode based on the user's request:

| Mode | Trigger | Input | Output |
|------|---------|-------|--------|
| **On-demand** | "summarize [ticker]'s earnings call" | 1 ticker | 1-page brief |
| **Comparison** | "how has [ticker] changed over the year" | 1 ticker, multiple quarters | 2-3 page evolution brief |
| **Peer Comparison** | "compare [ticker A] and [ticker B] calls" | 2-4 tickers | 2-3 page thematic comparison |
| **Tone & Sentiment** | "is management getting more/less confident?" | 1 ticker, multiple quarters | 1-2 page tone analysis |
| **Guidance Tracker** | "did they deliver on what they promised?" | 1 ticker, multiple quarters | 1-2 page commitment scorecard |
| **Scheduled** | "set up automatic briefs for my watchlist" | list of tickers | scheduled tasks |

**Audience Lens** (modifier — can be applied to any mode above):
If the user specifies an audience or perspective, apply the corresponding lens. See `references/audience-lenses.md` for extraction criteria per lens. Default lens is "strategic investor" if none specified. Available lenses: strategic investor, prospective employee, short thesis, supplier/partner, general research.

When the user's request maps to multiple modes (e.g., "compare AAPL and MSFT tone over the past year"), combine the relevant modes — in that case, Peer Comparison + Tone & Sentiment.

## Shared: Transcript Sourcing

All modes depend on sourcing earnings call transcripts. This process is the same regardless of mode.

### Search Strategy

**Step 1 — Verify the current date.** Write down today's date. This anchors all freshness checks.

**Step 2 — Search for transcripts.** Run multiple web searches in parallel:
```
"[Company] earnings call transcript Q[N] [Year]"
"[Company] quarterly earnings transcript [Year]"
"[Ticker] earnings call transcript" site:seekingalpha.com OR site:fool.com OR site:nasdaq.com
```

**Step 3 — Validate freshness.** Confirm the transcript date is from the target quarter. If the transcript is older than 4 months from today and you're looking for the most recent call, search again more aggressively.

**Step 4 — Extract key content.** Fetch the transcript page and extract prepared remarks (CEO, CFO, other executives), Q&A session, and any forward-looking guidance.

**Fallback sources** (if transcript is paywalled): company IR page press releases, SEC 8-K filings with earnings release attachments, financial news coverage summarizing the call. Be transparent in the output about which sources were used.

For multi-quarter modes (Comparison, Tone, Guidance Tracker): repeat the search for each quarter in the window. Label each transcript by quarter. Note any gaps transparently.

---

## On-Demand Mode

Produce a concise 1-page .docx brief from a company's most recent earnings call.

### Analysis Framework

Extract five sections from the transcript. Think like a strategic investor — focus on signal, not noise.

**Section 1 — Three Major Takeaways:** The three most consequential things said on the call — items that would change an investor's thesis. Rank by materiality. Each: 2-3 sentences covering what happened, why it matters, and what it implies.

**Section 2 — Management's Position on Major Risks:** What risks did management acknowledge? Look for: macro headwinds (inflation, rates, FX), competitive threats, regulatory exposure, operational risks, balance sheet concerns. Capture management's *tone* — confident, evasive, defensive, or proactive. How management discusses risk matters as much as what risks they name.

**Section 3 — Top Priorities for Next Quarter / Year:** Capital allocation, product launches, market expansion, cost programs, org changes. Tag items [Q] for near-term and [FY] for medium-term.

**Section 4 — Important Announcements:** New/revised guidance (quantify the change), executive changes, partnerships, divestitures, buyback authorizations, accounting changes.

**Section 5 — Notable Q&A Highlights:** 2-3 analyst questions that elicited revealing answers. Format: what was asked, what was answered, what the answer reveals.

### Output

Read `references/brief-template.md` for exact layout, formatting, and docx-js implementation guidance. Read the docx SKILL.md before generating.

**File naming:** `[Ticker]_Earnings_Brief_Q[N]_[FY Year].docx`

### Quality Check
- [ ] Transcript date matches most recent quarter (not stale training data)
- [ ] All five sections present and substantive
- [ ] Fits on one page
- [ ] Tone appropriate for audience (default: strategic investors)
- [ ] Sources cited at bottom
- [ ] No hallucinated quotes — paraphrase if unverifiable

---

## Comparison Mode

Source multiple quarters of earnings calls for a single company and synthesize a narrative arc. Default window: last 4 quarters. See the On-demand section for the per-quarter analysis framework.

### Synthesis Structure

**Executive Summary (1 paragraph):** How the company's story evolved. Dominant theme at start vs. where management is now.

**Strategic Direction & Business Plan:** How did priorities shift? Pivot, double down, or retreat? Identify inflection points.

**Risk Landscape Evolution:** Which risks grew, shrank, or emerged? How did management's tone on key risks change?

**Management Credibility Check:** Did management deliver on prior-quarter commitments? Track promises against outcomes. This is one of the most valuable things a multi-quarter view reveals.

**Key Metrics Trajectory:** Trace repeatedly-emphasized KPIs quarter to quarter. How did management frame the trajectory?

**Outlook:** What should the reader expect going forward, based on the evolution?

### Output
Target 2-3 pages. Use formatting from `references/brief-template.md`. Header bar: "[Company] ([Ticker]) | Earnings Call Evolution | [Start] – [End]"

**File naming:** `[Ticker]_Earnings_Evolution_[Start]_to_[End].docx`

---

## Peer Comparison Mode

Compare 2-4 companies' most recent earnings calls side by side, organized by theme rather than by company. This is the mode that generates the most differentiated insight — it surfaces narrative divergences that are invisible when reading transcripts in isolation.

### When to Trigger

User mentions multiple tickers in the context of earnings analysis, or asks to compare competitors, or phrases like "how does [X]'s story compare to [Y]?" or "peer comparison."

### Phase 1: Source All Transcripts

Source the most recent earnings call for each company using the shared search strategy. Ideally all transcripts should be from the same quarter for a clean comparison. If companies report on different fiscal calendars, note the date offsets and adjust for seasonality differences.

### Phase 2: Per-Company Analysis

Run the on-demand five-section analysis for each company as internal working notes. These won't appear in the output but provide the raw material for thematic synthesis.

### Phase 3: Thematic Synthesis

Organize the comparison around themes, not companies. The goal is to answer: **"Where do these companies' narratives converge and diverge, and what do the divergences reveal?"**

Structure the output as:

**Peer Set Overview:** One-paragraph table setting context — who these companies are, market caps, what quarter is being compared, and why this peer group is relevant.

**Growth Outlook Comparison:** How does each company frame their growth trajectory? Who is accelerating, decelerating, or inflecting? Surface any contradictions (e.g., one company says "demand is softening" while a peer says "we're seeing acceleration in the same end market").

**Margin & Profitability Narrative:** What's the margin story for each? Expanding, contracting, investing for future scale? How do management teams justify their margin trajectory?

**Risk Framing Divergences:** This is where the most valuable insight lives. If all peers call out the same risk, it's an industry issue. If only one company mentions a risk that peers ignore, that's either candor or a company-specific problem. Flag both patterns.

**Capital Allocation Philosophy:** How is each company deploying cash? Aggressive investment vs. returning capital vs. deleveraging. Different capital allocation strategies within a peer group often signal different views of where the industry is heading.

**Management Tone Comparison:** Read `references/tone-analysis-framework.md` and apply the confidence/hedge scoring framework comparatively. Which management team sounds most and least confident? Where are the tonal mismatches vs. the financial reality?

**Divergence Summary:** A tight summary of the 3-5 most meaningful divergence points. For each: what diverges, why it matters, and what a strategic investor should do with the information.

### Output
Target 2-3 pages. Header bar: "Peer Comparison | [Ticker A] vs. [Ticker B] [vs. ...] | Q[N] [Year]"

**File naming:** `Peer_Comparison_[Tickers]_Q[N]_[Year].docx`

---

## Tone & Sentiment Tracking Mode

Analyze how management's language, confidence, and framing have shifted across multiple earnings calls. This mode is specifically designed to detect subtle signals that precede major business inflection points — signals that are hard to catch by reading any single transcript but become visible in aggregate.

### When to Trigger

User asks about management confidence, tone shifts, whether executives are "getting more/less confident," language changes, or sentiment tracking over time.

### Phase 1: Source & Analyze

Source 4-8 quarters of transcripts (default: 4). For each quarter, perform the analysis described in `references/tone-analysis-framework.md`, which covers:
- Confidence vs. hedge language ratios
- Specificity scoring (concrete numbers vs. vague qualifiers)
- Topic prominence tracking (what gets airtime vs. what disappears)
- Q&A defensiveness indicators
- Forward-looking language patterns

### Phase 2: Synthesize the Trajectory

Structure the output as:

**Overall Tone Arc (1 paragraph):** Summarize the trajectory — e.g., "Management entered FY2025 with high confidence, language became increasingly hedged through Q2-Q3 as growth decelerated, and Q4 showed early signs of renewed conviction around the AI pivot."

**Confidence Trend:** Quarter-by-quarter assessment. For each quarter, note the overall confidence level (high/moderate/low) and the key linguistic evidence. Include a simple visual indicator in the document (e.g., ▲▲▲ / ▲▲ / ▲ / ▼ / ▼▼) to make the trend scannable.

**Specificity Trend:** Are management's commitments getting more or less precise? A shift from "we expect revenue of $24-25B" to "we're working toward a strong second half" is a meaningful degradation of specificity that often precedes a guidance cut.

**Topic Disappearances & Emergences:** What topics were prominent early in the window but dropped off? What new topics appeared? Track both management's prepared remarks (what they choose to talk about) and analyst Q&A (what they're forced to address). Conspicuous omissions are as important as explicit statements.

**Red Flags & Green Flags:** Summarize 3-5 specific linguistic signals that the reader should pay attention to. Frame each as "In Q[N], management said [X] — this matters because [Y]."

### Output
Target 1-2 pages. Header bar: "[Company] ([Ticker]) | Tone & Sentiment Analysis | [Start] – [End]"

**File naming:** `[Ticker]_Tone_Analysis_[Start]_to_[End].docx`

---

## Guidance Tracker Mode

Extract every quantitative and qualitative commitment management makes on earnings calls, then track delivery against those commitments in subsequent quarters. This builds a management credibility profile that compounds in value over time.

### When to Trigger

User asks about management credibility, whether they "deliver on promises," guidance accuracy, commitment tracking, or "did they do what they said they'd do."

### Phase 1: Extract Commitments

Source 4-8 quarters of transcripts (default: 4). From each call, extract every statement that constitutes a forward-looking commitment. These fall into categories:

**Quantitative commitments** (most trackable):
- Revenue or earnings guidance ("we expect FY25 revenue of $80-83B")
- Margin targets ("we're targeting 200bps operating margin expansion")
- CapEx plans ("$50B in capital expenditure this fiscal year")
- Headcount plans ("hiring 500 engineers by year-end")
- Product timelines ("launching Product X in Q3")

**Qualitative commitments** (still trackable):
- Strategic intentions ("we will prioritize international expansion")
- Market positioning goals ("we intend to be the #1 provider in [X]")
- Operational goals ("we're committed to simplifying our supply chain")
- Cultural/org goals ("building a world-class engineering team")

For each commitment, record: the exact or paraphrased statement, the quarter it was made, the quarter it was due (if specified), and the category.

### Phase 2: Track Outcomes

For each commitment, search subsequent transcripts and earnings data for evidence of delivery:
- **Delivered**: Management explicitly reported hitting or exceeding the target, or the data confirms it
- **Partially delivered**: Some progress but fell short of the stated target
- **Missed**: Target was explicitly missed, revised down, or quietly dropped
- **Pending**: Commitment hasn't come due yet
- **Not addressed**: Management stopped mentioning it without resolution — this is often the most telling outcome, and should be flagged as a yellow signal

### Phase 3: Build the Scorecard

Structure the output as:

**Credibility Summary (1 paragraph):** Overall assessment. What percentage of trackable commitments were delivered? Is the trend improving or deteriorating? How does this management team compare to what you'd expect from a well-run company?

**Commitment Scorecard Table:** A structured table with columns: Commitment, Quarter Made, Due By, Outcome (Delivered / Partial / Missed / Pending / Not Addressed), Evidence. Sort by quarter made, most recent first.

**Pattern Analysis:** Are there patterns in what gets delivered vs. what gets missed? For example: "Management consistently delivers on cost-cutting targets but over-promises on revenue growth timelines." Or: "Quantitative targets are usually met, but qualitative strategic commitments are frequently dropped without explanation." These patterns are more useful than any individual data point.

**Credibility Implications:** What does the track record mean for evaluating management's current forward-looking statements? If they've missed 3 of their last 5 revenue guidance ranges, the current guidance should be discounted. If they've delivered on every capital return commitment, their new buyback authorization is credible.

### Output
Target 1-2 pages. Header bar: "[Company] ([Ticker]) | Guidance Tracker | [Start] – [End]"

**File naming:** `[Ticker]_Guidance_Tracker_[Start]_to_[End].docx`

---

## Audience Lenses (Modifier)

Any mode above can be modified by an audience lens. The lens changes what gets emphasized, what tone is used, and what conclusions are drawn — but doesn't change the sourcing process.

If the user specifies a perspective (explicitly or implicitly), apply the corresponding lens. If no lens is specified, default to "strategic investor."

Read `references/audience-lenses.md` for the full extraction criteria, emphasis areas, and output tone for each lens. Brief summary:

| Lens | When to Apply | Primary Question Answered |
|------|---------------|--------------------------|
| **Strategic Investor** (default) | Board, investment committee, due diligence | "Is this a good business with credible management?" |
| **Prospective Employee** | "I'm thinking of joining...", "what's it like to work at..." | "Is this company growing, stable, and investing in its people?" |
| **Short Thesis** | "bear case", "red flags", "short thesis", "what could go wrong" | "Where are the cracks that management is trying to paper over?" |
| **Supplier / Partner** | "vendor assessment", "should we partner with...", "B2B prospect" | "Is this company a reliable, growing customer/partner?" |
| **General Research** | No specific angle, exploratory, "tell me about..." | "What's the current state and direction of this business?" |

When applying a lens, note it in the document header bar: e.g., "Apple Inc. (AAPL) | Q1 FY2025 Earnings Brief | Employee Perspective"

---

## Scheduling Mode

When the user wants to automate briefs for a watchlist, follow this process:

**Step 1 — Collect the watchlist.** Get the list of tickers.

**Step 2 — Look up earnings dates.** For each ticker, web search:
```
"[Ticker] next earnings date [current year]"
"[Company] earnings calendar [current year]"
```

**Step 3 — Create scheduled tasks.** Use the scheduling skill to create one task per company that fires the day after the expected earnings date, runs this skill in on-demand mode, and saves the output to the user's workspace.

Earnings dates shift quarter to quarter, so set up one quarter at a time. Remind the user to update when next quarter's dates are confirmed.

**Step 4 — Confirm with the user.** Present a summary table (ticker, expected earnings date, scheduled run date) and wait for confirmation before creating tasks.

---

## Tone and Style Guidelines

The default audience is a **board of strategic investors**. Adjust when an audience lens is applied (see `references/audience-lenses.md`).

Core writing principles regardless of audience:
- **Be direct.** No filler, no preamble. Lead with the most important information.
- **Be evaluative.** Don't just report — assess what it means.
- **Be specific.** Use numbers. "$24.3B, +12% YoY" beats "revenue came in strong."
- **Be balanced.** Note both bullish and bearish signals.
- **Be concise.** Every word earns its place. Use abbreviations where clear (YoY, QoQ, bps, mgmt, FY25E).

## Dependencies

- **Web search**: For sourcing transcripts and earnings dates
- **Web fetch**: For reading transcript pages
- **docx skill**: For generating formatted Word documents
- **schedule skill**: For automated runs (scheduling mode only)
