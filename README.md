# Earnings Call Brief

A Claude skill that sources, analyzes, and synthesizes earnings call transcripts for publicly traded companies into structured, professional-grade documents.

Give it a ticker and it produces a concise executive brief. Give it multiple tickers and it compares their narratives side by side. Ask it to track management credibility over time and it builds a commitment scorecard. All outputs are formatted `.docx` files ready to share.

---

## What It Does

The skill operates in six modes with an optional audience lens modifier:

| Mode | Input | Output | Use Case |
|------|-------|--------|----------|
| **On-Demand** | 1 ticker | 1-page brief | Quick post-earnings summary |
| **Comparison** | 1 ticker, multi-quarter | 2-3 page evolution brief | Tracking narrative shifts over time |
| **Peer Comparison** | 2-4 tickers | 2-3 page thematic comparison | Competitive analysis across earnings calls |
| **Tone & Sentiment** | 1 ticker, multi-quarter | 1-2 page tone analysis | Detecting management confidence shifts |
| **Guidance Tracker** | 1 ticker, multi-quarter | 1-2 page scorecard | Assessing management credibility |
| **Scheduled** | List of tickers | Automated tasks | Hands-off monitoring of a watchlist |

### Audience Lenses

Any mode can be combined with an audience lens to shift the analytical perspective:

- **Strategic Investor** (default) — Thesis-focused, evaluative, numbers-heavy
- **Prospective Employee** — Growth trajectory, culture signals, hiring/layoff indicators
- **Short Thesis** — Red flags, metric degradation, management evasion patterns
- **Supplier / Partner** — Purchasing trajectory, financial stability, partnership signals
- **General Research** — Balanced, accessible, jargon-light

---

## Example Prompts

```
Summarize NVDA's latest earnings call for me

Compare the latest earnings calls for AMD and NVDA — what are the key differences
in how management is positioning their AI strategy?

Has Boeing's management been getting more or less confident over the past year?

Has Tesla management actually delivered on what they promised? Track their
commitments from earnings calls.

I'm considering a job offer from Salesforce. Summarize their latest earnings call
from the perspective of someone deciding whether to join.

I want to track earnings calls for AAPL, MSFT, and GOOGL. Set up automatic
briefs after their next earnings.
```

---

## Installation

### Prerequisites

- [Claude Desktop](https://claude.ai/download) with Cowork mode enabled
- The `docx` skill (bundled with Claude's default skill set)

### Install the Skill

1. Download `earnings-call-brief.skill` from this repo
2. In Claude Desktop, open **Settings → Skills**
3. Click **Install Skill** and select the `.skill` file
4. The skill will appear in your available skills list

Alternatively, copy the `earnings-call-brief/` directory into your Claude skills folder:

```
~/.claude/skills/earnings-call-brief/
├── SKILL.md
└── references/
    ├── brief-template.md
    ├── tone-analysis-framework.md
    └── audience-lenses.md
```

---

## Skill Architecture

```
earnings-call-brief/
├── SKILL.md                              # Main skill instructions (~240 lines)
│                                         #   - Mode selection logic
│                                         #   - Shared transcript sourcing strategy
│                                         #   - Per-mode analysis frameworks
│                                         #   - Output and quality check specs
│
└── references/
    ├── brief-template.md                 # Document formatting for all output types
    │                                     #   - Shared styling (fonts, colors, header bar)
    │                                     #   - Per-mode layout specs
    │                                     #   - docx-js implementation notes
    │
    ├── tone-analysis-framework.md        # Linguistic analysis methodology
    │                                     #   - Confidence vs. hedge language taxonomy
    │                                     #   - Specificity scoring (1-3 scale)
    │                                     #   - Topic prominence tracking
    │                                     #   - Q&A defensiveness indicators
    │                                     #   - Forward-looking language patterns
    │
    └── audience-lenses.md                # Per-lens extraction criteria
                                          #   - Strategic investor (default)
                                          #   - Prospective employee
                                          #   - Short thesis
                                          #   - Supplier / partner
                                          #   - General research
```

### How It Works

1. **Transcript sourcing** — Web searches across multiple sources (Seeking Alpha, Motley Fool, company IR pages, SEC EDGAR 8-K filings). Falls back gracefully when transcripts are paywalled.
2. **Analysis** — Structured extraction framework tailored to each mode. The on-demand brief extracts 5 sections (takeaways, risks, priorities, announcements, Q&A highlights). Multi-quarter modes build per-quarter working notes then synthesize across time.
3. **Document generation** — Formatted `.docx` output using consistent styling (navy header bar, section dividers, color-coded tables for scorecards). Read from `references/brief-template.md` at generation time.
4. **Scheduling** — Calendar-aware task creation that fires the day after each company's expected earnings date, giving transcripts time to become available.

### Dependencies

The skill relies on capabilities available in Claude's standard toolset:

- **Web search & fetch** — For sourcing transcripts and earnings dates
- **docx skill** — For generating formatted Word documents
- **schedule skill** — For automated runs (scheduling mode only)

No external APIs, Python packages, or API keys are required.

---

## Sample Outputs

The `sample-outputs/` directory contains example briefs generated during development:

| File | Mode | Description |
|------|------|-------------|
| `NVDA_Earnings_Brief_Q4_FY2026.docx` | On-Demand | NVIDIA quarterly brief |
| `COST_Earnings_Brief_Q4_FY2025.docx` | On-Demand | Costco quarterly brief |
| `INSP_Earnings_Brief_Q4_FY2025.docx` | On-Demand | Inspire Medical (small-cap) brief |
| `LLY_Earnings_Evolution_Q1FY2025_to_Q4FY2025.docx` | Comparison | Eli Lilly multi-quarter evolution |
| `Peer_Comparison_AMD_NVDA_Q4_2026.docx` | Peer Comparison | AMD vs. NVIDIA AI strategy comparison |
| `BA_Tone_Analysis_Q1_to_Q4_2025.docx` | Tone & Sentiment | Boeing management confidence tracking |
| `TSLA_Guidance_Tracker_Q1_2025_to_Q4_2025.docx` | Guidance Tracker | Tesla commitment scorecard |
| `CRM_Earnings_Brief_Q4_FY2026.docx` | Audience Lens | Salesforce — prospective employee perspective |

---

## Benchmark Results

Tested across 9 eval cases comparing with-skill vs. without-skill (baseline) performance:

**Iteration 1** (core modes): 100% pass rate with skill vs. 84% without (+16%)

**Iteration 2** (new modes): 95% pass rate with skill vs. 70% without (+25%)

The skill adds the most value on **Peer Comparison** and **Tone & Sentiment** modes, where the structured frameworks (thematic organization, confidence/hedge ratios, topic prominence tracking) produce output the model doesn't naturally generate on its own.

---

## License

MIT
