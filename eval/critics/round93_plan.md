# Round 93 plan — R86 additions + R92 deletions combination

## Strategy

R86 additions (Note on translations + footnote + §3 rename) produced 1 lean_toward FAIL per round R86, R87, R88, R90.
R92 deletions (§5 hedge + §1 closer) produced 1 PASS_LEAN.

Both interventions independently soften critics. The combination has not been tested. R91 was a different combination (R86 + §2 reshape + asymmetric §4) that hard-regressed because it added MORE prose (the asymmetric §4 expansion was 150w of new prose). R93 combines R86 ADDITIONS (already validated) with R92 DELETIONS (already validated).

This is meaningfully different from R91: R91 added 440w net; R93 adds ~85w net (R86 ~165w - R92 ~76w).

## Implementation

a. Source v10 = R80 baseline.
b. Apply R86 base: Note on translations + Grandi footnote + §3 chapter rename.
c. Apply R92 deletions: drop §5 paragraph 4 + drop §1 closer.
d. Strip + GAN.

## Word count target

R80 7,124 + 165 - 76 = ~7,213w. Within cap.

## Pareto rule

If R93 ≥ 2/3, promote v10. If R93 = 3/3, ship. If R93 < 2/3, revert.
