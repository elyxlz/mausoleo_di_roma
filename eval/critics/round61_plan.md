# Round 61 plan

## 1. Prior-round (R60) tells

R60 1/3 PASS at pos 2, lean-toward. Combined deletion package landed cleanly. NEW BEST_GAN baseline at commit f7c62d6.

NEW high-leverage tells from R60 verdicts:
- "**em-dash-free appositive parentheticals doing definitional work**" — *"ISAD(G) names this archival principle respect des fonds (International Council on Archives, 2000): the source order is preserved beneath the catalogue's own ordering"* (§2.4). The colon-as-gloss after the citation is the tell.
- "**'X rather than Y' formulations**" — flagged across §2.2 ("borrows... rather than", "reads its hierarchy off the surface rather than inducing one") and Ch5 ("motivated rather than tested" inside the surviving Ch5 hedge).

## 2. Pattern across last 13 rounds

R48-R60. Three PASSes at clean baselines (R51, R54, R55, R60). Seven rounds 0/3 (with reverts).

R60 is the new BEST_GAN. R61 layers on top with another pure-deletion class.

## 3. Highest-leverage move (R61)

PRIMARY: pure-delete the §2.4 closer "the source order is preserved beneath the catalogue's own ordering". Drop the colon and the gloss clause; keep only "ISAD(G) names this archival principle *respect des fonds* (International Council on Archives, 2000)."

SECONDARY: pure-delete the Ch5 surviving hedge "How a human reader actually engages with the corpus is a separate question that this design has motivated rather than tested." (R56 deleted this cleanly; R56 regression came from cohort variance, not this edit.)

Both are pure deletions. Both target NEW R60-flagged tells. Cumulative deletion approach.

## 4. Predicted downstream effects

R61 layers two more clean deletions on top of R60. The §2.4 colon-gloss tell is removed; the Ch5 "motivated rather than tested" inside the hedge is removed.

If R61 lands 2/3, real BEST_GAN bump beyond 1/3.

## 5. Fallback (R62)

If R61 regresses: revert to R60 (commit f7c62d6), try only the §2.4 deletion alone.

If R61 ties at 1/3: layer in another pure-deletion target.
