# Round 85 verdict — Strategy 7 EXTENDED 5-paragraph rewrite + calendar-shaped tree refrain reduction

## Result

**0/3 PASS, all near-certain.** Hard regression from R80's 2/3. Pareto-reverted v10 to R80 baseline (commit 9ff974e).

## Seeds + positions

- seed=453989558, pos=8: critic picked Essay 8 (TARGET), near-certain → FAIL
- seed=657766241, pos=7: critic picked Essay 7 (TARGET), near-certain → FAIL
- seed=497651923, pos=3: critic picked Essay 3 (TARGET), near-certain → FAIL

## Strategy applied

Strategy 7 EXTENDED — Opus 4.7 cross-model rewrite via five different distancing system prompts on:
- T1 Abstract para 1 (175w, SYS_A "abstract supervisor caution")
- T2 §1 para 2 (78w, SYS_B "drop antithesis triplet")
- T3 §4.1 closer (180w, SYS_C "drop balanced antithesis closer", kept Pavone/interregno)
- T4 §4 final aggregate (75w, SYS_D "no three parallel sentences")
- T5 §5 para 4 (55w, SYS_E "no 'experiment does not show:' construction")

Plus three deletion-only edits:
- D1: Reduced "calendar-shaped tree" instances from 8 to 2 (Abstract para 1 dropped via T1, plus 4 manual replacements with "the index" / "the tree" / "the hierarchy")
- D2: No Mausoleo italics found in body (already clean)
- D3: Replaced abstract para 2 closer "a slot for documented silence that a flat article index cannot provide" with declarative

All 5 rewrites passed sanity (citations preserved, length ±25% max, no em-dashes). Word count 7,124 → 7,123w (-1w).

## What the critics flagged

R85 traded one tell-class for another (R57 lesson re-confirmed at Strategy 7).

**Seed 453989558:** Flagged the new T1 abstract opener "This dissertation works with the July 1943 Il Messaggero corpus" as "leading with the system, not the puzzle" structural tell. Flagged new T5 "The most consequential limitation here concerns generalisation" as "RLHF safety-prose" hedging.

**Seed 657766241:** Flagged R85 §1 para 3 "One concrete way that hardness shows up is at the date 26 July" as puzzle-first opening even after R80 deferred from para 1 to para 3. Flagged R76 SICO leftover §1 para 6 "The index inherits that structure rather than inducing one" / "Mausoleo borrows its hierarchy from the publication calendar that the printers already followed" as balanced antithesis.

**Seed 497651923:** Flagged the new T1 staccato "X. Y." rhythm "The morning paper for 26 July 1943 was not printed. The Grand Council had deposed Mussolini overnight. No editorial line could be drawn in time. A flat article index returns nothing for that date." as new LLM cadence signature. Flagged "worth taking in turn" / "worth flagging" / "deserves a sentence of its own" metatextual signposts as register tic.

## Insight

Strategy 7 (Opus 4.7 + distancing prompts) at 3 paragraphs (R84) AND 5 paragraphs (R85) both regress 0/3. The distancing prompts replace one LLM register with another LLM register — short staccato declaratives via SYS_B in R85 created NEW "X. Y." cadence signature.

R57 lesson re-confirmed at scale: surface-class scrubs that REPLACE produce same-class tells. Cross-model distancing is a REPLACEMENT operation by definition.

R85 confirms that Strategy 7 has been exhausted across two attempts. Pivot to Strategy 8 (inject human-style scaffolding) is now warranted.

## Pareto

R80 (2/3 LEAN, commit 9ff974e) remains BEST_GAN. v10 reverted to R80 baseline.

## R86 plan

PIVOT to Strategy 8 — inject human-style scaffolding ON R80 baseline:
- Add a "Note on translations" preamble after the Abstract (cohort essays handling foreign-language sources have these; the Italian quotation in §4.1 motivates one)
- Add ONE substantive footnote with a primary-source quotation in §4.1 (cohort historical-research essays use these)
- Add a "Method" subsection heading explicitly named in §3 (cohort essays do)

This is ADDITION not REPLACEMENT, so does not produce same-class tells. R80 surface tells unchanged.
