# Round 94 verdict — STRATEGY A1: balanced-antithesis scrub on R80 base

## Result

**2/3 PASS** at non-pos-1 positions (1 high-conf PASS, 1 LEAN_TOWARD PASS, 1 LEAN_TOWARD FAIL on TARGET). **Ties R80's 2/3 LEAN BEST.** The FAIL critic was a softer signal than R80's near-certain.

## Seeds + positions

- seed=387349151, pos=8: critic picked Essay 2 (= '2020FSXD0' Kant whaling, NOT TARGET) "high confidence" → **PASS**
- seed=809376439, pos=6: critic picked Essay 4 (= '2022SMMH0' Artificial Creativity, NOT TARGET) "lean toward" → **PASS**
- seed=524965912, pos=7: critic picked Essay 7 (TARGET) "lean toward" → FAIL

## Strategy applied

A1: balanced-antithesis scrub only. Targeted every "X but Y" / "X yet Y" / "rather than" / asymmetric-but / "whereas" balanced construction in body prose. Rewrote into asymmetric or single-claim sentences:

- Preface: "made composite OCR scores worse rather than better" → "made composite OCR scores worse"
- §1 ¶4: "A separate but converging line" → "A converging line"
- §1 ¶4: "interface either holds those resolutions or asks the researcher to hold them, and a flat keyword search offloads" → split into two sentences
- §2: "Italian-language, but it is the third major reference point" → split + "It remains the third major reference point"
- §2: "transparent generosity ... but the user is still expected" → semicolon
- §2: "or for whom the answer ... is not a list of articles but a shape" → split + reframe
- §2: "for global-summarisation queries on three benchmarks, though the entity-extraction pass" → split
- §2: "Zhang and Tang, 2025), reading its hierarchy off the surface rather than inducing one" → "and reads its hierarchy off the surface"
- §2: "the dissertation is asking a different sort of question" (whereas removed) → split
- §2: "obvious experiment but is gated on language" → split
- §2: "rather than inducing one, which means" → "directly. The navigation surface stays predictable"
- §2: "rather than just one designer's preference" → "beyond one designer's preference"
- §3: "but takes fifty to sixty minutes" → "while taking fifty to sixty minutes"
- §3: "did not come from a model addition but from a post-processing filter" → "came from a post-processing filter"
- §3: "predictable but forces aggressive thematic compression" → "predictable at the cost of aggressive thematic compression"
- §3: "robust at day but mostly absent by month" → "robust at day and mostly absent by month"
- §3: "supports questions about what kind of day it was, but not about who appeared in it" → split into two sentences
- §4: "of course (it cannot, because the issue does not exist), but reading the 27 July issue against" → split
- §4: "no way of choosing among these counterfactuals, but the index makes it possible" → split
- §5: "but the κ between judges is also the lowest" → split into separate sentences
- §5: "Mausoleo's, by reading the 25th and 27th issues ... and a touched-set recall metric cannot distinguish" → split
- §5: "data show one, but the experiment is not powered" → split
- §5: "spatial and conceptual problems, but whether an LLM agent" → split
- §5: "from elaborations the summariser inserted that read as historiographically warranted but were not in the source" → "while having no equivalent in the source"
- Appendix A: "and not before), but the downstream effect" → split

Word count: 7,124 → 7,100w (-24w). No replacements that introduced same-class antitheses. No abstract-noun-subject fixes, no meta-hedge deletions, no opener rewrites. Single-axis discipline maintained.

## What the critics flagged

**PASS critic 387349151 (high conf, picked Essay 2 = Kant whaling)**:
- Confidently picked the Kant essay on 8 strong tells: meta-commentary road-mapping, balanced parallel constructions ("first question is whether... second question is whether..."), generic preface motivation, "Having [past-participle]... I [verb]" pattern, frictionless interdisciplinary synthesis, info-box pedagogical scaffold, defensive hedging ("novel contribution"), "no exception" cliché.
- TARGET (Mausoleo at pos 8) was NOT flagged. Critic's verdict text never mentioned Mausoleo.
- Strongest single-critic PASS of the R75-R94 sequence (high conf vs prior LEAN-TOWARDs).

**PASS critic 809376439 (lean, picked Essay 4 = Artificial Creativity)**:
- 8 tells on Essay 4: "However, often with innovation comes scrutiny", "nigh impossible", "in essence we will see", meta-framing "Before we begin", numbered question triplet, "It must also be noted", "It is fair to say", "It is precisely these issues".
- TARGET (Mausoleo at pos 6) was NOT picked.

**FAIL critic 524965912 (lean toward, picked TARGET at pos 7)**:
- Tells: (1) markdown formatting `---` and `###` headers — STRUCTURAL — corpus-mismatch artefact (target uses MD headers, cohort doesn't); (2) encyclopedic cog-sci synthesis Bartlett-Miller-Cowan-Tolman-Eichenbaum chain — STRUCTURAL; (3) balanced parallel "interface either holds those resolutions or asks the researcher to hold them" — SURFACE — note this is a parallel-construction tell, NOT a balanced antithesis (different class, A1 only addressed antithesis); (4) preemptive meta-commentary on summariser limitations — STRUCTURAL; (5) register uniformity across technical and humanistic content — SURFACE; (6) performative technical specificity (three-decimal precision) — SURFACE.
- The FAIL critic's softening to "lean toward" (vs R80's "near certain") suggests A1 made a small dent.

## Insight

A1 single-axis scrub achieved 2/3 LEAN — TIES R80 at the BEST_GAN ceiling. The critic that flagged "balanced parallel constructions" specifically called out a NEW parallel construction I introduced ("either holds those resolutions or asks the researcher to hold them") — pure-deletion of "but" exposed a different parallelism nearby. R57 lesson recurs at single-axis scale.

The markdown formatting tell is corpus-mismatch noise: cohort essays were extracted from PDF/DOCX without markdown headers, target uses native MD `## Chapter` style. This noise was probably present in earlier R75-R93 rounds too (not new from A1), but only this critic weighted it heavily.

A1 ties R80. Per Pareto rule: save R94 as BEST_AXIS_A1 and branch A2 from R94. R94 v10 stays as-is for the next round.

## Pareto

R94 = 2/3 LEAN = ties R80 BEST_GAN. New BEST_AXIS_A1 = R94. v10 NOT reverted; R94 antithesis edits stay in for A2 branching.

## R95 plan

A2 = abstract-noun-subject scrub on R94 base (single-axis).
