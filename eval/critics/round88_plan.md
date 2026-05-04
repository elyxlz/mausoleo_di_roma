# Round 88 plan — Strategy 8 base (validated subset) + Strategy 9 asymmetric §4 case weighting

## Strategy

R85 critic 497651923 + R86 critic 572980918 + R87 critic 665845434 all independently recommended asymmetric §4 case weighting. THREE different critics across three different rounds named the same structural fix. R77 attempted 2-case collapse and regressed because it removed structural friction; R88 takes a different angle: KEEP all 3 cases but DEMOTE the two contrast cases to a single short paragraph and EXPAND the missing-26-July case with deeper close-reading.

Plus: KEEP R86 + R87's validated additions (Note, footnote, §3 chapter rename, §2 + §4 chapter renames, glossary appendix), DROP R87's LDA Preface paragraph (flagged by 2 critics).

## Implementation

a. Source v10 = R80 baseline (commit 9ff974e).
b. Apply R86 base (Note on translations + Grandi footnote + §3 rename).
c. Apply R87 additions MINUS LDA Preface (chapter renames §2 + §4, glossary appendix).
d. STRUCTURAL: in §4, demote "Two shorter cases" subsection (now 270w with both cases compressed in one paragraph) to a SHORT paragraph (~120w) summarising both cases. EXPAND "The missing 26 July" subsection by ~150w with extended close-reading drawn from the existing footnote primary-source content (the *ordine del giorno Grandi* prose around the King's proclamation, Badoglio government list, MinCulPop register drop). The expansion grounds the missing-day case's claim about cohort-positive specificity.

The asymmetric §4 design BREAKS the parallel three-case structure flagged across R75-R87 as the dominant STRUCTURAL tell, while preserving the κ=0.14 friction signal from comparative-coverage case (which R77 lost when removed).

## Word count target

R80 = 7,124w. + R86 (~165w) + R87 chapter renames (0w net) + glossary (~280w) - LDA Preface (-150w not added) + missing-26-July expansion (+150w) - two-case compression (-150w) = ~7,569w. Within cap.

## Pareto rule

If R88 ≥ 2/3, promote v10. If R88 = 3/3, ship and STOP. If R88 < 2/3, revert R80, plan R89 = R88 base + Strategy 9 §2 single-chapter reshape OR drop the asymmetric §4 if it backfires.

## Risk

§4 case demotion was explicitly tried in R77 with hard regression. R88's mitigation: don't DELETE case 3, just compress its prose; preserve the table row + the κ=0.14 friction signal; expand the missing-day case rather than cut others. R77 cut a case entirely; R88 weights asymmetrically.
