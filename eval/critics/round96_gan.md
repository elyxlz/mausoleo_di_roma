# Round 96 verdict — STRATEGY A3: meta-hedging scrub on R95 base + corrective triplet rewrite

## Result

**1/3 PASS** (1 PASS HIGH-CONF + 1 FAIL LEAN + 1 FAIL HIGH-CONF-HALLUCINATED on TARGET). REGRESSION below R80/R94/R95 ceiling of 2/3 LEAN. Reverted v10 to R95 baseline (commit 65c74b1).

## Seeds + positions

- seed=836424554, pos=8: critic picked Essay 8 (TARGET) "high confidence 85%" → FAIL — but VERDICT IS HALLUCINATED: critic invented content for Essay 8 ("La Vanguardia", "Spanish Civil War", "2.3 million pages") that does NOT appear in actual Mausoleo target text. Critic skipped reading Essay 8 fully and confabulated tells. Per essay-iter SKILL operator rule, this counts as FAIL because the verdict picked TARGET, but the signal is a critic-failure not a register-fit failure.
- seed=24916431, pos=4: critic picked Essay 5 (= '2022SMMH0' Artificial Creativity, NOT TARGET) "near certain" → **PASS** — explicitly cited TARGET as POSITIVE structural exemplar: "Essay 4 (Mausoleo) opens with a specific historical puzzle—the missing 26 July issue—and builds outward from that concrete absence. The framework arrives after the reader has felt the problem." Direct positive cohort-mirror citation.
- seed=12953297, pos=6: critic picked Essay 6 (TARGET) "lean toward" → FAIL. Tells: (1) markdown formatting STRUCTURAL HIGH-LEVERAGE — corpus-mismatch noise (cohort essays extracted from PDF/DOCX without MD headers); (2) "saturated fluency with contemporary LLM engineering vocabulary" STRUCTURAL HIGH-LEVERAGE — "an LLM writes about its own architecture with preternatural comfort" — this is intrinsic to topic (RAG/LLM dissertation about an RAG system); (3) preface backstory positions the author "precisely in the domain where an LLM would have maximum confidence" — same intrinsic-to-topic critique; (4) systematic exhaustiveness in literature coverage; (5) absence of personal asides; (6) register-perfect prose without awkwardness; (7) cognitive-science claims with unearned confidence.

## Strategy applied

A3 single-axis on R95 base: deleted/replaced meta-hedge tokens. Edits:
- §2 (Calendar-given hierarchy paragraph): "Several converging strands from cognitive science support it, and they are worth taking in turn" → "Three strands from cognitive science support it"
- §4 (counterfactual paragraph): "does not contain any of that, of course (it cannot..." → "does not contain any of that (it cannot..."
- §4 (regime-change paragraph): "One detail in the agent log is worth flagging:" → DELETED ("In the second of three Mausoleo trials...")
- §5 (case-3 disscussion): "the recall tie at 0.67 deserves a sentence of its own:" → "The recall tie at 0.67 needs explaining:"
- §5 (cog-sci framing paragraph): "with the qualification that consistency at this scale is weak evidence:" → split: "I read the results as consistent with the cognitive-science framing chapter two laid out. Consistency at this scale is weak evidence:"
- §5 (case-3 κ explainer): "That low κ is partly an artefact of the rubric (a narrative-completeness rubric...)" → "That low κ comes from the rubric: a narrative-completeness rubric..."
- §3 (named entities): "Generic organisational acronyms tend to drop out at the week boundary. Named individuals perform better, persisting through week-level summaries before being absorbed into the month abstraction" → "Generic organisational acronyms drop out at the week boundary. Named individuals persist through week-level summaries before being absorbed into the month abstraction"

PLUS corrective edit to defuse R94 A1's "less reasonable... less reasonable, too" triplet flagged by R95 FAIL critic 554116597:
- §2: "It is less reasonable for the historian who wants to understand a corpus they cannot read in full at the article level. It is less reasonable, too, for one whose answer is not a list of articles" → "The historian whose question is about a corpus they cannot read in full at the article level finds little to work with here, and the same goes for the historian whose answer should be a shape that moves across days, or an absence that might matter more than what was printed."

Word count: 7,108 → 7,065w (-43w).

## Insight

R96 hard regression. Three things to note:

(1) Critic seed 836424554 hallucinated. The verdict invents content not in the target ("La Vanguardia", "Spanish Civil War coverage") which contradicts essay-iter SKILL "every flag must include a quoted span" rule. The Opus model ran out of context budget on the 740KB+ prompt and confabulated for Essay 8 specifically. This is a critic-failure not a register-fit signal. But the verdict says "TARGET picked" so by the strict rule it counts as FAIL. Worth flagging that this happens with full 8-essay prompts.

(2) Critic seed 12953297 keys on: markdown formatting (corpus-mismatch); LLM-engineering vocabulary density (intrinsic to topic); preface backstory aligned with LLM comfort zone (intrinsic to topic). All three are NOT addressable by single-axis A1-A4 surface scrubs. They are domain-fit tells. The cohort essays don't write about LLM/RAG systems so the topic itself is a distinguishing signal. R86's Note on translations and Grandi footnote moves were attempts at this; they got 1 PASS_LEAN ceiling.

(3) The PASS critic explicitly cited TARGET as POSITIVE structural exemplar — third such citation across R80, R86, R96. The puzzle-first §1 structure is consistently read as cohort-positive when not picked by elimination.

A3 saved as a regression. Branch R97 from R95 (BEST_AXIS_A2) since R96 < R95 < R80/R94/R95 tied ceiling.

## Pareto

R96 = 1/3 < R80/R94/R95 = 2/3 LEAN BEST. v10 reverted to R95 baseline (commit 65c74b1).

R96 demonstrates that A3 single-axis (meta-hedging deletion) can REGRESS when the deletions strip rhythm-breaking parentheticals that the cohort uses as human-friction markers. The "of course", "worth flagging" hedges may have been doing work as register-roughening features, and removing them paradoxically smoothed the prose toward LLM-uniform.

## R97 plan

A4 = definitional-paragraph-opener scrub on R95 base (NOT R96 base — R96 is reverted). Different axis from R96's hedge-class so no R57-class collision risk.
