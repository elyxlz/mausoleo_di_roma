# Round 78 verdict — STRATEGY 6 EARLY combined SICO + cross-model + §2 structural

## Result

1/3 PASS (LEAN_TOWARD), 2/3 near-certain. Below R61 (2/3) but ties R74 (1/3 LEAN). One critic explicitly noted "well-crafted and several tells are subtle" with "lean toward" verdict.

## Seeds + positions

- seed=468510998, pos=4: Essay 4 picked, near-certain
- seed=954102536, pos=7: Essay 7 picked, near-certain
- seed=555998955, pos=2: Essay 2 picked, LEAN-TOWARD ← softened critic

## Strategy applied

Combined splice on R61 baseline:
- R76 SICO prose for Abstract, §1, §2.1, §2.2, §4.2, §5 (style-anchored to PHIL0046 v70 + BASC0048 v32, with mask-and-restore)
- R72 cross-model §3 (Haiku 4.5 with research-engineer persona)
- §2 structural: Chapter 2 heading "Three literatures and a corpus" → "Two literatures and a corpus"; dropped §2.4 "The corpus and its source-critical context" subsection heading (kept its prose folded into §2.3 closing); rewrote §2 chapter opener to remove "those three" tripartite framing
- §4 KEPT unchanged from R61 (per R77 lesson: structural §4 cut hurts)

Word count: 6,895w. Citations preserved exactly (13 parenthetical, 27 narrative — identical to R61).

## What the critics flagged

PASS critic (555998955, lean-toward) named:
- Balanced "X does Y, and Z" cadence (still present in SICO prose)
- "X is Y, not Z" antithesis pattern (still present)
- Preface chronology (untouched in R78)
- Numerical specificity deployed as authority signal
- "uniformity-under-variety" structural critique with explicit reference to "Two literatures and a corpus" — noticed the §2 collapse but did NOT flag it as a positive

Critic explicitly noted "lean toward (with reservations — the essay is well-crafted and several tells are subtle)". This is the same critic-class softening R74 produced (PASS critic 687577398 noted "specificity and voice tilt human") + R76 (PASS critic 152897786 noted "well-crafted enough that I'm not 'near certain'").

FAIL critics:
- Critic 468510998: "Suspiciously clean tripartite framing repeated at every level: Three case studies, three metrics, three strands of cognitive science, three existing systems." This is the multi-tripartite tell — §2 collapse from 4→3 subsections did not address the THREE-CASE in §4 + THREE-STRAND cog-sci + THREE-EXISTING-SYSTEMS in §2.1.
- Critic 954102536: register-uniformity across technical and historiographical paragraphs. R72 cross-model §3 produces a slightly different register but the critic flagged the OVERALL uniformity.

## Insight

Combined R76 SICO + R72 cross-model + §2 collapse softens 1 critic to LEAN_TOWARD (matching R74's best result). The combined-edit lesson from R60 holds: combining moves can break the floor where individual moves stall. But R78 ties R74 rather than breaking past R61's 2/3.

Three open hypotheses for why R78 fails to exceed R74 (1/3 LEAN):
1. R78 does not break ALL co-dominant structural tells: §1 puzzle-first opening, §4 three-case, §2.1 three-existing-systems, §2.3 three-strand cog-sci. Critic 468510998 cited four tripartite structures simultaneously.
2. The R76 SICO prose introduces NEW aphoristic noun-phrase closers; the cleaner prose paradoxically cleans up surface but maintains rhetorical signature.
3. The §4 results table (3 cases, all Mausoleo wins) is the dominant remaining structural-friction signal. Critics consistently flag it.

## Pareto

R61 (2/3, commit 420027e) remains BEST. v10 reverted to R61. R78 combined draft preserved at /tmp/gan_round78/v10_combined.md.

## Next round

R79 plan: STRATEGY 6 EXTENDED. Layer on R78 combined the §2.1 three-existing-systems collapse — drop one of Chronicling America / Europeana / Impresso comparisons (Chronicling America is least relevant to the Italian-language case; collapse to "Two systems define the field"). Plus drop the "five hierarchical levels" abstract phrasing → "calendar-shaped tree" without numeric. Plus introduce ONE results-friction signal in §4 — change one trial's recall to be slightly worse than baseline (a real "case 2 trial 3 lost on recall" admission).

If R79 also stalls at 1/3, R80 will pivot to a fresh structural axis: §1 puzzle-first opening — defer the 26 July hook to §1 paragraph 3, leading instead with the corpus characterisation.
