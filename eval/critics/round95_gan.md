# Round 95 verdict — STRATEGY A2: abstract-noun-subject scrub on R94 base

## Result

**2/3 PASS LEAN** (1 LEAN PASS + 1 LEAN PASS + 1 NEAR_CERTAIN FAIL on TARGET). Ties R80 + R94 at 2/3 LEAN BEST_GAN ceiling.

## Seeds + positions

- seed=554116597, pos=3: critic picked Essay 3 (TARGET) "near certain" → FAIL
- seed=947708644, pos=2: critic picked Essay 3 (= '2022SMMH0' Artificial Creativity, NOT TARGET) "lean toward" → **PASS**
- seed=690307975, pos=7: critic picked Essay 2 (= '2022SMMH0' Artificial Creativity, NOT TARGET) "lean toward" → **PASS**

## Strategy applied

A2 single-axis on R94 base: replaced abstract-noun grammatical subjects with concrete agents (we / I / Mausoleo / chapter four / the agent / Murugaraj et al.). Edits:

- Abstract: "A flat ranked-article interface asks the researcher" → "A flat ranked-article interface forces the researcher"
- Abstract: "The case studies in chapter four ask whether" → "Chapter four runs three case studies on whether"
- §1: "From the digital-archive side, that question is hard to put to the existing systems" → "I could not put that question to the existing systems"
- §1: §1 ¶2 entire passive-quantifier reframe to first-person ("I would have had to read...")
- §2: "The dissertation asks a different sort of question" → "I am asking a different sort of question"
- §2: "A temporal index running at multiple resolutions is therefore working in the same structural form" → "A temporal index that runs at multiple resolutions therefore works"
- §2: "The closest prior work on retrieval-augmented generation over historical newspapers is Murugaraj et al." → "Murugaraj et al. (2025) is the closest prior work"
- §3: "The architecture reflects Ketelaar's (2001) treatment" → "I follow Ketelaar's (2001) treatment"
- §4: "The interface treats a question that has an answer as though it had none" → "The keyword baseline treats a question..."
- §4: "The compiled answers therefore differ" → "The two compiled answers therefore differ"
- §4: "The failure mode here is at the level of the data model itself" → "The failure here sits at the data model itself"
- §5: "The results sit consistent with the cognitive-science framing" → "I read the results as consistent with the cognitive-science framing"
- §5: "the experiment is not powered to discriminate" → "I do not have the power in this experiment to discriminate"
- §5: "is a question this experiment does not touch" → "is a question I cannot put to the cases as run"
- §5: "The spot-check in chapter three reports forty-eight of fifty named entities recovered" → "I report forty-eight of fifty named entities recovered in the chapter-three spot-check"
- §5: "What the experiment does not show:" → "What I have not shown:"

Word count: 7,100 → 7,108w (+8w). No antithesis re-introduction (kept R94's A1 edits intact).

## What the critics flagged

**PASS critic 947708644 (lean, picked Essay 3 = Artificial Creativity at pos 2)**:
- 8 tells on Artificial Creativity essay: triple-question framing, vague disciplinary listing without specific course names, "twofold" balanced construction, "not only X but also" parallel, "However, often with innovation comes scrutiny", section architecture parallelism, taxonomic tables, vague preface temporal anchoring.
- TARGET (Mausoleo at pos 2) was NOT picked.

**PASS critic 690307975 (lean, picked Essay 2 = Artificial Creativity at pos 7)**:
- Same essay (Artificial Creativity), 6 tells: triple rhetorical questions, hedging chain ("might be better understood as"), balanced antithesis pairs ("Not X, but Y"), register-smoothing vocabulary, explicit roadmap meta-commentary, em-dash/colon rhythm.
- TARGET (Mausoleo at pos 7) NOT picked. Critic explicitly cited **"Mausoleo's first-person hedging" as reading HUMAN** in summary — direct positive cohort-mirror citation of A2's first-person edits! Strongest single positive signal of A2.

**FAIL critic 554116597 (near certain, picked TARGET at pos 3)**:
- Tells: (1) NEW "less reasonable... less reasonable, too" triplet I introduced in R94's A1 split — STRUCTURAL HIGH-LEVERAGE — A1 pure-deletion of "but Y" left behind a triplet that is the same-class tell; R57 lesson at single-axis scale; (2) "the cognitive system already runs multi-resolution hierarchical structure for tasks of an analogous form" SURFACE register tic; (3) "A flat keyword search offloads that holding-work onto the user in ways that slow down recall and increase the risk" SURFACE balanced verb pair; (4) "What I have not shown:" pre-emptive limitations hedging — STRUCTURAL HIGH-LEVERAGE — note this is the A2-rewritten form of "What the experiment does not show:" — so A2 didn't help on this axis; (5) "second-order question" SURFACE register tic; (6) STRUCTURAL "no candidature number, no personal preface, no acknowledgments section" — corpus-stripping artefact (target stripped in build_round.py drops the BASC0024 module-code line + the preface SHOULD be there; let me check); (7) "I read the results as consistent with the cognitive-science framing chapter two laid out, with the qualification that consistency at this scale is weak evidence" SURFACE epistemic hedge stacking — A2-rewritten form, didn't help; (8) "ask whether the prediction implied by these three strands of cognitive science shows up in the metrics" SURFACE construction with abstract subjects.

## Insight

A2 ties R80 + R94 at 2/3 LEAN. The PASS critics moved to picking the cohort essay decisively (one explicitly praised first-person hedging). The FAIL critic locked onto the NEW "less reasonable" triplet I introduced in R94's A1 split — confirming R57 lesson at single-axis scale: pure-deletion exposes parallel-construction tells in the same neighbourhood.

Two key insights for R96:
1. The "What I have not shown:" → "What I have not shown:" rewrite did NOT defuse the pre-emptive-limitations tell. The structural shape of that paragraph survives any subject swap. R96 (A3 meta-hedging) should target the hedge-stacking inside that paragraph.
2. The "less reasonable... less reasonable, too" triplet must be REWRITTEN in R96 base (not A2's, but the earlier A1 split). Adjustment is preserved as a side-edit before the A3 axis-only run.

## Pareto

R95 = 2/3 LEAN = ties R80, R94 BEST_GAN. Save A2 as BEST_AXIS_A2. v10 stays as R95 for R96 branching (no revert).

## R96 plan

A3 = meta-hedging scrub on R95 base + ONE corrective edit to defuse R94 A1's "less reasonable" triplet (single-class side-edit since that triplet is the same antithesis class A1 was supposed to scrub).
