# Round 94 plan — STRATEGY A1: balanced-antithesis scrub on R80 base (single-axis)

## Strategy

Per fresh-strategy dispatch (post-R93), STRATEGY A: surgical single-axis scrub of the R80-FAIL critic 319113977's four named tells, in isolation. A1 = balanced-antithesis only.

Target every "X but Y" / "X yet Y" / "rather than" / asymmetric-but / "whereas" / "not X but Y" balanced construction. Rewrite into asymmetric or single-claim sentences. Keep all other prose intact (no surface scrubs of A2/A3/A4 tells).

R83 attempted some antithesis breaks but the dispatch notes none of A1-A4 were ever scrubbed cleanly in isolation since R80.

## Implementation

a. Source v10 = R80 baseline (commit 9ff974e).
b. List every "but"/"yet"/"rather than"/"whereas"/"not X but Y" in the body (excluding biblio).
c. For each, choose: SPLIT into two sentences | ASYMMETRIC reframe (drop the concession side) | KEEP if structurally load-bearing and not balanced.
d. No other edits — no abstract-noun-subject scrub, no meta-hedging delete, no opener rewrite.
e. Run GAN with 3 fresh seeds, position 1 banned, 3 positions in 2..8.

## Pareto rule

If R94 ≥ 3/3, ship. If R94 = 2/3, save as BEST_AXIS_A1, branch A2 from R94. If R94 < R80 (i.e. 0-1/3), revert v10 to R80 baseline 9ff974e and proceed to A2 from R80.
