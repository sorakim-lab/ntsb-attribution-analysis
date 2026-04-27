# NTSB Attribution Analysis

Computational analysis of attribution patterns in NTSB aviation accident reports (1982–2025): coding-level and grammatical-level evidence of organizational accountability displacement.

> *"Attribution is not discovered; it is designed."*

## Overview

This repository contains a two-phase analysis of how the U.S. National Transportation Safety Board (NTSB) attributes responsibility in aviation accidents:

- **Phase A** examines NTSB's structured *Findings* coding (n = 71,114 findings, 14,940 events).
- **Phase B** examines the *grammatical* structure of NTSB probable-cause statements (n = 23,742 statements, dependency parsing via spaCy).

The two phases use independent methods and units of analysis but converge on the same finding: NTSB systematically displaces organizational accountability — first by withholding it from the evidentiary record, then by demoting it to "contributing" status when it does appear. A third pattern, visible only when both phases are read together, is that the attribution genre itself shifts in response to changes in the formal classification regime.

## Key Findings

### Phase A: Coding-level analysis (Findings table)

1. **Category-level asymmetry.** Personnel and Aircraft findings concentrate as Cause (C/F = 5.83 and 13.46 respectively). Organizational findings reverse this pattern (C/F = 0.36). Chi-square = 2,863, p < 0.001; standardized residual for Organizational × Factor = +34.14.
2. **Strengthening over time.** Aircraft C/F multiplied 4× from 2005-2009 (9.40) to 2020-2024 (46.25); Personnel multiplied 2.6×. Organizational C/F has remained at 0.3–0.4 for 40 years.
3. **Sub-category demotion.** Among organizational findings, those addressing oversight, regulatory enforcement (FAA), and safety program adherence are most systematically classified as Factor rather than Cause (C/F = 0.00–0.14).
4. **Classification regime collapse.** From 2008–2018 the Cause/Factor classification rate was stable at ~85%. Beginning 2019 it declines monotonically; from 2021 onward, NTSB no longer classifies findings as either Cause or Factor (100% unclassified, 2021–present).
5. **Double displacement.** Across 14,940 accident events (2008–2018, the clean classification window), only 0.58% (n = 87) identify any organizational issue as Cause. Of the 2.0% with any organizational finding, 70.8% are coded as Factor only.

### Phase B: Grammatical-level analysis (probable-cause statements)

6. **Subject distribution.** Across 23,742 probable-cause statements, the grammatical subject is an individual actor (pilot, instructor, mechanic, etc.) in 73.99% of cases. Organizational subjects (manufacturer, government, etc.) appear in 0.42%. Individual:Organizational ratio = 177:1.

7. **Clause-level demotion.** When statements contain a "Contributing" clause, organizational actors appear in the contributing clause 6× more often than in the main clause (2.05% vs. 0.35%).

8. **Temporal pattern.** Five 5-year buckets (2025 contains a single calendar year, n = 617):

   | Bucket | n | Individual % | Mechanical % | Organizational % |
   |---|---|---|---|---|
   | 2005–09 | 3,265 | 74.70 | 16.11 | 0.89 |
   | 2010–14 | 7,383 | 74.14 | 17.43 | 0.60 |
   | 2015–19 | 6,705 | 74.57 | 17.23 | 0.22 |
   | 2020–24 | 5,772 | 71.71 | 19.44 | 0.16 |
   | 2025 (partial) | 617 | 83.31 | 10.05 | 0.32 |

   For 20 years (2005–2024), individual attribution stayed in a 3-point band (71.7–74.7%), mechanical attribution drifted upward (16.1 → 19.4%), and organizational attribution declined monotonically by an order of magnitude (0.89 → 0.16%). In 2025 all three patterns break simultaneously: individual jumps +11.6 points to 83.3%, mechanical falls -9.4 points to 10.0%, and organizational reverses direction (0.16 → 0.32%).

9. **Severity inversion.** Within the clean window (2008–2024 statements with severity codes), individual attribution rises to 81.32% in fatal accidents (vs. 73.78% in no-injury accidents), while mechanical attribution drops from 17.78% to 11.56%. NTSB redirects attribution from machines to humans when fatalities are involved.

### Cross-phase pattern: regime change is visible at both levels

Phase A finding 4 documents that NTSB stopped classifying findings as Cause/Factor in 2021. Phase B finding 8 shows that 2025 — the only bucket fully inside that post-classification regime — is also the only bucket that breaks the 20-year grammatical pattern. The two shifts align in time:

- Coding-level (Phase A): Cause/Factor classification rate drops from ~85% (2008–2018) to 0% (2021+).
- Grammatical-level (Phase B): The 20-year stable distribution of subjects breaks in 2025 — individual concentration intensifies, mechanical attribution collapses, organizational attribution stops declining.

The 2025 bucket is a single year of data and cannot on its own establish a new trend. But its alignment with the formal regime change is what the project's central claim predicts: if attribution is designed rather than discovered, then changes in the classification apparatus should be detectable in the language NTSB uses. The 2025 break is the first place this prediction can be tested, and the direction of the break is consistent with it.

### Triangulation

| Phase | Method | Unit | Window | Organizational share |
|---|---|---|---|---|
| A | Cause/Factor coding | Events | 2008–2018 | 0.58% |
| B | Dependency parsing | Cause statements | 2005–2025 (full corpus); severity sub-analysis: 2008–2024 | 0.42% |

Two methods, two units — same finding on the cross-sectional structure, and a co-occurring shift on the temporal axis.

## Repository Structure

- `notebooks/01_ntsb_phase_a.ipynb` — Coding-level analysis
- `notebooks/02_ntsb_phase_b.ipynb` — Grammatical-level analysis
- `figures/` — Paper-quality visualizations
- `data/phase_b_actors_v2.csv` — Extracted actors per cause statement
- `data/phase_b_temporal.csv` — Temporal distribution (5 buckets, 2005–2025)
- `data/phase_b_severity.csv` — Severity distribution (2008–2024 clean window)
- `data/phase_b_validation_sample.csv` — Manually annotated random sample (n = 100) supporting the accuracy estimate reported below

## Data

The primary data source is the NTSB Aviation Accident Database (`avall.mdb`), publicly available at:

- https://www.ntsb.gov/Pages/AviationDownloadDataFiles.aspx

The database is not redistributed in this repository (~546 MB). All findings reported here are reproducible by downloading the database directly from NTSB.

## Methods

### Phase A
Direct queries against the `Findings` table joined with the `events` table. Cause/Factor flags compared across category codes (01 Aircraft, 02 Personnel, 03 Environmental, 04 Organizational). Chi-square tests of independence with standardized residuals for cell-level significance. Temporal aggregation uses 5-year floor buckets (`year // 5 * 5`). Severity and event-level analyses are restricted to 2008–2018 because Cause/Factor coding is required for these analyses and the classification regime breaks down beginning 2019 (Phase A finding 4).

### Phase B
spaCy `en_core_web_sm` (v3.8.0) dependency parsing of the `narr_cause` field. Statements with fewer than 50 characters of narrative text are excluded as non-substantive (n = 23,742 retained out of all non-null statements). Actor extraction proceeds via three strategies in order of priority: (1) `poss` dependency tokens (e.g., "the pilot's failure"), (2) prepositional `of` patterns (e.g., "failure of the pilot"), (3) first non-determiner noun chunk as fallback. Extracted actors are filtered against an action-noun blocklist (`failure`, `loss`, `lack`, etc.) and categorized via four whitelists: human individual, organizational, mechanical, other. Phase B severity analysis uses 2008–2024 because narrative text is unaffected by the Phase A classification regime change; the asymmetric window with Phase A is therefore intentional.

### Validation
A random sample of n = 100 statements was drawn (`random_state=42`) and manually annotated for extraction correctness; see `data/phase_b_validation_sample.csv` for the annotated sample. Overall extraction accuracy was approximately 91%, with errors concentrated in the smallest categories (organizational and mechanical), where misclassification has the largest proportional effect on reported percentages.

## Limitations

- **Phase A regime change.** The cessation of Cause/Factor classification in 2019–2021 limits direct longitudinal comparison; clean-window analyses use 2008–2018.
- **Partial 2025 bucket.** The 2025 bucket in Phase B contains only one calendar year (n = 617). It is reported in full alongside the four complete 5-year buckets, but a single year is insufficient to establish a new trend; its alignment with the post-2021 classification regime is suggestive, not confirmatory.
- **Whitelist ambiguity.** Two terms in the actor whitelists are inherently context-dependent: `operator` can refer either to an individual ("aircraft operator" = pilot) or to an organization ("commercial operator" = airline), and `maintenance` can refer to a person ("maintenance personnel") or an organizational function ("maintenance department"). In the current code, `operator` is classified as individual because `HUMAN_INDIVIDUAL` is checked before `ORGANIZATIONAL` in the categorization function, which has the effect of excluding commercial operators from the organizational count; `maintenance` is classified as organizational. This means the reported organizational share is, if anything, a lower bound. A sensitivity check varying these assignments would tighten the bound; this is left to future work.
- **Compound subjects.** Phase B extraction has known failure modes for compound-subject statements ("pilot and instructor's failure...") and for statements with no human or organizational agent ("loss of engine power"). The ~91% accuracy estimate from manual validation reflects these failures.
- **Scope.** This work analyzes NTSB outputs only. Future work integrates NTSB CAROL recommendations (n = 5,240, downloaded but not analyzed in this repository) and FAA response correspondence to examine the full regulatory cycle.

## Citation

If you reference this work, please cite as:

Kim, S. (2026). *NTSB attribution analysis: Coding-level and grammatical-level evidence of organizational accountability displacement.* GitHub repository. https://github.com/sorakim-lab/ntsb-attribution-analysis

## Contact

Sora Kim — [sorakim-lab.github.io](https://sorakim-lab.github.io)
