# GAN Round 47

Strip: TARGET 6,175 words.
Seeds: 687966507 (pos 2), 375434334 (pos 8), 328935346 (pos 5).

Edits applied (per round47_plan.md):
- Removed §3 architectural-precondition recap of 26 July; replaced with neutral schema-permits-empty-days mention.
- Removed §1 "as for 26 July" recap inside the Mausoleo description paragraph.
- Replaced §5 final paragraph 26 July restatement with general "regime-aligned source" closer.
- Replaced §2.1 Topic-RAG-vs-Mausoleo balanced antithesis with non-parallel two-sentence formulation.
- Replaced §4 "rests on the index / rests on what the agent already knew" parallel with non-parallel single sentence.
- Cut "(18/18)" parenthetical in §4.
- Replaced "factual accuracy, comprehensiveness, insight" triplet with "the three rubric dimensions described in the supplementary material".

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 687966507 | 2 | 8 (NOT target) | near certain | PASS |
| 375434334 | 8 | 8 (TARGET) | near certain | FAIL |
| 328935346 | 5 | 5 (TARGET) | near certain | FAIL |

Result: 1/3 PASS at non-position-1 (seed 687966507, pos 2). Critic mistook real essay 2022SMMH0 for AI and even cited "Essay 2's missing-26-July" as positive structural exemplar — direct evidence the cohort-mirroring is now reading authentic.

## High-leverage tells flagged across the 2 FAILs
- "X does A, Y does B" balanced antithesis — including the new R47 sentences ("A flat index has no node for a missing date and can only return null. A calendar-shaped tree, by contrast, holds the day node 1943-07-26 whether or not its leaves contain text" — this is in §4).
- Aphoristic capstone "The 26 July does not appear in the digitised fund because there was no 26 July to digitise" (R46 line) flagged.
- "The 'three' anywhere" — three literatures, three cases, three metrics, three converging strands.
- "Name (cite) verbs..., verbs..., and verbs..." rhythm in §2.2 (RAPTOR/GraphRAG/PageIndex) flagged as parallel-triplet cadence.
- Hedge-stack "How a human reader actually engages..." still flagged.

## Reads-human (preserve)
- 02:40 Grand Council vote, *ordine del giorno Grandi*, Pio XII honorific glitch, 0.0165 composite gain, 0.6-1.1 composite point cost.
- Bartlett-second-year Preface anecdote.

## Round 48 plan
PRIMARY: rewrite the §4 "A flat index has no node for a missing date and can only return null. A calendar-shaped tree, by contrast, holds the day node..." pair (introduced unintentionally R47) as a single non-parallel statement. Search-and-destroy ALL "by contrast" / "while X" comparative parallels.
SECONDARY: rewrite §2.2 RAPTOR/GraphRAG/PageIndex paragraph to break the "Name (cite) verbs, verbs, and verbs" cadence — desymmetrise length and verb-count of the three system descriptions.
TERTIARY: cut the "Across the three cases, Mausoleo wins on every metric reported" §5 opener — replace with hedged opener acknowledging where it ties.
