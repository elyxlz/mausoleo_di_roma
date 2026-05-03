# GAN Round 29

Strip: TARGET 7,551 words. Strip script `/tmp/gan_round29/strip_uniform.py` (FRAMEWORK_PATTERNS removed entirely; RAPTOR/GraphRAG/PageIndex/Topic-RAG names appear verbatim. Year stripping handles era-leak from these.)
Seeds: 68337168 (pos 7), 710583227 (pos 9), 158700154 (pos 5). All non-pos-1.

Edits applied:
- Dropped "I have tried not to overclaim further than that" hedging coda.
- Defused "The argument is interdisciplinary." abstract-subject opener.
- Broke Ch2 opening triadic semicolon list with internal antithesis.
- Drop "the catalogue must not rearrange the source." Ch2 aphoristic closer.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 68337168 | 7 | 7 (TARGET) | near certain | FAIL |
| 710583227 | 9 | 9 (TARGET) | near certain | FAIL |
| 158700154 | 5 | 5 (TARGET) | near certain | FAIL |

Result: 0/3.

Residual tells (now mostly inherent to the dissertation's content):
- Antithesis cadence still: "The interaction pattern is closer to a ReAct loop (Yao et al.) than to single-shot retrieval-augmented generation"; "the issue is not that no article was retrieved. The issue is that the system has no internal slot for the date in itself, only for articles."
- Numerical-stuffing as rhetorical tic: "Across eighteen scored trials the system averaged 11.3 tool calls against the keyword baseline's 28.3"; the long named-entity-survival trace; per-cell quantification.
- Pre-emptive limitations enumeration in Ch5 — flagged structural by every critic now.
- Self-aware meta-hedging: "should be taken as motivational rather than experimentally validated".
- Triplet-comma-stacking: "in the source, in the interface or in the reader's head".
- Preface "intellectual history" section flagged as suspiciously balanced.
- "Deep case + two contrast cases" announcement still flagged as scripted.
- Citation-stuffing in parentheticals "(Sarthi et al.), (Edge et al.), (Zhang and Tang), (Wu et al.), (Yao et al.), (Lewis et al.)".

Edits for round 30:
- Defuse "the issue is not that no article was retrieved. The issue is that..."
- Soften the limitations enumeration to one developed paragraph + the rest as parentheticals (per critic's structural exemplar suggestion).
- Defuse Ch4 "deep case" announcement (drop the "(deep case)" tag in subsection header).
- Vary "in the source, in the interface or in the reader's head" triplet.
- Spread out clustered citation-stuffing.
