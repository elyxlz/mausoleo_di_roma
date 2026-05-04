# Round 85 plan — Strategy 7 EXTENDED + R84-flagged refrain deletions

## Strategy

R84 confirmed Strategy 7 at three-paragraph scope is insufficient. R85 extends Strategy 7 to FIVE paragraphs in dense-tell sections (Abstract para 1, §1 para 2, §4.1 closer, §4 final aggregate paragraph, §5 para 4) PLUS three deletion-only edits addressing R84 critics' convergent recipe.

The R84 critics gave a precise 7-item recipe. R85 addresses items 1, 2, 4, 5, 6:
1. Break "X. Y." semicolon antithesis → addressed by 5-paragraph cross-model rewrite (each prompt explicitly forbids semicolon-balanced clauses)
2. Roughen chapter endings → addressed by Opus rewrite of §4 final + §5 para 4 with explicit "do not write a closing sentence that summarises" instruction
4. "Calendar-shaped tree" refrain (5+ instances) → DELETE: reduce to 2 instances (one in Abstract introducing the term, one in §1 system intro)
5. Mausoleo italics → DELETE: drop italics on first 3 mentions
6. Citation-name-dropping cadence → addressed via §1 para 4 (R84 carryover but rerun with stronger prompt for citation engagement)

Item 3 (mix numeric registers) and item 7 (three-case §4 symmetry) are deferred — item 3 too granular for one round, item 7 was tried in R77 with hard regression.

## Targets (Strategy 7 cross-model)

T1: Abstract paragraph 1 (175w) — drop "handles X and breaks down for Y" antithesis, drop puzzle-first cadence
T2: §1 paragraph 2 (78w) — drop "Article-level keyword search returns lists of articles, not a register-trajectory or a per-week shape" antithesis triplet
T3: §4.1 paragraph 5 ("Mausoleo can ground...", 110w) — drop "in Mausoleo's case the answer is grounded in the index, in the baseline's it leans on" balanced final
T4: §4 final aggregate paragraph (75w) — drop "the regime-change case cleared in roughly twelve Mausoleo tool calls against a baseline that saturated its thirty-call budget every trial" + chiastic ending
T5: §5 paragraph 4 ("What the experiment does not show", 55w) — drop "None of these are within the dissertation's scope and none of them can be inferred from the cases as run" definitional closer

Each gets a different distancing system prompt (rotate SYS_A, SYS_B, SYS_C, plus two new variants SYS_D, SYS_E for diversity).

## Deletion-only edits (after Opus rewrites splice)

D1: Reduce "calendar-shaped tree" instances. Inventory in current v10:
  - Abstract para 1 ("calendar-shaped tree of recursively summarised nodes")
  - Abstract para 2 ("calendar-shaped index")
  - §1 para 6 ("calendar-shaped tree")
  - §1 para 7 ("calendar contains a slot...")
  - §3 ("calendar-shaped tree")
  - Possibly elsewhere
  Target: keep Abstract introduction + §3 system-intro mention. Replace 3+ other instances with "the index" or "the tree" (already established term).

D2: Drop italics on Mausoleo. First 3 italicised mentions: change `*Mausoleo*` to `Mausoleo`. Keep title-page italics.

D3: Verify abstract para 2 closer "a slot for documented silence that a flat article index cannot provide" — this was R76 SICO output, has "X cannot Y" tell. Replace with declarative.

## Implementation

a. Source v10 = R80 baseline (commit 9ff974e).
b. Run Opus 4.7 cross-model on T1-T5 (~20 min cumulative).
c. Splice rewrites back, sanity check.
d. Apply D1-D3 deletions.
e. Strip + GAN at 3 fresh non-pos-1 seeds.

## Pareto rule

If R85 ≥ 2/3 PASS (matches R80), promote to v10. If R85 = 3/3, ship and STOP. If R85 < 2/3, revert to R80, plan R86.

## Word count target

R80 = 7,124w. Five rewrites at ±15% on ~493w-total = ±74w. Deletions D1+D3 = -50w. Net ~7,150w. Within cap.

## Risk

Five-paragraph scope + three structural deletions is the largest single round in this session. Risk of cumulative register-collapse if Opus distancing prompts produce same-register output (R57 lesson). Mitigation: each Opus prompt has explicitly different voice.
