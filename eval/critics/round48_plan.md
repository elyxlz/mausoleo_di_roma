# Round 48 plan

## 1. Prior-round (R47) tells, verbatim

SURFACE
- Seed 375434334: "balanced antithesis as a structural reflex" — *"A flat index has no node for a missing date and can only return null. A calendar-shaped tree, by contrast, holds the day node 1943-07-26 whether or not its leaves contain text"*; *"In Mausoleo's case the answer is grounded in the index, in the baseline's it leans on the agent's training-corpus knowledge"* (the new R47 sentence) — STILL parallel.
- Seed 328935346: "balanced antithesis with 'where' / 'while' parallelism" — *"The prior systems above apply hierarchical retrieval either to a single document's section structure or to a clustering induced from chunk embeddings, while Mausoleo applies the same paradigm to an archival corpus whose hierarchy is given by chronology rather than induced from the data."*
- Seed 328935346: "Name (cite) verbs..., verbs..., and verbs..." rhythm in §2.2 RAPTOR/GraphRAG/PageIndex.
- Seed 375434334: "Aphoristic capstone sentences ending sections" — *"For a regime-aligned source, an editorial silence at a moment of regime change is itself part of the historical record, and a catalogue covering such a source needs to make that silence addressable."* (the new R47 §5 closer); *"The 26 July does not appear in the digitised fund because there was no 26 July to digitise."*
- Seed 375434334: "Suspiciously clean three-part scaffolding repeated at every level" — three literatures, three cases, three metrics, three converging strands.

STRUCTURAL
- Seed 375434334: triple-scaffolding tic.
- Seed 328935346: opens with the puzzle then "immediately collapses back into system-pitch" within two paragraphs.
- Seed 328935346: pre-emptive limitations folded into prose.

## 2. Pattern across last 3-5 rounds (R44-R47)
R45 PASS, R46 regress, R47 PASS. The PASSes share: structural change to recap distribution. R46 failed because it recapped 26 July at every chapter. R47's recap removal worked at pos 2. The new R47 closing sentence ("an editorial silence at a moment of regime change is itself part of the historical record") is itself an aphoristic capstone, but only flagged at one critic. The dominant remaining tell is RESIDUAL parallel antithesis at §2 and §4 — and the §2.2 RAPTOR/GraphRAG/PageIndex parallel triplet I have not touched in 47 rounds.

## 3. Highest-leverage move (R48)
**Rewrite §2.2 RAPTOR/GraphRAG/PageIndex paragraph to break the "Name (cite) verbs, verbs, and verbs" symmetric-parallel cadence.** This has been a stable tell for many rounds. Specifically: cut RAPTOR description to one short sentence; expand GraphRAG description with one substantive caveat; collapse PageIndex into an aside in the GraphRAG paragraph rather than a co-equal third entry. The "common move across these systems is to give the retriever something more than a flat list to work with" closer also goes.

## 4. Secondary moves
- Rewrite §4 "A flat index has no node for a missing date and can only return null. A calendar-shaped tree, by contrast, holds the day node `1943-07-26` whether or not its leaves contain text" — collapse to one sentence without "by contrast".
- Rewrite §2.2 closer "What unites these systems is the access template" / "the common move across these systems is..." — single brief observation.
- Cut §5 opener "Across the three cases, Mausoleo wins on every metric reported" — replace with hedged "On all three cases the Mausoleo configuration produced lower call-counts and higher judge means; recall ties on the missing-day case, where the metric is poorly suited."

## 5. Predicted downstream effects
The §2.2 desymmetrise risks cutting Edge et al. (2024) substance; will keep the citation. Replacing "wins on every metric" with hedged opener risks adding new hedge tell — will keep the hedge tight to one clause.

## 6. Fallback (R49)
If R48 flat: revert §2.2 to R47 and instead aggressively cut §3.1 lineage triplet ("space, time and conceptual relation" — appears 3x).
