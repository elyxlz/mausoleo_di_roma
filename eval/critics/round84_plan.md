# Round 84 plan — Strategy 7: cross-model rewrite via Opus 4.7 with distancing system prompts

## Strategy

R75-R83 exhausted SICO via Haiku 4.5 (R75-R76, R83) and Haiku cross-model (R72-R74, R78). The unexplored option per dispatch: use Opus 4.7 — same model class as the critic — but with a RADICALLY different system prompt that explicitly distances the prose from the critic's expectations of LLM-academic style.

Rationale: Haiku-based rewrites preserve a same-class signature because Haiku and Opus share Claude family register defaults. Opus-with-distancing-system-prompt may produce prose that is mechanically Opus-output but stylistically far enough from default-Opus to confuse the Opus critic.

## Targets (one prompt variant per paragraph, to avoid mass register collapse)

Layered on R80 v10. Three paragraphs touched, each via Opus 4.7 with a different system prompt:

**Target 1: §1 paragraph 4 (Bartlett / cognitive-science block)**
Currently reads as a definitional academic mini-survey. R80 FAIL critic 319113977 named "definitional paragraph openers" as a tell.
System prompt variant A: "You are an undergraduate writing in their first month of using academic prose. Mistakes are acceptable; rhetorical polish is not. Rewrite the paragraph with the same factual content and the same citations in the same order, but in flatter, more declarative prose. Avoid any rhetorical formula. If a sentence currently reads like a textbook gloss, replace it with a less elegant but more direct version. Keep all citations exactly as given."

**Target 2: §1 paragraph 5 (Tolman / Eichenbaum / Whittington block)**
Currently has the sentence "The relevance for an archival interface is direct" — a meta-claim that cohort essays don't carry. Plus parallel-structure cadence.
System prompt variant B: "Rewrite as a humanities undergraduate who has been told repeatedly to avoid academic register tics. Be flatter, less elegant, more declarative. Drop any sentence that summarises what was just said. Drop any 'X for Y' construction that reads as a thesis-summary. Keep all citations exactly. Length within ±15% of source."

**Target 3: §5 paragraph 2 (cog-sci consistency)**
Currently carries "with the qualification that consistency at this scale is weak evidence" — a hedge cohort essays carry less self-consciously. Plus the closing "the same domain-general machinery that handles analogous spatial and conceptual problems, but whether an LLM agent accesses any of that through the same route that biological learners do is a question this experiment does not touch" reads as an LLM-shaped careful-hedge.
System prompt variant C: "Mimic the prose of a working historian who has been asked to add a brief cog-sci framing paragraph and is uncomfortable with the framing. Be slightly grudging. Use shorter sentences. Do not use any thesis-summary or any 'this experiment does not X' meta-formula. Keep all citations exactly."

## Implementation

a. Source v10 = R80 baseline (commit 9ff974e).
b. Extract the three paragraphs.
c. Run Opus 4.7 with three different system prompts (one per paragraph).
d. Splice rewritten paragraphs back into v10.
e. Sanity check: word count within ±150w of 7,124, all citations preserved verbatim.
f. Strip + GAN at 3 fresh non-pos-1 seeds.

## Pareto rule

If R84 ≥ 2/3 PASS (matches R80), promote to v10 (or keep if 2/3 ties). If R84 = 3/3, ship and STOP. If R84 < 2/3, revert to R80, plan R85 with same Strategy 7 on different paragraphs.

## Word count target

R80 = 7,124w. Each rewrite ±15% on ~150w-paragraphs = ±22w. Net within ±70w. Stay under 9,950w cap by huge margin.

## Risk

Opus 4.7 with distancing system prompt is unexplored. May produce prose that reads as undergraduate-bad rather than undergraduate-real. Mitigation: per-paragraph sanity check before splicing; revert any rewrite that reads as broken.
