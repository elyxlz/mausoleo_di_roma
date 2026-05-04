# Round 80 plan — AGGRESSIVE STRUCTURAL §1 puzzle-first defusion

## Strategy

R75-R79 critics consistently flagged §1's puzzle-first opening as an LLM template tell. R80 defuses it by reordering §1: lead with corpus + cognitive-science framing (corpus characterisation drawn from R76 SICO §2.4 and §1 paragraph 3), then introduce the missing 26 July as a worked example in §1 paragraph 3 or 4, NOT as the opening hook.

Plus complete-rewrite of §5 to break parallel-summarisation cadence flagged by R79 critic 987957044.

Layered on R79 base.

## §1 reordering plan

Current R79 §1 structure (paragraph by paragraph):
1. "A query for *Il Messaggero* on the date 26 July 1943..." [puzzle hook]
2. "These archives index at the article level..." [implication for historians]
3. "There is a body of cognitive-science work..." [Bartlett intro]
4. "A separate but converging line of research..." [Tolman/Eichenbaum]
5. "This dissertation builds and tests an interface..." [system intro]
6. "A recent NLP literature on hierarchical retrieval..." [closing context]

Proposed R80 §1 structure (rotated):
1. NEW OPENER: "*Il Messaggero* between 1 and 31 July 1943 covered the war on the eastern and African fronts in parallel with the domestic crisis that culminated in the Grand Council vote, the King's intervention, and the formation of the Badoglio government on 25 July 1943. This dissertation works with the digitised fund of those thirty issues. The reading question that motivated the system this dissertation builds was about the editorial-register shift across the deposition: how did the front-page rhetoric move between the *MinCulPop*-aligned register of mid-July and the new-government register of late-July?" [corpus + reading question first]
2. "From the digital-archive side, that question is hard to put to existing systems..." [puzzle re-cast as access-template problem, no longer puzzle-first]
3. Move the original puzzle-hook into paragraph 3: "One concrete way that hardness shows up: a query for *Il Messaggero* on the date 26 July 1943, addressed to any of the major digitised newspaper archives that hold the paper, returns an empty result page..." [the original puzzle, now framed as "one concrete way"]
4. Cognitive-science context (kept from R79)
5. Tolman/Eichenbaum context (kept from R79)
6. System introduction (kept from R79)
7. NLP literature context (kept from R79)

Net effect: the missing-26-July hook is no longer the OPENING. The corpus and the reading question come first.

## §5 complete rewrite

Current R79 §5 has 4 paragraphs with parallel-summarisation cadence ("the size of the cost gap is largest on X / the absolute call-count gap is largest on Y"). Rewrite as:

Para 1: Honest acknowledgment of what the case studies do and do not show — "The two cases (the regime-change reconstruction and the per-week war-domestic balance) demonstrate that the calendar-shaped index reduces tool-call cost and improves judge quality on questions that take a temporal-aggregate or temporal-comparison shape. The missing-26-July case is structurally different..."

Para 2: cog-sci consistency note (kept)

Para 3: "What the system does NOT show" paragraph — limitations (kept short, friction-signal style)

Para 4: closing on Murialdi-style historiographical concern (kept)

Drop the parallel-summarisation cadence entirely; recast as natural-paragraph discussion.

## Pareto rule

If R80 ≥ 2/3, promote to new BEST_GAN. If R80 < R61, revert.

## Word count target

R79 ~7,000w + §1 reordering (~+150w for corpus opener) + §5 rewrite (~−50w) = ~7,100w. Within cap.

## Risk

§1 reordering is a substantial structural intervention. The original puzzle-first opening has been consistently cited as a structural tell BUT critic R47-R49 cited the missing-26-July signature as POSITIVE cohort-mirror. Defusing the puzzle-first opening risks losing the cohort-mirror signal. Mitigation: the puzzle is not REMOVED, it is moved to paragraph 3.

§5 rewrite is high-risk because §5 is short (~375w) and any rewrite that introduces NEW tells is a regression vector.

## Implementation

a. Start from R79 draft: /tmp/gan_round79/v10_r79.md.
b. Apply §1 reorder via Edit tool (large rewrite of §1).
c. Apply §5 rewrite via Edit tool.
d. Strip + GAN.
