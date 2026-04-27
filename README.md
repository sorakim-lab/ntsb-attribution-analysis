# NTSB Attribution Analysis

Computational analysis of attribution patterns in NTSB aviation accident reports (1982–2025): coding-level and grammatical-level evidence of organizational accountability displacement.

> *"Attribution is not discovered; it is designed."*

## Overview

This repository contains a two-phase analysis of how the U.S. National Transportation Safety Board (NTSB) attributes responsibility in aviation accidents:

- **Phase A** examines NTSB's structured *Findings* coding (n = 71,114 findings, 14,940 events).
- **Phase B** examines the *grammatical* structure of NTSB probable-cause statements (n = 23,742 statements, dependency parsing via spaCy).

The two phases use independent methods and units of analysis but converge on the same finding: NTSB systematically displaces organizational accountability — first by withholding it from the evidentiary record, then by demoting it to "contributing" status when it does appear.

## Key Findings

### Phase A: Coding-level analysis (Findings table)

1. **Category-level asymmetry.** Personnel and Aircraft findings concentrate as Cause (C/F = 5.83 and 13.46 respectively). Organizational findings reverse this pattern (C/F = 0.36). Chi-square = 2,863, p < 0.001; standardized residual for Organizational × Factor = +34.14.
2. **Strengthening over time.** Aircraft C/F multiplied 4× from 2005-2009 (9.40) to 2020-2024 (46.25); Personnel multiplied 2.6×. Organizational C/F has remained at 0.3–0.4 for 40 years.
3. **Sub-category demotion.** Among organizational findings, those addressing oversight, regulatory enforcement, and safety program adherence are most systematically classified as Factor rather than Cause (C/F = 0.00–0.14).
4. **Classification regime collapse.** From 2008–2018 the Cause/Factor classification rate was stable at ~85%. Beginning 2019 it declines monotonically; from 2021 onward, NTSB no longer classifies findings as either Cause or Factor (100% unclassified, 2021–present).
5. **Double displacement.** Across 14,940 accident events (2008–2018), only 0.58% (n = 87) identify any organizational issue as Cause. Of the 2.0% with any organizational finding, 70.8% are coded as Factor only.

### Phase B: Grammatical-level analysis (probable-cause statements)

6. **Subject distribution.** Across 23,742 probable-cause statements, the grammatical subject is an individual actor (pilot, instructor, mechanic, etc.) in 73.99% of cases. Organizational subjects (manufacturer, government, etc.) appear in 0.42%. Individual:Organizational ratio = 177:1.
7. **Clause-level demotion.** When statements contain a "Contributing" clause, organizational actors appear in the contributing clause 6× more often than in the main clause (2.05% vs. 0.35%).
8. **Temporal invariance of the genre.** Individual attribution remained at 71.7%–74.7% across 2005–2024 (range: 3 percentage points). Organizational attribution declined 5.5× from 0.89% (2005-09) to 0.16% (2020-24), preceding the formal classification cessation observed in Phase A.
9. **Severity inversion.** In fatal accidents, individual attribution rises to 81.32% (vs. 73.78% in no-injury accidents) while mechanical attribution drops from 17.78% to 11.56%. NTSB redirects attribution from machines to humans when fatalities are involved.

### Triangulation

| Phase | Method | Unit | Organizational share |
|---|---|---|---|
| A | Cause/Factor coding | Events | 0.58% |
| B | Dependency parsing | Cause statements | 0.42% |

Two methods, two units — same finding.

## Repository Structure
