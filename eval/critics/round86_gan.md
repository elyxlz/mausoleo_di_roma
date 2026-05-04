# Round 86 verdict — Strategy 8 ADDITION-only human scaffolding

## Result

**0/3 PASS** (3rd at LEAN_TOWARD with explicit "unusually well-camouflaged" qualifier). Below R80's 2/3. Pareto-reverted v10 to R80 baseline.

## Seeds + positions

- seed=18701894, pos=8: critic picked Essay 8 (TARGET), near-certain → FAIL
- seed=572980918, pos=5: critic picked Essay 5 (TARGET), near-certain → FAIL
- seed=848681252, pos=2: critic picked Essay 2 (TARGET), **lean-toward "unusually well-camouflaged"** → FAIL_LEAN

## Strategy applied

Strategy 8 ADDITION-only — three insertions on R80 baseline:

1. **"A note on sources and translations" preamble** (between Abstract and Preface, ~85w): cohort essays handling foreign-language sources have these.
2. **Footnote `[^grandi]` in §4.1** (~75w): primary-source quotation of *ordine del giorno Grandi* opening + reference to Murialdi (1986) discussion of front-page prominence.
3. **Renamed §3 chapter heading** "How Mausoleo is built" → "System architecture: OCR pipeline, calendar tree, and agent interface": multi-clause IMRAD register, less aphoristic.

Word count: 7,124 → 7,311w (+187w). Within cap.

## What the critics flagged

**Strategy 8 partial signal**: Critic 572980918 (FAIL near-certain) explicitly cited the footnote and Note on translations as POSITIVE: *"the footnote about the Grandi ordine del giorno wording in the 27 July reappearance issue, both feel grounded in real source-handling — keep these and the source-language commitment in the 'note on sources' section"*. The scaffolding ADDITIONS landed as cohort-positive, but the surface tells in the underlying R80 prose remained strong.

Critic 18701894 (FAIL near-certain) flagged the new footnote AGAINST the dissertation: *"the footnote 'Il Gran Consiglio del Fascismo, riunitosi nell'attuale grave momento storico...' feel generated rather than transcribed — note the absence of OCR artifacts in a piece supposedly about OCR'd corpora"*. The Italian primary-source quotation was suspected of fabrication despite being attested historically.

Critic 848681252 (FAIL LEAN_TOWARD with "unusually well-camouflaged") — the strongest single positive signal of R75-R86 sequence. Critic spent extensive prose admitting hesitation. Did NOT flag the new scaffolding as tell. Picked TARGET on residual surface tells (balanced antithesis, pre-emptive limitations, "what the experiment does not show" coda).

## Insight

Strategy 8 partial-success: 1 critic explicitly cited the additions as positive, 1 critic was suspicious, 1 critic was hesitant. The mixed signal suggests the ADDITION direction is sound but R86's three additions are insufficient to flip multiple critics.

R86's lean_toward critic notes the "[edizione assente: ...]" Italian summary "reads as confidently composed Italian rather than quoted source material" — same critic's worry about the new footnote text. Even attested primary-source quotations can register as suspicious when they appear without OCR artifacts in a piece about OCR.

R57 lesson does NOT apply to Strategy 8 because the additions don't replace existing prose — but a new lesson emerges: scaffolding additions help the COHORT-MIRROR axis but do NOT defuse SURFACE tells that remain in the R80 underlying prose.

## Pareto

R80 (2/3 LEAN, commit 9ff974e) remains BEST_GAN. v10 reverted to R80 baseline.

## R87 plan

Strategy 8 EXTENDED:
- Keep R86's three additions (Note + footnote + chapter-rename) as base
- Add 3 more scaffolding pieces: glossary appendix, Preface dead-end paragraph (R85 critic recommended), additional chapter-title rename §2 + §4
- Optionally add OCR-artifact note in the footnote so critic 18701894's specific suspicion is addressed
