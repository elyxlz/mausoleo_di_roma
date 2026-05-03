# Round 56 plan

## 1. Prior-round (R55) tells

R55 1/3 PASS at pos 5 (lean-toward). Five R54-flagged tells cleanly defused with no negative signal. PASS critic cited TARGET's R54 month-level closer as positive structural exemplar.

NEW high-leverage tells from R55 verdicts (NOT yet addressed in v10):
- "**Pre-emptive limitation hedging woven into body prose**" — seed 379838795 cites *"How a human reader actually engages with the corpus is a separate question that this design has motivated rather than tested"* (Ch5 mid-paragraph, line 167 in v10). R53 deleted this; R53 was reverted. R54 + R55 baselines never re-deleted it.
- "**Self-referential meta-claim**" — seed 379838795 cites *"Why the calendar-given hierarchy should be the right shape of index for an archival interface, rather than just one designer's preference, is the substantive cognitive-science claim the dissertation rests on"* (§2.3 opener, line 62).

## 2. Pattern across last 8 rounds (R48-R55)

R48 1/3, R49 1/3, R50 0/3 (revert), R51 1/3, R52 0/3 (revert), R53 0/3 (revert), R54 1/3 clean, R55 1/3 clean.

Two clean rounds in a row. The closer-defusion + meta-commentary scrubs class is producing reliable progress. Continue.

## 3. Highest-leverage move (R56)

PRIMARY: **Delete Ch5 hedge** "How a human reader actually engages with the corpus is a separate question that this design has motivated rather than tested." (line 167 mid-paragraph). Single-sentence deletion. The paragraph already moves to "The summariser also adds material that the underlying issues did not contain..." which reads cleanly without the hedge.

SECONDARY: **Defuse §2.3 opener self-referential meta-claim** "Why the calendar-given hierarchy should be the right shape of index for an archival interface, rather than just one designer's preference, is the substantive cognitive-science claim the dissertation rests on. Several converging strands from cognitive science support it." -> Rewrite to a flat factual opener: "Several converging strands from cognitive science support the choice of a calendar-given hierarchy for an archival interface."

Both edits target NEW high-leverage tells with no risk of duplicate-hedge introduction. R53's deletion of the same Ch5 hedge was clean (the negative signal in R53 came from elsewhere, namely the surviving Ch5 closer that R54 has since rewritten).

## 4. Predicted downstream effects

R56 PRIMARY removes a hedge that has been on the flag list since R52 — net unambiguously positive at the closer-tell level. R56 SECONDARY removes the "the dissertation rests on" self-referential framing AND the "converging strands... worth taking in turn" four-beat enumeration (R53 already neutralised "worth taking in turn"; the R55 baseline still has the rest).

If R56 lands 2/3, real BEST_GAN bump.

## 5. Fallback (R57)

If R56 regresses: revert to R55 (commit 4c3e1b3), try defusing the §2.3 opener differently or skip it.

If R56 ties at 1/3: layer in defusion of the §2.2 closer "Mausoleo borrows its hierarchy from the publication calendar that the printers already followed" (flagged by R55 critic 379838795 as appositional summary clause).
