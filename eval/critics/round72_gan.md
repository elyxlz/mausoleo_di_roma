# GAN Round 72 — STRATEGY 3 (cross-model rewrite via Haiku 4.5)

Strip: TARGET 5,849 words (cross-model v10 6,721 words).
v10 = R61 baseline (commit 420027e). Cross-model file = `/tmp/gan_round72/v10_cross_model.md`.
Seeds: 938758483 (pos 5), 343602729 (pos 8), 647833258 (pos 2).

## Edits applied (BEFORE the revert)

§3 (Chapter 3: How Mausoleo is built, ~1,321w) and §5 (Chapter 5: Discussion paras 1-3, ~346w) regenerated via Claude Haiku 4.5 (different model class from
the Opus 4.7 critic), with a research-engineer-persona system prompt and an
explicit prohibitions list (no balanced antithesis with semicolon pivot, no
aphoristic closers, no "X handles Y, awkward for Z", no "Inputs are X.
Outputs are Y." parallel openers, no em-dashes, no " - " separator).

Sanity check on each rewrite enforced: all citations preserved, all numerics
preserved, all keywords (Mausoleo, ClickHouse, etc.) preserved, word count
within ±15%, no em-dashes, no " - ".

§3: 2 attempts (first lost Ketelaar's 2001 cite, second OK at 1,335w = +1%).
§5: 1 attempt OK at 329w = -5%.

Sonnet 4.5 was tried first but hit hard rate-limit on 6 consecutive attempts.
Haiku 4.5 worked first try.

Splice: §1 + §2 + §4 + §5 closer all preserved verbatim from R61. Headers and
table preserved verbatim. Final word count 6,721 (vs R61's 6,724).

## Verdicts

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 938758483 | 5 | 5 (TARGET) | near certain | FAIL |
| 343602729 | 8 | 8 (TARGET) | near certain | FAIL |
| 647833258 | 2 | 2 (TARGET) | lean toward ("unusually well-camouflaged") | FAIL |

Result: **0/3 PASS** but with one lean-toward (R72 ties R63/R65/R66/R69 at
FAIL_LEAN_NEAR pattern).

PER PARETO RULE: v10 stays at R61 baseline (commit 420027e). No commit to v10.

## Why R72 didn't break 2/3

The cross-model rewrite produced fluent, register-appropriate prose (no garble,
no grammar drift, all citations + numerics preserved). One seed visibly softened
to lean-toward with the qualifier "unusually well-camouflaged". But the other
two seeds keyed on tells in sections NOT touched by R72:
- §1 closer "and the issue did not run." reads as setup-for-aphorism cadence
- §2.3 cognitive-science argument spine retains balanced antithesis
- §4.1 missing-26-July Italian quotation block flagged as "too-perfect framing"
- §4.3 closer + §4.2 retain three-case symmetric experimental design
- §5 paragraph 4 closer still in place ("compression too is part of what the
  index records about July 1943") — explicitly flagged as "ring-composition
  ending" + "single most AI-feeling move"

## Key R72 lesson

**Cross-model rewrite of §3 + §5 alone is insufficient because the universal
tells span the entire dissertation, not just §3 + §5.** The R72 critic explicitly
called out the §5 para 4 closer (which we deliberately preserved as cohort-mirror)
as the worst single tell. That signal is unambiguous: the closer must go OR the
§1 + §2 + §4 surface must also shift.

## R73 plan: extend cross-model rewrite scope

R73: re-run cross-model rewrite via Haiku 4.5 on the WIDER set:
- §1 (Chapter 1: A missing newspaper) — full chapter
- §2.1 (Existing digitised newspaper archives) — 2 paragraphs
- §2.2 (The hierarchical-retrieval lineage) — 4 paragraphs
- §3 (Chapter 3: How Mausoleo is built) — re-rewrite
- §5 paragraphs 1-3 — re-rewrite
- §5 paragraph 4 closer — REWRITE this time (explicitly flagged in R72)

NOT touched (cohort-mirror PASS-cited preserves):
- Preface (R61 PASS critic praised it)
- Abstract (load-bearing positioning)
- §2.3 cognitive-science spine (load-bearing argument; preserve for argument
  integrity even if it carries some surface tells)
- §2.4 (the corpus and its source-critical context — a single paragraph)
- §4.1 missing 26 July (Italian quotation block + the OCR engineering
  frustration both PASS-cited as positive cohort-mirror)
- §4.2 + §4.3 (case studies + table — preserve numerical results verbatim;
  paraphrase only the wraparound prose)

Total target: ~3,500 words via cross-model. Network risk: rate limits if Haiku 4.5
queue gets saturated.

## Decision logic

If R73 lands 3/3: STOP.
If R73 lands 2/3: COMMIT new BEST.
If R73 lands 1/3: try R74 with abstract + Preface paraphrase too.
If R73 lands 0/3: SHIP R61 as final.
