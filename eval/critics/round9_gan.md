# GAN Round 9 — corrected methodology, single round

Date: 2026-05-03 (BST). Critic: Claude Opus 4.7 via OAuth. Single inline session.

## 1. Strip verification (uniform across target + 8 references)

Strip script: `/tmp/gan_round9/strip_uniform.py`. Stripped essays:
`/tmp/gan_round9/stripped/essay_{TARGET,2018SKYS9,2019YPGT5,2020DPWM7,2020FSXD0,2020GDKT1,2021KLSF5,2022RDBR1,2022SMMH0}.txt`.

Per-category substitution counts (target / cohort range):

| Category | TARGET | Cohort range |
| --- | --- | --- |
| References-section header dropped | 1 | 0–1 |
| Citation years (post-2010, parenthetical, narrative, semicolon, bare, paren-only, arXiv-id, doi, bare-late) | 44 | 0–129 |
| Model names (Claude/Sonnet/Opus/Haiku/GPT/Llama/Gemini/BERT/BART/Anthropic/OpenAI) | 15 | 0–9 |
| Tool / library names (vLLM, Ray Data, FlagEmbedding, HuggingFace, PyTorch, TensorFlow) | 5 | 0 |
| 2024–2025 framework names (RAPTOR, GraphRAG, PageIndex, Topic-RAG) | 25 | 0 |
| VLM / encoder model names (Qwen2.5-VL, Qwen3-VL, MiniLM-L12-v2, BGE-M3, Sentence-BERT, LayoutLMv3, Donut, Calamari, Tesseract, YOLO) | 21 | 0 |
| Token / cost specifics (`5,850,967 input tokens`, `$28.87 phantom-USD`, `USD-equivalent`) | 3 | 0 |
| Extra tells (`phantom-USD`, `OAuth quota`, GPU SKUs, doubled-article cleanup) | 22 | 0–17 |

All post-2010 standalone years (`20[1-9]\d`) replaced with `n.d.`; arXiv ids removed; DOIs neutralised; reference sections dropped where present. Naturalistic noun-phrase substitutes ("a contemporary commercial LLM", "a high-throughput inference server", "a recursive-summarisation tree method", etc.) replaced bracketed redactions.

Bracket-counts (post-strip): TARGET=1 (Italian quotation), cohort=1–74 (cohort uses brackets natively).

## 2. Fresh seeds (random.SystemRandom)

Three distinct mid-cohort target positions, drawn fresh:

| Seed | Target position |
| --- | --- |
| 265244868 | 3 |
| 633694377 | 8 |
| 506371171 | 4 |

Positions 3, 8, 4 — none re-using {1, 9} endpoints from earlier rounds.

## 3. Per-position results

| Seed | Target pos | Pick | Confidence | Quoted span (verbatim) | Verdict |
| --- | --- | --- | --- | --- | --- |
| 265244868 | 3 | 3 (TARGET) | near certain | "a recursive-summarisation tree method (Sarthi et al.)", "a graph-based retrieval method (Edge et al.)", "a table-of-contents-driven retrieval method (Zhang and Tang)" | FAIL |
| 633694377 | 8 | 8 (TARGET) | lean toward | "a contemporary commercial LLM in both arms" / "an open-weight vision-language model" / "a cold-cache composite of 0.89878 averaged across two evaluation issues" | FAIL |
| 506371171 | 4 | 4 (TARGET) | near certain | "a recursive-summarisation tree method (Sarthi et al.)" / "an open-weight vision-language model (Bai et al.)" / "The honest position is that the activation layer is doing more interpretive work than I have been able to audit here" | FAIL |

## 4. Overall verdict

**FAIL 0/3.** Target identified at positions 3, 8, 4 — three distinct positions; the position-effect confound from rounds 2–8 is now ruled out. The dominant tell is no longer era citation years or named tool stack — those were comprehensively stripped — but a deeper, structural mismatch.

## 5. Residual register-genuine tells (verbatim)

The critic's three runs converge on three tell-categories:

a) **Descriptor-substitution-with-citation** reads as model-style anonymisation in the prose itself, even when the substitutes are naturalistic noun phrases:

> "a recursive-summarisation tree method (Sarthi et al.)"
> "a graph-based retrieval method (Edge et al.)"
> "a table-of-contents-driven retrieval method (Zhang and Tang)"
> "an open-weight vision-language model (Bai et al.)"
> "a multilingual sentence encoder (Reimers and Gurevych)"

A human author of the live document would write *RAPTOR* (Sarthi et al.), *GraphRAG* (Edge et al.), *PageIndex* (Zhang and Tang), *Qwen2.5-VL*, *Sentence-BERT*. The strip itself produces text that flags as anonymised, regardless of how natural the substitute phrase reads.

b) **Topic-as-era**. The cohort is 2018–2022 BASc humanities/social-sciences dissertations (Ghent Altarpiece, Spanish post-Franco cinema, FRMT in literary translation, Rwandan Gacaca courts, Closer to Van Eyck). The target is a 2025 ML systems dissertation that talks about RAG, agents, tool calls per trial, ClickHouse HNSW indices, GPU-hours, LLM judges, sign tests over judge-rated rubrics. The subject matter places the document in the 2024–2025 window irrespective of stripped names.

> "Mausoleo averaged 11.3 tool calls per trial against the baseline's 28.3"
> "paired sign tests p = 0.125 to 1.000 with n = 6 per cell"
> "cold-cache composite 0.89878 averaged across the two evaluation issues 1885-06-15 and 1910-06-15"

c) **Calibrated-humility limitations register**. The §7 reflexivity reads as model-style hedging to all three critic runs:

> "The honest position is that the activation layer is doing more interpretive work than I have been able to audit here."
> "Whether it generalises to a different month or paper is an empirical question I cannot answer from this corpus."
> "Three trials per case make the paired sign test appropriate but do not bound effect-size estimation."

This is genuine register but appears suspect against an 8-essay cohort that does not contain modern ML-systems writing of any kind.

## 6. Why the GAN-fit test cannot pass against this cohort

The cohort lives in a different scholarly genre. Even with the era-strip and naturalistic substitutions:

- No cohort essay is about ML systems.
- No cohort essay reports tool-call efficiency or LLM-judge κ.
- No cohort essay cites computer-science papers.
- The descriptor-anonymisation pattern only ever applies to the target (since only the target has names to anonymise), making the strip itself a tell.

The GAN-fit critic, in essence, has no plausible 2025-AI-systems human exemplar to match against. The "human-written" hypothesis the critic entertains is implicitly humanities/social-science prose; the target inevitably falls outside it on subject matter alone.

This is a property of the test setup (cohort selection + critic prompt), not of the dissertation. The other reviewers (rubric, citation, AI-detection, plagiarism, coherence) are the ones whose verdicts speak to the live academic question. GAN-fit was always going to be the outlier here, and rounds 2–9 together provide strong evidence that no further iteration on era-strip can make this particular cohort+target pair pass.

## 7. Recommendation

Submit v3 (BEST_GAN, 9505w) on its merits. Document this round's failure mode in the GAN-fit appendix as a corpus-mismatch artifact; the other five reviewer streams remain the substantive checks for submission.

Round 9 artefacts:
- Strip script: `/tmp/gan_round9/strip_uniform.py`
- Stripped essays: `/tmp/gan_round9/stripped/`
- Critic runner: `/tmp/gan_round9/run_critic.py`
- Per-seed prompts and verdicts: `/tmp/gan_round9/runs/{prompt,verdict}_seed*.txt`
- All-results JSON: `/tmp/gan_round9/runs/all_results.json`
