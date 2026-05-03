# Phase 3 Round 2 — Rubric Critic Verdict

**Target draft**: `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v2.md`
**Measured main-body word count**: 9,894 (within the 9,900 buffer; 106w under the 10,000 hard cap)
**Target band**: high-1st on cats 1+4, mid-1st on cats 2+3.
**Marker stance**: anonymous, BASC0024 final dissertation rubric (4 cats), with three additional dimensions per the rubric_prompt.md template (stance clarity, imperative robustness, engagement specificity).

---

## CATEGORY 1: Framing of the research question/purpose in an interdisciplinary light

Rubric tier descriptor for 1st: "Research question/project framed clearly and comprehensively to reveal motivation for interdisciplinary approach and outlines how it will be tackled." The opening question of §1 ("How does a historian read a month of a fascist-era newspaper across the rupture of 25 to 27 July 1943?") still lands as a textbook-perfect interdisciplinary frame: a historiographical question whose answer requires engineering. The two-task-type carve-up (aggregate questions, missing-data questions) names the gap concretely. Case 1 is named in §1 as folding three disciplines into a single object ("a CS retrieval problem, an archival-science question of the provenance of absence, and a historical event in a single object"); the same sentence is restated in §6.2 and §7.1 as structural reinforcement. The Preface now explicitly names the discipline pair under Cat 2 rationale and acknowledges Dr Yi Gong as supervisor. The trim has tightened §1 from 1,020w to 893w without losing the framing density. Cleanly in 1st territory; the question itself remains the strongest cat-1 evidence in the dissertation.

[RESULT] 4

## CATEGORY 2: Disciplinary grounding

Rubric 1st descriptor: "Excellent awareness of epistemological and methodological stances of two (or more) disciplines in relation to the subject matter. Insightful detail and excellent grasp of more general points." §2 is now lighter (1,401w vs v1's 1,550w) but methodologically tighter. The §2.3 rewrite added a methodological-stance sentence on Italian-press source-criticism: "Source-criticism in this tradition is not a neutral reading but a methodological commitment to read the regime press as an artefact of the regime's information apparatus: which directives shaped the day's editorial policy, and what the implicit reader was expected to infer." This is the kind of methodological-stance specificity that v1 lacked. The Cook (2013) paraphrase was hedged in §2.2 ("the trajectory Cook (2013) traces from juridical-evidentiary custody towards active mediation (compressing his four-paradigm schema)") which is more honest about the schema being a four-paradigm one. CS side: RAPTOR / GraphRAG / PageIndex / Topic-RAG are still engaged, not name-dropped, as is Murugaraj 2025 with metric-level specificity (BERTScore / ROUGE / UniEval). The §3.2 hierarchical-indexing reasoning is grounded in archival-science vocabulary (provenance, original order). A weak point that lingers: the History side could still operationalise more of the historian's source-criticism toolkit at the level of WHAT the toolkit looks like procedurally; but the methodological-stance addition pushes this firmly into mid-1st rather than the v1 low-1st / 2:1 boundary.

[RESULT] 4

## CATEGORY 3: General academic qualities (logic, coherence, referencing, originality, mastery)

Rubric 1st descriptor: "Original and successful work (including original research) OR mastery of interdisciplinary subject matter married to truly excellent writing, perfect referencing." **Word count is now within the cap**: 9,894w main body, 106w buffer to the 10,000 hard cap. The structural Fail is removed. Logic and coherence: the §3 → §4 → §5 → §6 → §7 → §8 spine is intact and has been sharpened by the trim — the cross-references that v1 had wrong (§3.3 → §3.2 in §1; §4.2 → §4.3 for the LLM-post-correction ablation) are now correct. Referencing has graduated from "no reference list" to a full Harvard References section (40 entries). The two attribution errors v1 had (Soper / Maheshwari) are corrected to Kanerva et al. (2025) and Greif et al. (2025). The filename-string `zhao-2024-doclayout-yolo` is now `Zhao et al. (2024)`. The Doucet 2020 "convergence" claim is softened in §4.1 to what Doucet actually reports. Originality: chronologically-given hierarchy + agent-mediated drill-down + missing-data-as-first-class-node remains genuinely novel; the empirical demonstration (3 case studies × 3 trials × 2 judges) is non-trivial original research. Mastery: §4's cold-cache discipline, the 1885 page_accuracy-0.683 ground-truth-error story, the post-correction-hurts result, and §6.2's variance disclosure all stand. Writing remains dense but disciplined; no LLM-tells. The §6.5 trim removed redundant per-case mini-narratives; the table + sign-tests + κ list + cost paragraph + methodology notes carry the new material in 472w against the v1 1,765w. This is now firmly mid-1st on textual quality without the over-length cap.

[RESULT] 4

## CATEGORY 4: Integration/synthesis OR problematisation due to disciplinary disagreement

Rubric 1st descriptor: "Excellent integration/synthesis of disciplines as original insight or evidenced by deep appreciation of existing interdisciplinary synthesis; OR excellently characterised dissensus." §7.3 is now 467w (down from 868w) and stronger. The synthetic claim ("Mausoleo's chronologically-given hierarchy is the computational form of the archival principle of provenance") still lands. The new paragraph at the top of §7.3 explicitly NAMES the dissensus the synthesis resolves: "computational retrieval traditions (RAPTOR, GraphRAG, PageIndex) treat hierarchy as something to be induced from the data ... archival science (Cook, 2013; Schellenberg, 1956) treats hierarchy as something to be respected from the source ... Historians of the press routinely resist algorithmic salience filters as a category of source distortion." The reconciliation move ("chronology is at once a property the source already has and a structure the system can compute over without inducing it") is the load-bearing original sentence. Ketelaar's activation frame is then used to answer the historiographer's resistance ("holding the source layer separate from the description layer, which is the distinction the index physically enforces"). This is dissensus-named-then-resolved synthesis, which is the rubric-5 pattern. The W29 prolepsis reframing is preserved. The 26 July signature instance is preserved. High-1st in reach.

[RESULT] 5

## EXTRA DIMENSION: Stance clarity

Every section advances the thesis: §3 motivates the architecture against the synthesis, §4 reports OCR competitively without overclaiming, §5 owns the consistent-summary-length trade-off, §6 reports negative results honestly (the case-3 metric was wrong; admits it), §7 closes the loop. Stance is well-calibrated throughout.

[RESULT] 5

## EXTRA DIMENSION: Imperative robustness

The draft now avoids the v1 over-claims that Coherence flagged. Abstract no longer says "in every case" without qualification; it says "preferred by both LLM judges on a three-dimension rubric on the judge-mean score in every case tested ... with judge agreement varying across cases (Cohen's κ = 0.33 / 0.57 / 0.14)." §7.1 no longer says "BM25 baseline cannot return anything"; it says "the BM25 baseline cannot return any article from 26 July because none exist in the corpus, but the agent can still reason about the absence using context from surrounding days; §6.2 reports baseline recall 0.67 on the broader 25–27 July relevance set." §8 no longer says "definitional capability gap that flat retrieval cannot close at all"; it says "exposed a definitional capability gap: flat retrieval can reason around the absence but cannot ground it in a node that the index itself owns." The §6.2 closing now reports "definitional alongside the quantitative comparison" rather than "definitional rather than quantitative" (which was at war with §6.2's actual quantitative content). All paired sign tests still report their high p-values (0.125–1.000) with the modest conclusion. Strong calibration.

[RESULT] 5

## EXTRA DIMENSION: Engagement specificity

The Preface now explicitly names Dr Yi Gong as supervisor ("I thank Dr Yi Gong for supervising this project; her guidance on archival methodology shaped §2.3 and §7.2") and names the BASc framework engagement specifically ("The historical methodology and machine learning modules taken in earlier years of the BASc programme supplied the working vocabulary; the BASc framework supplied the warrant to treat their intersection as a proper object of study"). The handbook's examiner-encouragement clause ("non-cognate disciplines") is implicitly addressed via the explicit Cat 2 rationale in the Preface. Engagement with the canonical sources is strong. Engagement with the BASC0024 framework is now grounded rather than gestural; the half-band of free grade that v1 was leaving on the table is now picked up.

[RESULT] 4

---

## STRENGTHS

- §1's opening question is unchanged and remains the textbook-perfect interdisciplinary frame.
- Word count is now within the cap (9,894w main body), removing the v1 binary structural Fail.
- §7.3 names the dissensus the synthesis resolves, then resolves it; this is the rubric-5 pattern for cat 4.
- All four citation errors flagged by the Citation critic in v1 are corrected; the References section is built (40 entries, Harvard).
- All three CRITICAL coherence issues from v1 (embedding-model contradiction, word-count overshoot, broken cross-reference) are resolved.
- Yi Gong + BASc engagement specificity gap is closed.
- Honest reporting throughout: §4.2's "the largest single win is a data-quality patch" stands, §6.2's variance disclosure stands, §6.4's metric-substitution honesty stands.
- The §6.5 trim from 1,765w to 472w preserved every load-bearing item (table, sign tests, κ, cost figures, methodology notes) while removing the per-case redundancy.
- No LLM-tells, no em-dashes, no symmetric both-sides framing where evidence is asymmetric.

## WEAKNESSES

- §2.3's methodological-stance addition is one sentence, not the two or three a deep cat-2 lift would carry. Reaching cat-2 = 5 would require explicitly operationalising the historian's source-criticism procedure (e.g., what the *velina*-reading workflow looks like and how Mausoleo's audit-trail enables it).
- Three trials per case still bound effect-size estimation; this is a real limitation acknowledged in §7.2 but not a rubric concern unless the evaluator wants stronger statistical claims.
- The Preface's BASc-module naming is generic ("historical methodology and machine learning modules") rather than naming specific modules by code (e.g. BASC0001, BASC0019). If a marker is also a BASc convenor they may notice.

## SPECIFIC EDITS (in priority order)

1. None of the v1 blocking edits remain unaddressed.
2. (Optional, cat-2 → 5 lift) §2.3 could add one sentence on the *velina* / source-criticism procedure, e.g., "The procedure is well-rehearsed: read each item against the day's MinCulPop directive, against the surrounding days' coverage, and against the post-war historiography that names what the regime suppressed; Mausoleo's audit-trail (every summary descends to the leaf paragraph) preserves the traversal the procedure requires." (~50w; would consume the remaining buffer to 9,944w but stay under 10,000 cap.)
3. (Optional, low-cost) §1 could name the BASc framework's "non-cognate" framing explicitly in one clause, since the Preface gestures at it without using the handbook's word. Currently the engagement-specificity score is 4; this would push it to 5.
4. (Optional, polish) The Preface's BASc-module naming could specify module codes if known; the rubric does not require this but a convenor-marker would notice.

## TRIM PLAN (LOAD-BEARING DELIVERABLE — RESOLVED)

| § | Subsection | v1 | v2 | Cut | Status |
|---|---|---|---|---|---|
| §1 | Introduction | 1,020 | 893 | -127 | Done |
| §2 | Lit review | 1,550 | 1,401 | -149 | Done (with §2.3 methodological lift) |
| §3 | System design | 1,571 | 1,375 | -196 | Done (BGE-M3 reconciled to MiniLM) |
| §4 | OCR evaluation | 1,247 | 1,135 | -112 | Done (citations fixed, Doucet softened) |
| §5 | Knowledge index | 1,175 | 1,086 | -89 | Done (BGE-M3 reconciled) |
| §6 | Case studies | 3,864 | 2,378 | -1,486 | Done (§6.5 cut from 1,765w to 472w) |
| §7 | Discussion | 1,012 | 1,212 | +200 | Done (§7.2 expanded for limitations; §7.3 reduced 868→467) |
| §8 | Conclusion | 502 | 480 | -22 | Done (overclaim softened) |
| | **TOTAL** | **11,940** | **9,894** | **-2,046** | **Within cap** |

(§7 grew slightly because §7.2 absorbed the limitations that the coherence critic flagged were promised but undelivered; the §7.3 cut was deeper than 200w, so the net is correct.)

## STANCE / INTERDISCIPLINARY FRAMING AUDIT

§7.3's synthetic claim continues to land. The new dissensus-naming sentence at the top is exactly the sentence the v1 verdict said would push cat 4 from 4 to 5. The reconciliation move ("chronology is at once a property the source already has and a structure the system can compute over without inducing it") is the load-bearing original sentence and the right shape for a cat-4 = 5 synthesis: it identifies the substantive disagreement, names where it can be reconciled rather than chosen between, and tests the reconciliation empirically in §6. The Ketelaar-frame answer to the historiographer's resistance is preserved and now does the work the v1 critique said was missing.

## ENGAGEMENT SPECIFICITY AUDIT

Yi Gong is now named in the Preface ("I thank Dr Yi Gong for supervising this project; her guidance on archival methodology shaped §2.3 and §7.2"). BASc modules are named generically as "the historical methodology and machine learning modules taken in earlier years of the BASc programme" rather than by code, which is acceptable per the v1 fallback recommendation. The Cat 2 discipline-pair rationale is named explicitly. The handbook's "non-cognate" framing is implicit in the Preface's "single-discipline dissertation could only have produced either a methodological essay without a system or a retrieval system without a reason to be chronological"; making this explicit (calling out non-cognacy by name) would lift the score to 5.

## VERDICT

Per-cat scores: cat 1 = 4 (low-mid 1st), cat 2 = 4 (mid-1st), cat 3 = 4 (mid-1st), cat 4 = 5 (high-1st).

Extra dimensions: stance = 5, imperative robustness = 5, engagement specificity = 4.

**Overall band**: low-to-mid 1st (predicted 70–74%). The cat 4 = 5 plus cat 1 + 2 + 3 all at 4 is the band-target the outline specified.

Confidence: **high**. The blocking failures from round 1 (word count, citation attribution, embedding-model contradiction, broken cross-references, overclaim language, missing supervisor naming) are all resolved. Two optional cat-lifts (§2.3 source-criticism procedure; §1 non-cognate-framing call-out) are flagged for the next round if a stretch toward high-1st is wanted; both are zero-risk additions within the remaining word buffer.

Overall band: 1st (low-to-mid)
Confidence: high
[RESULT] 4
