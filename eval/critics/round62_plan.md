# Round 62 plan

## 1. Prior-round (R61) — BREAKTHROUGH 2/3

R61 hit 2/3 PASS at non-pos-1, the first 2/3 in 60+ rounds. NEW BEST_GAN. Two PASS critics picked DIFFERENT real essays; both cited Mausoleo (TARGET) positively as cohort exemplar.

The remaining FAIL (seed 863684421 pos 8 near certain) flagged:
- Opening with system-reveal rather than puzzle (structural Mausoleo signature, not changing)
- Balanced antithesis (saturating; surface)
- Aphoristic closers — *"At month level the summariser had compressed the regime-change to *l'arresto di Mussolini (25 luglio)*, and that compression too is part of what the index records about July 1943"* (R54 closer, split-flagged across critics)
- Triplet "paragraph in article in issue in day in week in month" (Ch1 thesis sentence + §2.2 closer)
- "the X" abstract-noun phrasing
- Italian summary block (deeply integrated, not changing)
- Numeric specificity
- Pre-emptive limitation hedging in §4 (Impresso head-to-head note)

## 2. Highest-leverage move (R62)

R62 should target tells that BOTH the FAIL critic and earlier FAIL critics flagged, while preserving the cohort-mirror signature that produced R60 + R61 PASSes.

PRIMARY: **Defuse the parallel triplet "paragraph in article in issue in day in week in month"** by COLLAPSING (deletion-by-shortening) rather than rewriting. R57 attempted full rewrite which introduced same-class tell. R62 collapses to a flatter form:

Ch1 thesis (line 33): "stores the *Il Messaggero* July 1943 corpus as a calendar-shaped tree of recursively summarised nodes at five hierarchical levels, with the leaf level holding paragraphs of source text and successively higher levels collecting articles into days, days into weeks and weeks into a single month root" -> "stores the *Il Messaggero* July 1943 corpus as a calendar-shaped tree of recursively summarised nodes, with paragraphs at the leaf level and the full month at the root"

§2.2 closer (line 58): "Daily newspapers carry a temporal hierarchy in their production schedule (paragraph in article in issue in day in week in month), and the index inherits that structure rather than inducing one." -> "Daily newspapers carry a temporal hierarchy in their production schedule, and the index inherits that structure rather than inducing one." (delete the parenthetical entirely.)

SECONDARY: **Defuse the §4 chiastic closer "in Mausoleo's case the answer is grounded in the index, in the baseline's it leans on the agent's training-corpus knowledge of the regime change"** — this canonical chiasmus has been flagged across many rounds. Reshape to a non-chiastic form: "Mausoleo's compiled answer comes from the index; the baseline's relies on the agent's prior knowledge of the regime change."

EXCLUDE: do NOT touch Preface, Italian block, OCR section, abstract opening, Ch5 closer (R54 closer is split-flagged but R55 + R60 PASSes saw it), §2.3.

## 3. Predicted downstream effects

R62 builds on R61 by removing two more high-leverage tells flagged across multiple rounds. The collapsed form of the triplet eliminates the rhythmic noun-stacking entirely (no replacement tell). The chiastic closer is broken into a flatter parallel.

If R62 lands 3/3, MISSION COMPLETE.

## 4. Fallback (R63)

If R62 regresses: revert to R61 (commit 420027e), try only the chiastic closer defusion alone.

If R62 ties at 2/3: continue with another pure-deletion target (the §4 Impresso pre-emptive hedge).
