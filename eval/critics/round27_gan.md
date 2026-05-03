# GAN Round 27

Strip: TARGET 7,578 words. Strip script `/tmp/gan_round27/strip_uniform.py` (FRAMEWORK_PATTERNS now use descriptive names: "chunk-clustering tree method" / "graph-community summarisation method" / "table-of-contents-based method", removing the placeholder tell from rounds 24-26).
Seeds: 686762964 (pos 3), 697527100 (pos 9), 357946735 (pos 8). All non-pos-1.

Edits applied:
- Defused "The hierarchy in Mausoleo is not induced. It is the publication calendar..." → "Mausoleo's hierarchy comes from elsewhere. The publication calendar, which the printers already followed, supplies it for free."
- Defused "The architecture is what does the work here" → "The architectural commitment matters here."
- Dropped "A wider point underwrites all of this. An archive is part of the system the historian thinks with..." closing aphorism. Replaced with "Whether the cognitive framing turns out to do as much explanatory work as the technical results need it to do is, finally, what the human-subjects study above is meant to test."
- Rewrote preface third paragraph yet again (removed any narrative arc cadence).

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 686762964 | 3 | 3 (TARGET) | near certain | FAIL |
| 697527100 | 9 | 9 (TARGET) | near certain | FAIL |
| 357946735 | 8 | 8 (TARGET) | near certain | FAIL |

Result: 0/3.

Residual tells (now mostly STRUCTURAL):
- "The way I worked round the gap was to read the 25th and the 27th instead and infer backwards. That worked, but it left me thinking the interface had treated a question with a real answer as if it had no answer at all." — preface compressed setup-pivot-summation rhythm.
- "Tree traversal supplies provenance and chronological position; semantic search is the escape hatch when chronology is the wrong axis. The application programming interface is minimal and stateless; reasoning is pushed into the agent." — chapter 3 closing antithesis pair.
- Pre-emptive hedging: "That story should not be told without acknowledging the costs and the limits." / "I would not push it further than that here."
- "running from paragraph at the bottom up through article, day, week and month" — still a sequential triplet.
- Bare "(specific articles at one extreme and monthly aggregates at the other, with narrative episodes across days in between)" — flagged as "X at one extreme... Y at the other... Z in between" formula.
- Section-closing summative gestures: "Whether the framing scales to a working historian's reading practice is not yet shown."
- Three critics now strongly recommending one structural move: collapse the parallel three-case symmetry to one deep case with shorter contrasts. The current Setup / Case 1 / Case 2 / Case 3 / Aggregate parallel structure is itself reading as LLM scaffolding.

Edits for round 28:
- Defuse the preface "That worked, but it left me thinking..." sentence.
- Defuse the Ch3 "Tree traversal supplies provenance...; semantic search is the escape hatch..." closing antithesis.
- Drop "That story should not be told without acknowledging the costs and the limits."
- Rewrite "(specific articles at one extreme... in between)" formula.
- Drop final "Whether the framing scales..." section-closer.
- STRUCTURAL: rebalance Ch4 — make missing-26-July visibly longer than the other two cases and remove the parallel "Setup / Case 1 / Case 2 / Case 3 / Aggregate" header structure.
