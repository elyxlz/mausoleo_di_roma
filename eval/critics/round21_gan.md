# GAN Round 21

Strip: TARGET 7,749 words. Strip script `/tmp/gan_round21/strip_uniform.py` (FRAMEWORK_PATTERNS shortened so RAPTOR/GraphRAG/PageIndex no longer expand into a parallel triplet of method-names).
Seeds: 127555292 (pos 4), 346060391 (pos 2), 282997004 (pos 3). All non-pos-1.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 127555292 | 4 | 4 (TARGET) | near certain | FAIL |
| 346060391 | 2 | 2 (TARGET) | lean toward | FAIL |
| 282997004 | 3 | 2 (NOT TARGET) | lean toward | PASS |

Result: 1/3 — first non-position-1 PASS at the new constraint.

Residual tells (FAIL critics):
- Triadic "X-task: the answer is Y" parallel in Chapter 4 setup ("an episodic-retrieval task in the sense of chapter two: the answer is bound to a specific date. The second is the regime change of 25 to 27 July, a narrative-integration task: the answer is the trajectory across episodes. The third is...").
- "not a metaphor on cognition" appears twice (chapter 2 and chapter 5).
- Chapter 5 limitations litany — six parallel limitations in identical cadence.
- Aphoristic closers: "touched-articles is the wrong instrument when the answer is an absent issue", "Once the metric matches the question, the structural prediction holds".
- "Mausoleo does not induce. The hierarchy here is the publication calendar..." — negation-correction cadence.
- Self-narration of asymmetric weighting: "The first case is reported at length because... the second and third are reported more briefly".
- Bookend symmetry chapter 1 ↔ chapter 6 (puzzle stated, puzzle resolved).

Structural rewrite suggestions provided by seed-346060391 critic:
1. Break the chapter 1 ↔ chapter 6 bookend symmetry; end on the human-subjects gap rather than returning to the absent day.
2. Stop self-narrating asymmetric weighting.
3. Scrub aphoristic closers paragraph by paragraph.
4. Break up the chapter 5 limitations litany; vary sentence length, embed two limitations in earlier discussion.

Edits for round 22: apply structural moves 1-4.
