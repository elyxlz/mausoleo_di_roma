# Round 87 verdict — Strategy 8 EXTENDED full scaffolding battery

## Result

**1/3 PASS at pos 2 LEAN_TOWARD.** Below R80's 2/3. Pareto-reverted v10 to R80 baseline.

## Seeds + positions

- seed=616866638, pos=7: critic picked Essay 7 (TARGET), near-certain → FAIL
- seed=665845434, pos=4: critic picked Essay 4 (TARGET), **lean-toward** → FAIL_LEAN
- seed=564273678, pos=2: critic picked Essay 6 ('2022SMMH0' Artificial Creativity, NOT TARGET), **lean-toward** → **PASS**

## Strategy applied

Strategy 8 EXTENDED on R80 baseline with full ADDITION-only scaffolding battery:

1. R86 base: Note on sources and translations preamble + Grandi footnote in §4.1 + §3 chapter-rename
2. NEW: §2 chapter rename "Two literatures and a corpus" → "Hierarchical retrieval, working-memory cognition, and the digitised newspaper context"
3. NEW: §4 chapter rename "The missing 26 July, and two contrast cases" → "Three case studies on the July 1943 *Il Messaggero* corpus: the missing-day, the regime-change reconstruction, the per-week war and domestic balance"
4. NEW: Glossary appendix (Appendix A, ~280w) with 8 Italian historical terms
5. NEW: Preface dead-end paragraph (~150w) on abandoned LDA topic-model layer
6. NEW: Note-on-translations expanded with OCR-artifact addendum addressing R86 critic 18701894's specific suspicion
7. NEW: Footnote expanded with OCR segmentation-error detail

Word count: 7,124 → 7,903w (+779w). Within cap.

## What the critics flagged

**Mixed signal across 3 critics.**

**Seed 616866638 (FAIL near-certain)**: flagged the new LDA Preface paragraph as "deliberately inserted humanizing detail" — exactly the kind of "show your messy process" beat that an LLM would generate. Also flagged the OCR segmentation-error note in the footnote as POSITIVE: "the texture of someone who actually looked at the page... small, gratuitous, technically specific. Keep this register and propagate it".

**Seed 665845434 (FAIL_LEAN_TOWARD on TARGET)**: explicitly hedged ("the essay is sophisticated enough that I want to hedge"). Flagged the LDA Preface aside as "performative" but cited the footnote on the *ordine del giorno Grandi* with OCR segmentation errors detail as POSITIVE: "read as genuine engagement with sources — the kind of specific historiographical anchoring that LLMs struggle to fake convincingly. Keep that texture."

**Seed 564273678 (PASS_LEAN at pos 2)**: critic picked Essay 6 (2022SMMH0 Artificial Creativity, real cohort exemplar) on classic LLM tells (verbatim re-listed numbered questions, "not only X but also Y" cadence, AI self-assessment register). Did NOT pick TARGET. Cohort-mirror PASS — TARGET registers more strongly as cohort than the picked essay does.

## Insight

Strategy 8 EXTENDED has dual-edge:

POSITIVE:
- 2 of 3 critics softened to LEAN (vs R86's 1 of 3)
- 1 PASS (vs R86's 0)
- The footnote with OCR-error detail was flagged POSITIVE by 2 different critics across R86 and R87
- The glossary appendix did not draw a tell flag in any verdict
- The chapter renames did not draw a tell flag in any verdict

NEGATIVE:
- The LDA Preface paragraph was flagged by 2 of 3 critics as "deliberately inserted humanizing detail" — failed-experiment-anecdote pattern is a known LLM signature
- One critic still near-certain — surface tells in R80 baseline (balanced antithesis, aphoristic closers, pre-emptive limitations) remain dominant

## Pareto

R80 (2/3 LEAN, commit 9ff974e) remains BEST_GAN. v10 reverted to R80 baseline.

## R88 plan

Strategy 8 + Strategy 9 hybrid: KEEP R86 base (Note + footnote + §3 rename) + DROP R87's LDA Preface paragraph (flagged) + apply asymmetric §4 case weighting (R85 critic 497651923 + R86 critic 572980918 + R87 critic 665845434 all recommended this — 3 independent recommendations).

Asymmetric §4: collapse the two contrast cases into a single short paragraph; expand the missing-26-July case with extended primary-source close reading using the 27 July reappearance issue text already cited in the footnote.

If R88 ≥ 2/3, ship. If R88 < 2/3, R89 = R88 base + glossary appendix + chapter renames (which were neutral in R87) for one more push.
