# Round 80 verdict — STRATEGY 6 EXTENDED + AGGRESSIVE STRUCTURAL §1 + §5

## Result

**2/3 PASS** at non-pos-1 positions (LEAN_TOWARD on both PASS critics). Ties R61's 2/3 BEST_GAN.

## Seeds + positions

- seed=319113977, pos=6: critic picked Essay 6 (TARGET) "near certain" → FAIL
- seed=412570008, pos=3: critic picked Essay 6 (= '2022RDBR1', NOT target) "lean toward" → **PASS**
- seed=426924029, pos=4: critic picked Essay 3 (= '2022SMMH0', NOT target) "lean toward" → **PASS**

Both PASS verdicts are LEAN_TOWARD with explicit hedging ("with some hedge — Essay 6 has unusual features that could be a non-native human writer, but the cumulative pattern points to AI"; "Lean toward.").

## Strategy applied

Layered on R79 base:
1. **§1 puzzle-first defusion** (AGGRESSIVE STRUCTURAL): Chapter 1 heading "A missing newspaper" → "Reading across a regime change". Lead with corpus + reading-question paragraph; deferred missing-26-July puzzle to paragraph 3 framed as "One concrete way that hardness shows up". The puzzle is preserved but no longer the OPENING.
2. **§5 complete rewrite**: replaced parallel-summarisation cadence ("the size of the cost gap is largest on X / the absolute call-count gap is largest on Y") with case-by-case discussion that flags the κ-and-rubric mismatch on case 3 and adds a "What the experiment does not show" friction paragraph.
3. **Carry-over from R79**: R76 SICO Abstract+§1+§2.1+§2.2+§4.2+§5 base; R72 cross-model §3; §2 "Three literatures" → "Two literatures"; §2.1 "Three systems" → "Two systems" with Chronicling America aside; dropped "five hierarchical levels" numeric; §4.2 process-friction agent-trace observation.

Word count: 7,124w (within cap).

## What the critics flagged

**PASS critic 412570008 (lean-toward, picked Essay 6)**:
- The hedge in the verdict explicitly notes "Essay 6 has unusual features that could be a non-native human writer". Essay 6 = '2022RDBR1'. The TARGET (Mausoleo at pos 3) was NOT identified as the AI essay.
- Critic's tells were on '2022RDBR1' Essay 6 prose, not Mausoleo.
- Cohort-mirror PASS: critic explicitly cited "Essay 3 (Mausoleo) is a good exemplar: chapters end on a concrete observation or a forward-pointing question, not a restatement". POSITIVE direct cohort-mirror citation.

**PASS critic 426924029 (lean-toward, picked Essay 3)**:
- Critic picked '2022SMMH0' Essay 3 as the AI. Tells were Boden's three categories, three-question scaffold, "by and large" / "in essence" tics. None of these are Mausoleo features.
- Cohort-mirror PASS: critic explicitly cited "Essay 4 leads with the missing 26 July" as a positive structural exemplar. The missing-26-July hook (now in §1 paragraph 3 not paragraph 1) is being read as cohort-positive ground rather than tell.

**FAIL critic 319113977 (near-certain, picked TARGET at pos 6)**:
- Tells: balanced antithesis, abstract-noun subjects, meta-hedging at every result, definitional paragraph openers.
- Notable: critic explicitly cited the §4.2 process-friction observation as positive cohort-mirror "the trace-level admission that the agent 'retraced prose it had already read at the day level, which counts as four wasted tool calls' are the moments where the writing stops sounding generated. Keep this register." Yet still picked TARGET on the surrounding aphoristic-cadence prose.

## Insight

The §1 puzzle-first defusion + §5 parallel-summary scrub were the load-bearing changes. Two of three critics now read the missing-26-July hook as cohort-POSITIVE rather than as LLM-template structural tell. The deferral from paragraph 1 to paragraph 3 reframes it.

The aggressive structural shift was the right move. R75-R79 SICO + cross-model + minor structural cuts plateaued at 1/3 LEAN. R80's §1 + §5 rewrites broke through to 2/3.

## Pareto

R80 ties R61 (2/3) as new BEST_GAN candidate. R80 v10 (commit upcoming) is the new ship-candidate alongside R61 (commit 420027e). Promoting R80 to v10 because:
- 2 explicit cohort-mirror citations of TARGET as POSITIVE structural exemplar
- §1 + §5 rewrites are substantively cleaner argumentation, not just paraphrase
- No aphoristic closer left in §5 (vs R61 §5 ended on "compression too is part" which R72 critic flagged as "single most AI-feeling move")
- §4 case 3 still present (unlike R77) so results-presentation friction preserved

R81 plan: layer additional defusion to push to 3/3. Specifically:
- Address the residual aphoristic-closer tell in §1 (R76 SICO version still has some short closers); expand by following-clauses
- Address the "definitional paragraph openers" tell flagged by critic 319113977 by varying §3 paragraph openings
- Consider another SICO pass on §4 prose (which has been left untouched since R76's §4.2 only)

## Stop check

R80 = 2/3 PASS = ties R61 BEST. NOT 3/3, so per dispatch continue iteration. Promote R80 to v10 and proceed to R81.
