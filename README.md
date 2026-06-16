# CSAT Analysis — DoorLoop Support Operations

Internal analysis of DoorLoop's CSAT pipeline, with a focused investigation into Fin AI voice call underperformance (GTM-482).

---

## Files

| File | Description |
|---|---|
| `index.html` | Main CSAT dashboard — open in browser |
| `csat-pipeline-health.html` | CSAT pipeline health report — open in browser |
| `fin-ai-voice-csat-analysis.html` | Fin AI Voice CSAT analysis — open in browser |
| `fin-ai-voice-csat-analysis.docx` | Same analysis as a Word document |
| `fin-ai-voice-csat-summary.md` | Summary of the Fin AI voice investigation |
| `summary.md` | Summary of the CSAT pipeline health analysis |
| `reporting-dataset-export.*.csv` | Raw Intercom reporting data export |

---

## How to use

All HTML files are self-contained — no server required. Download and open directly in any browser.

---

## Project 1 — CSAT Pipeline Health

**Files:** `index.html`, `csat-pipeline-health.html`, `summary.md`

An audit of how CSAT is measured across DoorLoop's support channels, with verified metrics from Intercom Operator. Key findings:

- **Overall CSAT response rate: 15.2%** — surveys are reaching far fewer conversations than raw CSV exports suggest (CSV figures are inflated ~2.3×)
- **Fin AI CSAT: 88.5%** vs **Teammate CSAT: 89.9%** — a 1.4 point gap, not the dramatic difference some GTM tickets implied
- **Chatbot CSAT: 36.8%** (858 responses) — the most urgent quality signal in the report, unrelated to Fin AI
- **Jeremy G outlier:** 70.9% CSAT across 234 responses — 18–25pp below comparable peers, warrants conversation-level review
- **GTM-506 correction:** The "79% Fin CSAT" figure cited in that ticket is almost certainly Intercom's AI-evaluated CX Score, not human CSAT

---

## Project 2 — Fin AI Voice CSAT Investigation (GTM-482)

**Files:** `fin-ai-voice-csat-analysis.html`, `fin-ai-voice-csat-analysis.docx`, `fin-ai-voice-csat-summary.md`

A targeted investigation into why Fin AI's voice CSAT score was flagged at 65% in Linear issue GTM-482 (target: 80%+).

### Key findings

**The 65% is real.** It comes from Confirmed Resolution calls (17 rated, 65% positive). When Fin marks a voice call as resolved and a CSAT survey fires, more than 1 in 3 customers says the issue wasn't actually resolved.

**The bigger problem is the resolution rate.** Fin resolves only 21–29% of voice calls per month, with 60–70% escalating to humans. Escalated calls score 89% — humans are performing well. The gap is entirely in Fin's resolution performance.

### Verified data (Feb–Jun 2026)

| Month | Fin Volume | Resolution Rate | Escalation Rate |
|---|---|---|---|
| Feb 2026 | 346 | 24.9% | 62.4% |
| Mar 2026 | 939 | 24.8% | 62.8% |
| Apr 2026 | 517 | 21.9% | 69.6% |
| May 2026 | 423 | 20.3% | 62.9% |
| Jun 2026 (MTD) | 115 | 28.7% | 60.0% |

| Resolution State | Rated Calls | CSAT |
|---|---|---|
| Confirmed Resolution | 17 | **65%** |
| Assumed Resolution | 2 | 50% |
| Escalated | 37 | **89%** |

### Recommended actions

1. **Investigate why Fin resolves only 21–29% of calls** — Leases (221 escalations) and Deposits (149) are the top escalation topics. Expanding resolution coverage is the highest-leverage action.
2. **Review the 17 confirmed-resolution calls that received CSAT** — 6 of 17 were negative. Manual review or Custom Scorecards (GTM-379) on this specific bucket will identify what Fin is getting wrong.
3. **Fix CSAT survey delivery for resolved calls** — Surveys currently fire on human close, not Fin resolution. Only 3.4% of resolved calls receive a survey. *(GTM-506)*
4. **Instrument the Assumed Resolution bucket** — ~800+ calls, 2 CSAT ratings. Effectively unmonitored. *(GTM-379, GTM-766)*

### Linked Linear issues

`GTM-482` · `GTM-379` · `GTM-506` · `GTM-513` · `GTM-740` · `GTM-766`

---

## Data sources

- **Intercom Fin AI Operator** — volume, resolution rate, escalation rate, CSAT by resolution state
- **Intercom Operator reporting** — 12-month CSAT metrics by channel, agent type, and teammate
- **Intercom REST API** — raw conversation search and filtering
- **Linear** — GTM issue snapshots (GTM-482, GTM-506)

---

*Author: Samuel Huang, Support Operations Analyst — DoorLoop CX*
*Last updated: June 2026*
