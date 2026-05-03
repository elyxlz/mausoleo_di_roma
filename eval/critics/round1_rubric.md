# Phase 3 Round 1 — Rubric Critic Verdict

**Target draft**: `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v1.md`
**Measured main-body word count**: 12,333 (per per-section retabulation; user's headline 11,971 likely subtracts subheadings; either way the draft is ≥10% over the 10,000 hard cap and is therefore currently capped at 40% pass regardless of quality).
**Target band**: high-1st on cats 1+4, mid-1st on cats 2+3.
**Marker stance**: anonymous, BASC0024 final dissertation rubric (4 cats), with three additional dimensions per the rubric_prompt.md template (stance clarity, imperative robustness, engagement specificity).

---

## CATEGORY 1: Framing of the research question/purpose in an interdisciplinary light

Rubric tier descriptor for 1st: "Research question/project framed clearly and comprehensively to reveal motivation for interdisciplinary approach and outlines how it will be tackled." The opening of §1 lands this descriptor — *"How does a historian read a month of a fascist-era newspaper across the rupture of 25 to 27 July 1943?"* is a historiographical question that the engineering then answers, which is the cleanest possible form of an interdisciplinary frame at this rubric. The two-task-type carve-up (aggregate questions, missing-data questions) names the gap concretely. The case-1 frame ("simultaneously a CS retrieval problem, an archival-science question, and a historical event") is the single best sentence in the dissertation for cat 1; it appears once in §1 and is repeated effectively in §6.2 and §7.1. The Preface states the interdisciplinary commitment plainly without over-claiming. Where this slips toward 2:1 is in §1's middle paragraphs: the Mausoleo-extends-RAPTOR-and-PageIndex moves are CS-internal rather than interdisciplinary, and the framing-paragraph density would benefit from one sentence stating that the discipline pair is non-cognate (history-as-archival-science is closer to information science than to literature, which is part of why the synthesis is non-trivial). High-1st territory once trimmed; the question itself is excellent.

[RESULT] 4

## CATEGORY 2: Disciplinary grounding

Rubric 1st descriptor: "Excellent awareness of epistemological and methodological stances of two (or more) disciplines in relation to the subject matter. Insightful detail and excellent grasp of more general points." Disciplinary grounding is split between History (Annales/Braudel, archival science via Cook 2013, Ketelaar 2001, Schellenberg 1956, Italian-press historiography via Murialdi 1986, Forno 2012, Bonsaver 2007, plus Pavone 1991 / Bosworth 2005 / Deakin 1962 for the regime change) and CS (RAPTOR, GraphRAG, PageIndex, plus the OCR / IR baseline lineage of BM25, BGE-M3, ReAct, Lewis 2020). §2.1, §2.2, §2.3 each operate at a competent literature-review register; §2.3 in particular handles the Da/Underwood debate with appropriate hedging ("The critique applies with less force to Mausoleo than to most computational literary studies, because Mausoleo does not produce statistical claims about its corpus"). The History side is genuinely engaged, not name-dropped — Cook's "active mediation," Ketelaar's "tacit narratives," Schellenberg's primary/secondary distinction all do interpretive work in §3.2 and §7.3 rather than sitting in the lit review only. The weakness is methodological-stance specificity: the dissertation tells the reader what each discipline *holds* (Annales = multi-resolution, archival science = provenance) but is thinner on how each *operates epistemologically* (e.g., the historian's source-criticism toolkit, the IR community's relevance-judgement protocols, the OCR community's CER-vs-character-recognition convention). The Murialdi/Forno block in §2.3 reads as situating the corpus rather than as engaging Italian-press historiography's methodological commitments. Mid-1st sits in reach but is not yet hit; this is currently a low-1st / high-2:1 boundary.

[RESULT] 3

## CATEGORY 3: General academic qualities (logic, coherence, referencing, originality, mastery)

Rubric 1st descriptor: "Original and successful work (including original research) OR mastery of interdisciplinary subject matter married to truly excellent writing, perfect referencing." Logic and coherence: section-to-section flow is strong — §3 architecture → §4 OCR eval → §5 index quality → §6 evaluation → §7 discussion → §8 conclusion is a clean argumentative spine, and the cross-references (§3.3 → §6.2 → §7.1 → §7.3 on the missing 26 July) are deliberate and function as structural reinforcement of the signature finding. Referencing is consistent Harvard ("Sarthi et al., 2024", "Cook (2013)") with no obvious format errors in the inline citations sampled; the bibliography is not in the file under review so completeness is unverifiable here. Originality: the chronologically-given hierarchy + agent-mediated drill-down + missing-data-as-first-class-node combination is genuinely novel; the empirical demonstration (3 case studies × 3 trials × 2 judges) is non-trivial original research. Mastery is visible in §4 (cold-cache discipline, ground-truth-error story at 1885 page_accuracy 0.683, the post-correction-hurts result against Thomas et al. 2024) and §5.3 (the 36→7→6→1 entity-survival trace is the kind of empirical handle that examiners reward). The writing is dense but disciplined; no LLM-tells (no "delve," no "tapestry," no "in conclusion"), no symmetric both-sides framing where evidence is asymmetric. *The single load-bearing failure on cat 3 is the word count.* At 12,333 main-body words the dissertation is ≥10% over the 10,000 hard cap and capped at 40% regardless of how well any of the above is executed. This is a binary structural failure that cannot be argued around. Until the trim plan below is applied, cat 3 is structurally a Fail; on textual quality alone (assuming the trim is applied non-destructively) this is high-2:1 / mid-1st. Marked at the lower band per the rubric instruction.

[RESULT] 2

## CATEGORY 4: Integration/synthesis OR problematisation due to disciplinary disagreement

Rubric 1st descriptor: "Excellent integration/synthesis of disciplines as original insight or evidenced by deep appreciation of existing interdisciplinary synthesis; OR excellently characterised dissensus." §7.3 is the dissertation's load-bearing synthesis attempt: *"Mausoleo's chronologically-given hierarchy is the computational form of the archival principle of provenance"* — and this lands. The argument is that Annales-school stratification of temporal scales and Schellenberg/Cook/Ketelaar's provenance-and-activation are the same prescription expressed in two vocabularies, and that the chronological hierarchy is the computational object at which they coincide. This is a *synthetic* claim, not a side-by-side juxtaposition; the case studies of §6 then test it empirically rather than asserting it. The W29 prolepsis (§5.3) is reframed in §7.3 as Ketelaar-activation rather than as model error, which is the move that turns a possible bug into evidence for the claim — examiner-friendly territory. The missing 1943-07-26 as the "signature finding" closes the synthetic loop because it is simultaneously a CS retrieval object, an archival-science exemplar (provenance of absence), and a historical event. The reason this scores 4 not 5: §7.3 at 868 words is the longest discussion subsection but its argumentative core is one move; some of those words could be redirected to *characterising the friction* between the two disciplines before declaring the synthesis (e.g., the historiographer's resistance to algorithmic salience as a real epistemic objection that Mausoleo's "summary as activation" frame addresses but does not dissolve). Currently the synthesis is asserted and tested, but the dissensus that the synthesis resolves is named only obliquely. High-1st on cat 4 is in reach with a small reframe plus modest trimming.

[RESULT] 4

## EXTRA DIMENSION: Stance clarity

Every section advances the thesis: §3 motivates the architecture against the synthesis, §4 reports OCR competitively without overclaiming, §5 owns the consistent-summary-length trade-off explicitly, §6 reports negative results (the case-3 article-id-recall metric was wrong) honestly, §7 closes the loop. No section is purely descriptive. The honesty of §4.2 ("the largest single win is therefore a non-machine-learning data-quality patch, and the reader is owed the qualifier") and §6.2's variance disclosure (trial 2 recall dip to 0.45) raises the score: stance is not just clear, it is well-calibrated.

[RESULT] 5

## EXTRA DIMENSION: Imperative robustness

The draft generally avoids unwarranted certainty: paired sign tests are reported with their high p-values (0.125–1.000) and the conclusion is explicitly the modest one ("Mausoleo wins consistently on the cases tested, not that the win generalises with bounded confidence"). The N=3-trial limitation is named in §6.5 and §7.2. The single area of soft over-claim is the §7.3 claim that flat retrieval *cannot* handle missing-data without "a separate missing-data subsystem bolted on" — a more careful framing is "without ad-hoc out-of-band metadata." The statistical hedging is otherwise calibrated, and there is no symmetric both-sides framing where the evidence is asymmetric (the post-correction-hurts result in §4.3 is reported as the asymmetric result it is, against Thomas et al. 2024 / Soper-Kanerva 2025).

[RESULT] 4

## EXTRA DIMENSION: Engagement specificity

This is the dimension where the draft most clearly drops a band. The supervisor (Dr Yi Gong) is **never named** in the draft body, the Preface, or anywhere else. There is no mention of any seminar, support session, or convenor (Sicard / Dar / Nicolas) frame; no fingerprint of having engaged with BASC0024-specific material beyond the one mention "BASC0024 Final Year Dissertation" on the cover line. There is no mention of which BASc modules feed in (the Preface gestures at "prior modules in historical methodology and in machine learning" but does not name any). The handbook's "examiners are encouraged to reward projects of a more radical interdisciplinary nature which may span disciplines usually regarded as less cognate" is exactly the prompt this dissertation should pick up explicitly — history-as-archival-science + CS-as-IR-systems-engineering is non-cognate and the draft should say so. Engagement with the canonical sources is strong (Cook, Ketelaar, Schellenberg, Braudel, RAPTOR, GraphRAG); engagement with the *BASC0024 framework specifically* is missing. Not catastrophic — the rubric does not require the supervisor be named — but it is a free hand to grade that the draft is currently leaving on the table.

[RESULT] 2

---

## STRENGTHS

- §1's opening question is a textbook-perfect interdisciplinary frame: a historiographical question whose answer requires engineering, with the missing 1943-07-26 as the signature instance that holds three disciplines (CS retrieval, archival science, history-of-the-event) in a single object.
- §7.3 commits to a synthetic claim ("the chronological hierarchy is the computational form of provenance") rather than juxtaposing disciplines side-by-side. This is the single highest-scoring move on cat 4, and it is empirically tested by §6 rather than asserted.
- Honest reporting throughout: §4.2's "the largest single win is a data-quality patch," §6.2's trial-2 recall dispersion to 0.45, §6.4's frank disclosure that the first-run case-3 metric was wrong and was replaced. Examiners reward this.
- The OCR-evaluation chapter (§4) is the disciplinary-grounding chapter for the CS side — cold-cache discipline, the ground-truth-error story at 1885 page_accuracy 0.683, and the negative LLM-post-correction result against Thomas et al. 2024 are all the mark of someone who has actually run the system.
- Cross-reference discipline is excellent: §3.3 → §6.2 → §7.1 → §7.3 on the missing 26 July is a deliberate structural spine.
- No LLM-tell prose, no symmetric both-sides framing where evidence is asymmetric.

## WEAKNESSES

- **WORD COUNT IS THE LOAD-BEARING FAILURE.** At 12,333 main-body words the draft is ≥10% over the 10,000 hard cap and is currently capped at 40% pass regardless of any of the above. This is binary and structural; nothing else matters until it is fixed. Required cut: ≥2,433 words to reach 9,900 (100w buffer).
- §6.5 is grossly overgrown at 1,763 words against an outline target of 300 — roughly 6× over. The redundant per-case prose ("Case 1 — the missing 1943-07-26", "Case 2 — July 25 regime change", "Case 3 — comparative coverage across July") restates §6.2/§6.3/§6.4 verbatim. The cost / billing-model / phantom-dollar / embedding-restoration / methodology-notes blocks together account for 600–700w that belong in an appendix or in §3.1/§7.2 by reference.
- §7.3 is 868w against 300w outline target. The synthesis lands but in 350w; the rest is restatement.
- Disciplinary-stance specificity (cat 2): the dissertation tells the reader what each discipline *holds* but is thin on how each *operates epistemologically*. The Italian-press historiography block in §2.3 (Murialdi, Forno, Bonsaver) reads as corpus-situating rather than as methodological engagement.
- Engagement specificity: Yi Gong is not named anywhere; no seminar/convenor/handbook fingerprint; no named BASc modules in the Preface.
- §7.3 declares the synthesis without first naming the dissensus the synthesis resolves. The historiographer's resistance to algorithmic salience is a real epistemic objection that Ketelaar-activation answers but does not dissolve; making this resistance explicit would push cat 4 from 4 to 5.
- §6.2's quote of the Italian summary text (the `[edizione assente: ...]` block) is load-bearing for the case but currently a 100w bilingual excerpt that should remain — but the surrounding meta-narration around it is bloated.

## SPECIFIC EDITS (in priority order, file:section → action)

The trim plan below is the load-bearing edit list. Listed here in priority order with quoted spans and rewrite directions; the per-section word-count cuts that implement these are tabulated in the next section.

1. **`MAUSOLEO_FULL_DRAFT_v1.md`:§6.5 — collapse from 1,763w to ~350w.** The four "### Case N — ..." restatement blocks (lines ~309–356, ~440w combined) duplicate §6.2/§6.3/§6.4 and must be deleted entirely. The "Cost (absolute)" block (~330w) collapses to a 60w paragraph with the per-query and one-time totals; move full breakdown to §7.2 or an appendix. The "Embedding restoration" / "Char-budget caveat" / "Methodology notes" blocks (~350w combined) collapse to a single 80w paragraph or move to a footnote. Keep: the headline results table, the sign-test bullet list, the inter-judge κ list, the case-3-metric-substitution paragraph (already in §6.4 — could be cut here since §6.4 owns the rationale).

2. **`MAUSOLEO_FULL_DRAFT_v1.md`:§7.3 — collapse from 868w to ~350w.** The synthesis lands in the first three paragraphs (~400w). The remaining ~470w restates Braudel/Cook/Schellenberg/Ketelaar in repeated forms; cut the second restatement. Add: one sentence near the top naming the dissensus the synthesis resolves ("Historians of the press routinely resist algorithmic salience filters as a category of source distortion; Ketelaar's activation frame answers this concern by holding the source layer separate from the description layer, which is the distinction the index physically enforces").

3. **`MAUSOLEO_FULL_DRAFT_v1.md`:Preface — name Yi Gong and the BASc framework specifically.** Currently 410w, can stay at 410w with a substitution: replace the generic "Prior modules in historical methodology and in machine learning supplied the working vocabulary" with a sentence naming 1–2 actual BASc modules (whichever are honest — methodology side and ML side) and adding "I thank Dr Yi Gong for supervising this project." Names the supervisor and grounds the BASC0024-framework engagement at zero word cost.

4. **`MAUSOLEO_FULL_DRAFT_v1.md`:§2.1 — trim the Impresso paragraph from 326w to ~250w.** The "transparent generosity" Düring quote and the systems' page counts can be tightened; the positioning point ("Mausoleo addresses the access modality this template under-serves") is already made twice in §1 and §2 intro, so §2.1's third paragraph can lose its first 60w.

5. **`MAUSOLEO_FULL_DRAFT_v1.md`:§2.3 — tighten the Italian-press historiography block from ~200w to ~120w** and use the recovered budget to add 80w of methodological-stance specificity for cat 2 (e.g., one sentence on the source-criticism toolkit historians bring to the regime press; one sentence on what this means for whether a summary is treated as primary or secondary evidence).

6. **`MAUSOLEO_FULL_DRAFT_v1.md`:§3.1 — trim the deterministic-merge paragraph from 524w to ~400w.** The REPLACE/ADDITIVE/quality-weighted detail belongs in §4.2 (where it appears again) or an appendix; §3 should describe the architecture, not the merge config.

7. **`MAUSOLEO_FULL_DRAFT_v1.md`:§4.2 — trim the per-component decomposition from 369w to ~300w.** The leave-one-out swing values (0.029, 0.015, 0.002–0.017) are worth a sentence, not a paragraph.

8. **`MAUSOLEO_FULL_DRAFT_v1.md`:§4.3 — trim the LayoutLMv3/Donut/Tesseract aside from 396w to ~320w.** The "not evaluated head-to-head because of domain mismatch" point can compress to 30w.

9. **`MAUSOLEO_FULL_DRAFT_v1.md`:§5.1 — trim the schema description from 284w to ~220w.** Schema details overlap with §3.2; the duplication (level / parent_id / position / date_range / summary / embedding / raw_text) should appear once with a back-reference.

10. **`MAUSOLEO_FULL_DRAFT_v1.md`:§6.2 — trim the case-1 narration from 681w to ~520w.** The Italian summary quote stays. The "two judges disagree at κ = 0.33" passage can compress to a sentence; the variance-note paragraph already cross-references `case_1_variance_note.md` and can lose its in-text repetition.

11. **`MAUSOLEO_FULL_DRAFT_v1.md`:§3.3 — trim the human/agent inversion paragraph from 362w to ~290w.** The "the human never sees the JSON unless they ask for it" closing belongs in §6 or §8, not in §3.3 systems.

## TRIM PLAN (LOAD-BEARING DELIVERABLE)

Target: main body ≤ 9,900w (100w buffer under 10,000 hard cap). Current measured: **12,333w**. Required cut: **≥2,433w**.

| § | Subsection | Current | Target | Cut | Rationale |
|---|---|---|---|---|---|
| §1 | Introduction | 1,020 | 880 | -140 | Tighten the RAPTOR/PageIndex/Topic-RAG positioning paragraph (the third graf). Already covered in §2.2. Keep the opening question, two-task-type carve-up, and case-1-as-signature framing intact. |
| §2.1 | Existing archives | 326 | 250 | -76 | Compress the Impresso "transparent generosity" paragraph; the positioning claim is already in §1 and §2-intro. |
| §2.2 | IR lineage | 512 | 440 | -72 | Trim the BM25/Salton/Robertson historical-baseline paragraph (~50w cut); the Mausoleo-extends-this-lineage paragraph (~22w cut). |
| §2.3 | Historical methodology | 593 | 540 | -53 | Trim the Da/Underwood debate prose; the Italian-press block compresses but the recovered words go into adding methodological-stance specificity (net cut 53w; cat 2 lift). |
| §3.1 | OCR pipeline | 524 | 380 | -144 | Move the REPLACE/ADDITIVE/quality-weighted merge detail to §4.2 or appendix; §3 keeps the architectural description. |
| §3.2 | Hierarchical indexing | 500 | 430 | -70 | Trim the schema description (overlaps with §5.1); collapse the "central design commitment is given not learned" closing (overlaps with §5.2 closing). |
| §3.3 | Agent-mediated search | 362 | 280 | -82 | Trim the human/agent inversion paragraph (3rd graf); the architectural point lands in 1 sentence. |
| §4.1 | OCR methodology | 387 | 340 | -47 | Compress the composite-score formula explanation; the formula is self-documenting. |
| §4.2 | Pipeline configuration | 369 | 300 | -69 | Compress the per-component leave-one-out values to a sentence. |
| §4.3 | Comparison | 396 | 320 | -76 | Tighten the LayoutLMv3/Donut/Tesseract domain-mismatch aside; compress the post-correction comparison to Thomas/Soper-Kanerva. |
| §5.1 | Schema and node IDs | 284 | 220 | -64 | Replace overlapping schema description with a back-reference to §3.2. |
| §5.2 | Recursive summarisation | 393 | 340 | -53 | Trim the Wu-2021/Yang-2016 lineage paragraph; the prior is named in §2.2 already. |
| §5.3 | Quality assessment | 420 | 360 | -60 | Tighten the 25 July example trace (the W29 prolepsis is already discussed in §6.3 and §7.3). |
| §6.1 | Experimental setup | 355 | 320 | -35 | Compress the relevance-GT provenance paragraph. |
| §6.2 | Case 1 (07-26) | 681 | 520 | -161 | Compress the inter-judge κ disagreement passage; cut the variance-note in-text repetition (xref `case_1_variance_note.md` instead). Keep the Italian summary quote. |
| §6.3 | Case 2 (07-25) | 456 | 380 | -76 | Tighten the "useful artefact of the W29 prolepsis" paragraph (already covered in §5.3 and §7.3). |
| §6.4 | Case 3 (comparative) | 427 | 360 | -67 | Compress the metric-substitution rationale (already restated in §6.5; can be one paragraph here). |
| §6.5 | Aggregate results | 1,763 | 350 | **-1,413** | **Largest single cut.** Delete the four "### Case N — ..." restatement subsections (lines ~309–356, ~440w). Compress the "Cost (absolute)" block to a 60w paragraph with totals; move detailed breakdown to §7.2 or appendix. Collapse "Embedding restoration" + "Char-budget caveat" + "Methodology notes" to one 80w paragraph or footnote. **Keep**: the headline results table, the sign-test bullet list, the inter-judge κ list, the metric-substitution one-paragraph note. |
| §7.1 | What case studies show | 374 | 320 | -54 | Compress the case-2/case-3 numerical recap (the table in §6.5 already carries it). |
| §7.2 | Limitations | 252 | 240 | -12 | Minor tighten; this section is well-sized and absorbs the cost figures from §6.5. |
| §7.3 | Annales hierarchy as provenance | 868 | 360 | **-508** | **Second-largest single cut.** Keep the synthetic claim (first three paragraphs, ~400w) and add one sentence naming the dissensus the synthesis resolves. Cut the second restatement of Braudel/Cook/Schellenberg/Ketelaar; the literature is named in §2.3 and §5.1. |
| §8 | Conclusion | 502 | 460 | -42 | Tighten the future-work enumeration (4 directions can compress to 2 sentences). |
| | **TOTAL** | **12,333** | **9,820** | **-2,513** | Brings main body to 9,820w, 80w under the 9,900 buffer (180w under hard cap). Allows 100–180w expansion budget if any cut goes too aggressive. |

**Order of cuts to implement first** (highest leverage):
1. §6.5 (-1,413w) — delete the case restatements; compress cost/embedding/methodology blocks. **This single edit gets the dissertation from "capped at 40%" to "under 10% over."**
2. §7.3 (-508w) — trim the second restatement; keep the synthesis.
3. §6.2 (-161w) — tighten the inter-judge / variance-note passages.
4. §3.1 (-144w) — relocate merge config to §4.2/appendix.

After edits 1+2 alone the draft is at ~10,412w — still 4% over but in the <10% band where the penalty is -5pp rather than the cap. After all four highest-leverage edits the draft is at ~10,107w — still over but very close. Edits 5–N (the remaining trim table) bring the draft to 9,820w.

## STANCE / INTERDISCIPLINARY FRAMING AUDIT

§7.3's synthetic claim **does land**. The argument that Annales-school stratification of temporal scales and Schellenberg/Cook/Ketelaar's provenance-and-activation are the same prescription expressed in two vocabularies — and that the chronological hierarchy is the computational object at which they coincide — is a genuine synthesis, not a side-by-side juxtaposition. Three reasons it works:

1. The synthesis is *predictive*: it predicts that the missing 26 July, archivally significant precisely because it is a gap in the provenance, will be a first-class object in the right computational form. §6.2 then tests this prediction empirically and finds it holds.
2. The synthesis is *load-bearing for the architecture*: the choice to make the hierarchy chronological rather than learned (the §3.2 commitment) is justified by the synthesis, not the other way around. This is the right direction of justification — the engineering follows from the disciplinary commitment, not vice versa.
3. The W29 prolepsis is reframed in §7.3 as Ketelaar-activation rather than as model error. This is the move that turns a possible bug into evidence for the synthetic claim, and it is the kind of reframing that distinguishes integration from juxtaposition.

Cat 4 reads as integration, not as side-by-side. Where it falls short of high-1st: §7.3 declares the synthesis without first naming the dissensus the synthesis resolves. Adding one sentence near the top of §7.3 — historians of the press routinely resist algorithmic salience filters as a category of source distortion, and Ketelaar's activation frame answers this concern by holding the source layer separate from the description layer — would push cat 4 from 4 to 5 at zero word cost (since the §7.3 cut is already 508w).

## ENGAGEMENT SPECIFICITY AUDIT

**Yi Gong is not named anywhere in the draft body or Preface.** Searched for "Yi Gong", "Gong", "supervisor", "BASc", "BASC0024", "seminar"; only hit is the cover line "BASC0024 Final Year Dissertation". This is a free hand to grade that the draft is leaving on the table — the rubric does not strictly require the supervisor be named, but the Preface explicitly invites BASc-framework engagement ("explains interdisciplinary rationale and how it connects to BASc modules" per the handbook), and acknowledging the supervisor is standard.

The Preface gestures at "prior modules in historical methodology and in machine learning supplied the working vocabulary" but names no specific module. No mention of the BASC0024 seminar series, no co-convenor (Sicard/Dar/Nicolas) reference, no fingerprint of having engaged with handbook framing beyond the cover line. The handbook's examiner-encouragement clause ("examiners are encouraged to reward projects of a more radical interdisciplinary nature which may span disciplines usually regarded as less cognate") is exactly the prompt the dissertation should pick up — history-as-archival-science + CS-as-IR-systems-engineering is non-cognate (less cognate than e.g. CS + cognitive science), and the draft should say so explicitly in §1 or the Preface.

**Recommended fix at near-zero word cost**: in the Preface, replace "Prior modules in historical methodology and in machine learning supplied the working vocabulary" with "Prior BASc modules — [name 1 history-side module, e.g. a historiographical methods seminar; name 1 CS-side module, e.g. an ML or NLP module] — supplied the working vocabulary, and I thank Dr Yi Gong for supervising the project." Adds 12w, recovers a half-band on the engagement-specificity dimension and at the margin on cat 1.

## VERDICT

Overall band (with current word count):

- **As-submitted (12,333w main body, ≥10% over 10,000 cap)**: capped at 40% pass per BASC0024 over-length rule. Quality is irrelevant to mark until trimmed.

Overall band (assuming the trim plan is applied and the draft hits ≤9,900w main body):

- Cat 1: high-2:1 / low-1st (4 → low 1st with the framing tweak)
- Cat 2: low-1st (3 → mid-1st with the §2.3 methodological-stance addition)
- Cat 3: mid-1st (2 → 4 once word-count is fixed; high-2:1 / mid-1st on textual quality)
- Cat 4: low-1st (4 → high-1st with the §7.3 dissensus sentence)

**Predicted final band post-trim**: low-to-mid 1st (66–72%), tracking the outline.md target of high-1st on cats 1+4 + mid-1st on cats 2+3.

Confidence: **high** on the word-count diagnosis and the per-section cuts (these are mechanical); **medium** on the post-trim band prediction (depends on how cleanly the cuts preserve the strongest passages). The §6.5 cut is the single highest-leverage edit in the entire dissertation.

[RESULT] 3
