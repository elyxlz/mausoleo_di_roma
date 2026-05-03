# Round 58 plan

## 1. Prior-round (R57) lesson

R57 regressed because each surface scrub REPLACED a tell with a same-class tell. The R54 + R55 PASSes worked because edits were pure deletions or fold-ins, not rewrites that introduced new shapes.

## 2. Pattern across last 10 rounds (R48-R57)

R48 1/3, R49 1/3, R50 0/3, R51 1/3, R52 0/3, R53 0/3, R54 1/3 (pure deletion of meta-claims), R55 1/3 (pure deletion of meta-claims + fold-in of closers), R56 0/3, R57 0/3.

Pattern: PURE DELETIONS work; REWRITES often produce same-class tells.

## 3. Highest-leverage move (R58) — pure deletions only

PRIMARY: delete two single sentences flagged across rounds for which the surrounding text remains coherent without them:

(a) **§2.3 "On the neural side the recent work shows that the same hierarchical-relational organisation extends from space to time and concept."** (line 68 paragraph opener) — flagged in R52 + R53 as "On the neural side" discourse-marker. The next sentence ("Tolman (1948) showed that rats build *cognitive maps* exceeding stimulus-response chains.") works as paragraph opener.

(b) **§1 paragraph 27 sentence "What the interface cannot do is register that the absent day is part of the corpus's testimony, the editorial silence of twenty-four hours of regime transition."** — self-narrating meta-claim. Flagged in multiple rounds as "X holds Y" / "X does Y" abstract-noun-as-agent construction. The previous sentence ("Historians have always read around such gaps...") and the next ("A narrower question about the editorial-register shift...") both work without it.

SECONDARY: delete one further single sentence:

(c) **§2.2 paragraph 56 closer "On a corpus with a strong native temporal hierarchy this assumption is harder to defend."** — meta-claim that the next sentence already makes concretely. The next sentence ("For a question about a regime collapse...") carries the argument.

## 4. Predicted downstream effects

R58 deletes three sentences without rewriting anything, removing three flagged tells without introducing new shapes. Net word count drops by ~50, well under the ceiling.

If R58 lands 2/3, real BEST_GAN bump.

## 5. Fallback (R59)

If R58 regresses: revert to R55, delete only ONE of the three sentences and re-test.

If R58 ties at 1/3: continue with another pure-deletion round on a different sentence cluster.
