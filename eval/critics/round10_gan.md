# GAN Round 10 — first round on cog-sci-reframed v8

Date: 2026-05-03 (BST). Critic: Claude Opus 4.7 via OAuth. Inline session.

## 1. Strip verification (uniform across target + 8 references)

Strip script: `/tmp/gan_round10/strip_uniform.py` (reused from round 9, source pointed at `MAUSOLEO_FULL_DRAFT_v8.md`).

Stripped essays in `/tmp/gan_round10/stripped/`. Per-category substitution counts (target):

| Category | TARGET |
| --- | --- |
| References-section header dropped | 1 |
| Citation years (post-2010) | ~40 |
| Model names | 13 |
| Tool / library names | 4 |
| Framework names (RAPTOR, GraphRAG, PageIndex, Topic-RAG) | 25 |
| VLM / encoder model names | 21 |
| Token / cost specifics | 0 (cog-sci reframe stripped most cost prose) |
| Extra tells | 19 |

## 2. Fresh seeds (random.SystemRandom)

| Seed | Target position |
| --- | --- |
| 901924162 | 7 |
| 365590892 | 1 |
| 802810236 | 3 |

## 3. Per-position results

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 901924162 | 7 | 7 (TARGET) | near certain | FAIL |
| 365590892 | 1 | 9 (decoy) | lean toward | PASS |
| 802810236 | 3 | 3 (TARGET) | near certain | FAIL |

## 4. Overall verdict

**FAIL 1/3.** Tied with rounds 4–8 best (1/3). The cog-sci reframe did NOT change the dominant tell, which remains descriptor-substitution from the strip itself.

## 5. Residual tells (verbatim from critic)

a) **Descriptor-substitution-with-citation** (unchanged from round 9):
> "a recursive-summarisation tree method (Sarthi et al.)"
> "a graph-based retrieval method"
> "an open-weight vision-language model (Bai et al.)"
> "a contemporary commercial LLM"
> "a high-throughput inference server"
> "a research-grade GPU"

b) **Hedged self-aware caveat phrasing** (LLM-style register):
> "Rigorous testing of the cognitive parallel against human researchers is left to future work; the present evaluation tests the design's effect on an LLM-agent proxy"
> "The honest caveat is that..."
> "The honest position is that..."

c) **Numerical scaffolding**:
> "averaged 11.3 tool calls per trial against the baseline's 28.3"
> "paired sign tests p = 0.125 to 1.000 with n = 6 per cell"

## 6. Edit plan for round 11

The "honest caveat" / "honest position" / "headline finding" register MUST go (eliminate meta-commentary phrases). The "tests the design's effect on an LLM-agent proxy" appears verbatim in abstract + §7.3 — keep one, rewrite the other. Cog-sci reframe is good but does not by itself address surface register tells.
