# Document Templates — All Modes

This reference defines the formatting specs and layout for every output mode. All modes share the same base styling (fonts, colors, page setup) but have different section structures.

## Shared Formatting

### Page Setup
- **Paper**: US Letter (12240 x 15840 DXA)
- **Margins**: 0.75 inches all sides (1080 DXA)
- **Orientation**: Portrait

### Fonts and Sizes

| Element | Font | Size | Weight |
|---------|------|------|--------|
| Company header line | Arial | 14pt (28 half-pts) | Bold |
| Section headers | Arial | 10pt (20 half-pts) | Bold, dark navy |
| Body text | Arial | 9pt (18 half-pts) | Normal |
| Table header cells | Arial | 8pt (16 half-pts) | Bold |
| Table body cells | Arial | 8pt (16 half-pts) | Normal |
| Sources footer | Arial | 7pt (14 half-pts) | Italic |
| Lens indicator | Arial | 8pt (16 half-pts) | Italic, medium blue |

### Color Palette

| Use | Color (hex) |
|-----|-------------|
| Header bar background | #1B3A5C (dark navy) |
| Header bar text | #FFFFFF (white) |
| Section header text | #1B3A5C (dark navy) |
| Section divider lines | #1B3A5C (dark navy) |
| Body text | #333333 (dark gray) |
| Accent / key figures | #2E75B6 (medium blue) |
| Positive signal | #2E7D32 (forest green) |
| Negative signal | #C62828 (deep red) |
| Neutral / pending | #F57F17 (amber) |
| Table header background | #D5E8F0 (light blue) |
| Table alt-row background | #F5F5F5 (light gray) |

### Header Bar (all modes)
A full-width shaded bar (navy background, white text) implemented as a single-row, two-cell table with navy shading and no visible borders.
- **Left cell**: Company name and ticker — e.g., "Apple Inc. (AAPL)"
- **Right cell**: Mode-specific label — varies by mode (see below)

If an audience lens is applied, add a second row below the header bar with light blue background and italic text: e.g., "Perspective: Prospective Employee"

### Sources Footer (all modes)
- Thin navy rule (paragraph bottom border)
- Small italic text listing all sources used, with dates
- Example: Sources: Q1 FY2025 Earnings Call Transcript (Jan 30, 2025) via Motley Fool; 8-K filed Jan 30, 2025 via SEC EDGAR.

### docx-js Implementation Notes
- Use `LevelFormat.BULLET` for bullets (never unicode)
- Paragraph spacing: `before: 60, after: 60` for body; `before: 120, after: 60` for section headers
- Line spacing: single (240 twentieths of a point)
- Table widths: use `WidthType.DXA`, set both `columnWidths` and per-cell `width`
- Table shading: use `ShadingType.CLEAR` (never SOLID)
- Cell margins: `{ top: 80, bottom: 80, left: 120, right: 120 }`

---

## On-Demand Brief (1 page)

**Header right cell:** "Q[N] FY[Year] Earnings Call | [Date]"

**Page constraint:** Must fit on 1 page. If overflowing, reduce body to 8.5pt before cutting content.

### Layout (top to bottom)
1. **Header Bar**
2. **KEY TAKEAWAYS** — 3 numbered items, each 2-3 sentences. Bold lead-in phrase.
   - Example: **1. Cloud revenue accelerated.** AWS grew 19% YoY to $24.2B, up from 16% last quarter, driven by AI workload migration.
3. **RISK ASSESSMENT** — 3-5 compact bullets. Bold risk category, 1-sentence management position.
   - Example: **FX headwinds** — Mgmt expects 200bps revenue drag in Q2; hedging covers ~60% of international exposure.
4. **PRIORITIES — NEXT QUARTER / YEAR** — 3-5 bullets with [Q] / [FY] prefix tags.
5. **NOTABLE ANNOUNCEMENTS & Q&A** — Combined section. Announcements first, then 2-3 Q&A items formatted as "Q: [question] → A: [insight]"
6. **Sources Footer**

---

## Comparison Brief (2-3 pages)

**Header right cell:** "Earnings Call Evolution | [Start Quarter] – [End Quarter]"

### Layout
1. **Header Bar**
2. **EXECUTIVE SUMMARY** — 1 paragraph narrative arc
3. **STRATEGIC DIRECTION & BUSINESS PLAN** — Prose paragraphs with inflection points highlighted
4. **RISK LANDSCAPE EVOLUTION** — Risks organized as growing / shrinking / emerged, with tone commentary
5. **MANAGEMENT CREDIBILITY CHECK** — Promise-vs-delivery narrative
6. **KEY METRICS TRAJECTORY** — Inline table or narrative tracking KPIs across quarters
7. **OUTLOOK** — Forward-looking assessment based on trajectory
8. **Sources Footer**

---

## Peer Comparison Brief (2-3 pages)

**Header right cell:** "Peer Comparison | Q[N] [Year]"

### Layout
1. **Header Bar** — Left cell lists all tickers: "AAPL vs. MSFT vs. GOOGL"
2. **PEER SET OVERVIEW** — Context table: company, ticker, market cap, quarter reported, earnings date
3. **GROWTH OUTLOOK** — Thematic comparison (not per-company)
4. **MARGIN & PROFITABILITY** — Each company's margin narrative
5. **RISK FRAMING DIVERGENCES** — Industry-wide risks vs. company-specific risks. Flag where narratives diverge.
6. **CAPITAL ALLOCATION** — How each company deploys cash
7. **MANAGEMENT TONE COMPARISON** — Comparative confidence scoring (see tone framework)
8. **DIVERGENCE SUMMARY** — 3-5 most meaningful divergences, each: what diverges, why it matters, action implication
9. **Sources Footer**

---

## Tone & Sentiment Analysis (1-2 pages)

**Header right cell:** "Tone & Sentiment Analysis | [Start] – [End]"

### Layout
1. **Header Bar**
2. **OVERALL TONE ARC** — 1 paragraph summary of trajectory
3. **CONFIDENCE TREND** — Quarter-by-quarter with visual indicators (▲▲▲ / ▲▲ / ▲ / — / ▼ / ▼▼ / ▼▼▼). Implement as a compact table: Quarter | Confidence | Key Evidence
4. **SPECIFICITY TREND** — Tracking precision of management's forward statements. Same visual indicator format.
5. **TOPIC MAP** — What appeared, what disappeared. Two-column table: "Emerged" | "Dropped Off" with quarter notations.
6. **RED FLAGS & GREEN FLAGS** — 3-5 specific linguistic signals. Bold signal text, normal explanation. Use green/red accent colors.
7. **Sources Footer**

---

## Guidance Tracker Scorecard (1-2 pages)

**Header right cell:** "Guidance Tracker | [Start] – [End]"

### Layout
1. **Header Bar**
2. **CREDIBILITY SUMMARY** — 1 paragraph overall assessment with delivery percentage
3. **COMMITMENT SCORECARD** — Full-width table with columns:
   - Commitment (text, 40% width)
   - Quarter Made (10% width)
   - Due By (10% width)
   - Outcome (15% width) — color-coded: Delivered (green), Partial (amber), Missed (red), Pending (gray), Not Addressed (red italic)
   - Evidence (25% width)
4. **PATTERN ANALYSIS** — Prose paragraphs identifying systematic patterns in what gets delivered vs. missed
5. **CREDIBILITY IMPLICATIONS** — What the track record means for evaluating current guidance
6. **Sources Footer**

### Scorecard Color Coding
- Delivered: cell text in #2E7D32 (forest green)
- Partially delivered: cell text in #F57F17 (amber)
- Missed: cell text in #C62828 (deep red)
- Pending: cell text in #757575 (gray)
- Not addressed: cell text in #C62828 (deep red), italic

---

## One-Page Constraint (On-Demand only)

Strategies to fit on a single page:
1. Write tight — eliminate filler, use abbreviations (YoY, QoQ, bps, mgmt)
2. Limit takeaways to 2-3 sentences each
3. Limit risk and priority bullets to 1 sentence each
4. Combine announcements and Q&A into one section
5. If still overflowing: reduce all fonts by 0.5pt
6. Last resort: drop one Q&A highlight or one priority bullet
