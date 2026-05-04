# Round 96 plan — STRATEGY A3: meta-hedging scrub on best-on-A2 base (single-axis)

## Strategy

Per fresh dispatch STRATEGY A3: delete every "notably / importantly / it must be admitted / one might note / it is worth noting / arguably / by and large / in essence / ultimately" lexical hedge. Keep all other prose intact (no antithesis, no abstract-noun-subject, no opener fixes added beyond prior A1+A2).

## Branch

If R95 ≥ 2/3: branch from R95.
If R95 < R80 and R94 ≥ 2/3: branch from R94.
Else branch from R80 baseline.

## Implementation

a. Grep for every meta-hedge token ("notably", "importantly", "it must be admitted", "it is worth noting", "arguably", "by and large", "in essence", "ultimately", "indeed", "of course", "one might note", "to be sure").
b. Delete each in place; rejoin sentence cleanly. Do NOT replace with another hedge.
c. Preserve "of course" only where it serves as a parenthetical aside that breaks rhythm naturally (cohort-mirror).

## Pareto rule

Same as prior. ≥ 2/3 = save as BEST_AXIS_A3. Else revert to branching baseline.
