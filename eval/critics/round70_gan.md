# GAN Round 70 — STRATEGY 1 (AuthorMist sentence-level paraphrase, narrow scope)

Strip: TARGET 5,848 words (paraphrased v10 6,720 words).
v10 = R61 baseline (commit 420027e). Paraphrased file = `/tmp/gan_round70/v10_full_paraphrased.md`.
Seeds: 434602589 (pos 5), 946052068 (pos 2), 712153256 (pos 7).

## Edits applied (BEFORE the revert)

AuthorMist (`authormist/authormist-originality`, Qwen2.5-3B-Instruct fine-tune)
applied paragraph-by-paragraph at temperature 0.7, top_p 0.9, on a masked v10
draft. Mask classes: citations (C), proper nouns (P), italics/Italian (I),
technical terms (T), numbers (N), file paths (F), markdown headers/tables (H).

Target sections (4 chunks):
- §2.1 (Existing digitised newspaper archives) — 253w
- §3 (Chapter 3: How Mausoleo is built) — 1,321w
- §4.2 (Two shorter cases) — 151w
- §4.3 wraparound (Aggregate numbers paragraph) — 216w

Per-chunk token-retention audit after AuthorMist run:
- chunk 0 (§2.1):  92% retention — KEPT paraphrased
- chunk 1 (§3):    71% retention — REVERTED (25 dropped tokens incl. citations + numbers)
- chunk 2 (§4.2):  77% retention — REVERTED (11 dropped numerics)
- chunk 3 (§4.3 wraparound): 92% retention — KEPT paraphrased

Net distribution shift: §2.1 + §4.3 wraparound only (469w paraphrased; 6,251w
identical to R61 baseline).

## Verdicts

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 434602589 | 5 | 5 (TARGET) | near certain | FAIL |
| 946052068 | 2 | 5 (= 2022SMMH0) | lean toward | PASS |
| 712153256 | 7 | 7 (TARGET) | near certain | FAIL |

Result: **1/3 PASS**. Below R61's 2/3 BEST.

PER PARETO RULE: v10 stays at R61 baseline (commit 420027e). No commit to v10.

## What the verdicts said

**Seed 434602589 (FAIL near-certain)** flagged:
- Balanced antithesis with semicolons (universal R61–R69 tell, untouched by R70)
- "Inputs are X. Outputs are Y." parallel construction in §3 (unchanged because §3 reverted)
- Three-case symmetric experimental design in §4 (STRUCTURAL, untouched by R70)
- Italian quotation block as "too-perfect framing"
- Aphoristic chapter titles
- Praised: "0.872 on 1885, 0.926 on 1910" OCR numbers + "0.6 to 1.1 composite points"
  failure-reporting as positive engineering frustration

**Seed 946052068 (PASS lean-toward, picked Essay 5 = 2022SMMH0 Artificial Creativity)** flagged
2022SMMH0 on:
- Balanced antithesis "is not X but Y"
- Triadic question framing revisited verbatim in Discussion
- Fabricated-sounding numerical specificity
- IMRAD beats too-clean
Mausoleo at pos 2 was not flagged (cohort-mirror PASS).

**Seed 712153256 (FAIL near-certain)** flagged Mausoleo at pos 7 on the
universal balanced-antithesis cadence + three-case symmetry STRUCTURAL tell.

## Why R70 didn't move from R61

The narrow paraphrase scope (only §2.1 + §4.3 wraparound) left every R61–R69
high-leverage tell intact:
- Balanced antithesis with semicolons (§1, §2, §3, §4, §5 all carry it)
- Aphoristic closers (§1, §3, §4 still carry them)
- Three-case symmetric experimental design (STRUCTURAL, §4 unchanged)
- Italian quotation register
- Preface "I came from X, encountered Y, realised Z" arc

The reverted §3 chunk would have most affected the "Inputs are X. Outputs are Y."
parallel construction tell, but token-loss in AuthorMist's output forced the revert.

## Token-loss diagnosis for R71

AuthorMist Qwen2.5-3B at temperature 0.7 dropped 36 of 122 §§...§§ tokens
across chunks 1+2 (29% loss). Hypotheses:
- Long input paragraphs (260w+) blow past the model's effective attention window
  for placeholder-tracking
- Numeric-dense text (chunk 2 has 26 numeric tokens in 151 words) is the worst
  case for placeholder-tracking
- Temperature 0.7 may be too high for placeholder fidelity

R71 plan: re-run AuthorMist with (a) hard paragraph-length cap (split paragraphs
> 100w into sub-paragraphs by sentence), (b) temperature 0.5, (c) per-paragraph
retry up to 3 attempts with token-retention check.

## Decision: continue per Strategy 1 escalation rules

Per Phase 3 Stage B 70+ directive: "iterate AuthorMist scope (more sections /
different sections) for 1-2 more rounds" before pivoting to SICO.

R71 plan: AuthorMist with stricter paragraph-chunking on the wider scope
(§1, §3, §5 mid-prose).
