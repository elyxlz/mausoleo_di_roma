# Round 75 plan — STRATEGY 4 SICO voice-clone

## Strategy

SICO style-anchored paraphrase using Elio's own prior academic writing as in-context style exemplars for Haiku 4.5. Skipped by the previous agent (jumped from AuthorMist R70-R71 directly to cross-model R72-R74); landing it now.

The hypothesis is that the GAN flags R61-R74 baselines on a "polished machine-smooth performance" texture that survives default-Claude rewrite (R72-R74) precisely because Claude's default register IS the polished register. Anchoring on Elio's actual recent prose (PHIL0046 essay round_70 v70, BASC0048 essay round_5_authormist v32) should drag the surface toward his real distributional fingerprint: paragraph-length variance, mid-sentence asides, first-person grounding when relevant, sentence fragments at high-stakes turns, and the occasional rough cadence the polished-Claude register avoids.

## Style anchor corpus selection

- **PHIL0046 v70**: 3,649 words. Recent (May 2026), graded 1st-class register, Elio's authorial voice on cognitive-science material — directly relevant register for §2.3 cog-sci spine adjacencies. Selected paragraphs:
  - lines 7-11 (intro: "Lake et al. (2017) put sample-inefficiency...", paragraph hook + concrete-number ground)
  - lines 31-35 (McCoy slope-not-step argument: rebuttal cadence, Elio's "I think this overshoots" mid-paragraph turn, slope/step contrast)
  - lines 41-45 (Mary thought experiment: reframing move with "It helps here to push on a thought experiment of my own", first-person hedge "That is weaker than I would like.")
  - lines 56-57 (Spelke residue paragraph: "There is one piece of Spelke's data I have not figured out how to handle on this picture, and given the word limit I am going to flag rather than resolve it.")

- **BASC0048 v32**: 2,057 words. Recent (Apr 2026), HCI/STS register but the structural-argument cadence is the exact analogue for Mausoleo's §2 + §5 critical-discussion register. Selected paragraphs:
  - lines 5-7 (intro paragraph + Figure 1 personal-data anchor: "I have been getting Discover Weekly since I was sixteen...")
  - lines 30-32 (Discover Weekly defence-breaks-at-X analytical paragraph)
  - lines 36 (the four-criteria-with-bolded-headers paragraph; mirrors Mausoleo's archive-criteria material in §2.1)
  - line 50 (artist-side political-artefact paragraph: cumulative argument with cross-references)

These two essays together carry: (a) personal-experience ground anchored in concrete dates/projects, (b) cited literature woven into argument rather than displayed, (c) mid-paragraph "I think X overshoots / I want to push on" first-person turns, (d) hedge tail-clauses ("That is weaker than I would like", "I do not have a tidy answer to this"), (e) sentence fragments at high-stakes argumentative turns. None of these are present in the polished v10.

## Sections to apply SICO to

Per dispatch: §1, §2.1, §2.2, §5. Skip §3 (technical-engineer register, different load), §2.3 (cog-sci spine, load-bearing — risk too high), §2.4 (corpus context, short and citation-dense), §4 (case studies + table — too risky for R75).

Word counts (approx, from v10):
- §1 Chapter 1 lines 23-35: ~712 words
- §2.1 Existing digitised newspaper archives lines 44-48: ~310 words
- §2.2 The hierarchical-retrieval lineage lines 50-58: ~525 words
- §5 Chapter 5 Discussion lines 159-167: ~415 words

Total ≈ 1,962 words ≈ 29% of the 6,724-word body. Wider scope than R72 (~9%), narrower than R73 (~47%) and R74 (~80%). The diff is that R75 changes the register-anchor (Elio voice) where R73/R74 changed only sections (default Claude voice).

## SICO procedure

1. Extract source paragraphs from v10 for §1, §2.1, §2.2, §5.
2. Mask citations (Author, Year), proper nouns (Mussolini, Pavone etc.), numbers, Italian phrases, technical terms (ClickHouse, BM25, RAPTOR, GraphRAG, etc.) using placeholder tokens — NOT done in cross-model R72-R74. The mask reduces Haiku's tendency to overfit on the citation/terminology surface and forces it to attend to prose register.
3. Compose a Haiku 4.5 system prompt that specifies: (a) you are voice-cloning the author of the in-context exemplars, (b) preserve mask tokens verbatim, (c) preserve markdown headers, (d) no em-dashes, no " - ", no balanced-antithesis-with-semicolon, no aphoristic closers.
4. User prompt includes 3-5 in-context exemplar paragraphs from PHIL0046 v70 + BASC0048 v32, then the masked target.
5. Generate paraphrase. Run sanity-check: mask integrity, ±15% word count, no em-dash, no " - ".
6. Restore masks.
7. Spot-check named-device integrity (ClickHouse, vLLM etc. all back).

## Prose-quality assessment per candidate

Pre-run: Haiku 4.5 with strong style anchors should produce prose that is closer to Elio's actual register than R72-R74's default-Claude paraphrase. Failure modes:
- Style-anchor leakage: rewritten Mausoleo prose imports first-person idiosyncrasies that DO NOT belong in a dissertation body (Discover Weekly's "I have been getting since I was sixteen" register would not transfer cleanly to §2.1). Mitigation: system prompt explicitly says "voice-clone the cadence and sentence-rhythm but preserve the third-person dissertation register where the source is third-person".
- Over-rough register: PHIL0046 has more first-person hedging than the dissertation conventionally allows. Mitigation: target sections §1, §2.1, §2.2, §5 are precisely the sections where some authorial register is acceptable; §3 and §4 stay Claude-default polished.
- Mask-restore corruption: Italian quotation block in §4 is preserved (§4 not in scope); other Italian lemmas (Pavone, Murialdi titles) are masked-and-restored.

## GAN test

Strip → 3 fresh seeds at non-pos-1 positions → Opus 4.7 critic per existing run_critic.py.

## Pareto rule

If R75 < R61 (2/3), revert v10 to R61 baseline 420027e. R75 paraphrased version stored at /tmp/gan_round75/v10_sico.md and only promoted to v10 on R75 ≥ 2/3.

## Word count target

v10 currently 6,724w. SICO ±15% on ~1,962 affected words allows ±294 net swing on the affected sections. Total stays ≤7,000w (well under 9,950w cap).
