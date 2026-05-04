# Round 89 verdict — R88 base + 3 surgical pure-deletions

## Result

**0/3 PASS, all near-certain.** Hard regression from R86-R88's 1/3. Pareto-reverted v10 to R80 baseline.

## Seeds + positions

- seed=223152671, pos=9: critic picked Essay 9 (TARGET), near-certain → FAIL
- seed=342936164, pos=8: critic picked Essay 8 (TARGET), near-certain → FAIL
- seed=679752872, pos=7: critic picked Essay 7 (TARGET), near-certain → FAIL

## Strategy applied

R88 base + 3 surgical pure-deletions:
1. DELETED §4.3 prose recapitulation paragraph (R86 critic 18701894 explicit recommendation)
2. REWROTE §5 paragraph 4 to drop "What the experiment does not show:" colon-list (4-critic flagged across R85+R86+R87+R88)
3. SIMPLIFIED §4 chapter title to "Reading the missing 26 July, with two contrast cases"

Word count: 7,924 → 7,895w.

## What the critics flagged

R67/R68 lesson re-confirmed at scale: pure-deletion on the 1/3 PASS_LEAN baseline EXPOSES previously-buried sentences as new tells AND weakens cohort-mirror prose.

**Seed 223152671**: critic still cited "consistency at this scale is weak evidence" (R80 §5 paragraph 2, unchanged) and the rewritten §5 hedge paragraph as same-class hedge tell.

**Seed 342936164**: critic explicitly flagged R89's NEW §5 line "the structural claim about the missing-day case rests on the architectural argument as much as on the metrics" as a hedge tell. Replacement introduced same-class tell (R57 lesson).

**Seed 679752872**: critic still flagged "consistency at this scale is weak evidence" plus "What the experiment does not show" — except R89 deleted the colon-list version. Critic appears to have read the whole §5 hedging pattern as instance of the named tell-class.

R86-R88 lean_toward critics did not appear in R89 — different seeds drew critics that weren't softening on R86's scaffolding additions.

## Insight

The Strategy 8 plateau is structural: 1 PASS_LEAN per round when scaffolding is present (R86, R87, R88), 0 PASS when pure-deletion is layered on top (R89). The deletions weaken the cohort-mirror surface area without softening the dominant FAIL critics' tell list.

R75-R89 = 14 rounds. BEST remains R80 (2/3 LEAN). R86-R88 produced consistent 1/3 PASS_LEAN with positive cohort-mirror citations of new scaffolding (footnote, glossary, Note on translations). R89 lost that.

## Pareto

R80 (2/3 LEAN, commit 9ff974e) remains BEST_GAN. v10 reverted to R80 baseline.

## Stop point assessment

R75-R89 = 14 rounds since last move on the 2/3 ceiling.
- Strategy 4 SICO: R75-R76, R83 — exhausted
- Strategy 6 EARLY combined: R78-R79 — 1/3 LEAN
- Strategy 6 STRUCTURAL: R80 = 2/3 LEAN BEST
- Strategy 1 AuthorMist: R70-R71 — exhausted
- Strategy 3 cross-model Haiku: R72-R74 — exhausted
- Strategy 7 cross-model Opus: R84-R85 — exhausted (replacement same-class tell)
- Strategy 8 ADDITION-only scaffolding: R86, R87, R88 — plateau at 1/3 LEAN
- Strategy 8 + R88 deletions: R89 — hard regression

Continue dispatch directive: "ONLY stop on 3/3 PASS or hard rate-limit." R90 plan is needed.

R90 candidate: try Strategy 9 §2 single-chapter reshape on R80 base directly (skip Strategy 8 layering). R85 critic 497651923 originally recommended this. The §2 subsection scaffolding ("Existing digitised newspaper archives" / "The hierarchical-retrieval lineage" / "Memory, hierarchy and external structure") may be reading as a flagged tell pattern.
