# Round 92 plan — pure-deletion of 2 multi-critic flagged sentences

## Strategy

R75-R91 = 17 rounds. R80 still BEST at 2/3 LEAN. The two consistently flagged sentences across 5+ critics:

1. §5 paragraph 4 "What the experiment does not show: ..." (flagged by R85, R86, R87, R88, R90, R91 — 6 rounds, multiple critics each).
2. §1 closer "Mausoleo borrows its hierarchy from the publication calendar that the printers already followed" (flagged R57, R65, R66, R85, R88, R90, R91 — many critics, many rounds).

R67/R68 lesson says pure-deletion on PASS_LEAN baseline EXPOSES buried sentences. R69 confirms single-edit deletion at noise floor. But R66 individual deletion was clean (no re-flagging) just produced no PASS movement. Worth testing 2-edit minimal pure-deletion on R80 base.

## Implementation

a. Source v10 = R80 baseline.
b. DELETE §5 paragraph 4 entirely ("What the experiment does not show: whether the cost gaps generalise outside July 1943, ...").
c. DELETE §1 closer sentence "Mausoleo borrows its hierarchy from the publication calendar that the printers already followed."
d. Preserve preceding sentence in each location as new closer (no replacement, just truncation).
e. Strip + GAN.

## Word count target

R80 = 7,124w. -50w (§5) -25w (§1 closer) = ~7,049w. Within cap.

## Pareto rule

If R92 ≥ 2/3, promote v10. If R92 = 3/3, ship and STOP. If R92 < 2/3, revert.

## Risk

R67/R68/R69 establish that single + 2-edit pure-deletions on PASS-tied baseline plateau at noise floor. R92 may produce same result. But these 2 sentences are the most-flagged across 17 rounds; if any pure-deletion will work, this should.
