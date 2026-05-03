# Round 71 plan — STRATEGY 1 (AuthorMist, wider scope, stricter chunking)

## 1. R70 result + diagnosis

R70: 1/3 PASS at pos 2 lean. Below R61's 2/3.

Two of three FAIL critics flagged universal R61–R69 tells (balanced antithesis,
three-case symmetric design, Italian quotation register) that R70's narrow
paraphrase scope (§2.1 + §4.3 wraparound only) did not touch.

Root cause: §3 + §4.2 paraphrased outputs were reverted because AuthorMist
dropped 29% of mask tokens (citations + numerics). The "Inputs are X. Outputs
are Y." parallel construction tell in §3 thus survived untouched.

## 2. R71 design

Two changes from R70:

(a) **Stricter AuthorMist invocation** — pre-split paragraphs > 80 words into
sub-paragraphs by sentence; temperature 0.5 (down from 0.7); per-paragraph
retry up to 3 attempts when token-retention < 95% before falling back to original.

(b) **Wider paraphrase scope** — add §1 (Chapter 1: A missing newspaper) and §5
(Chapter 5: Discussion) to the paraphrase target set. These two chapters carry
the universal balanced-antithesis cadence flagged by all 5 R65–R70 verdicts.

NOT included (preserve as R61 PASS-cited cohort-mirror):
- Preface (R61 PASS critic praised it; R68 FAIL flagged it but R61 still BEST)
- Abstract (load-bearing positioning)
- §2.3 cognitive-science argument spine
- §4.1 missing 26 July headline + Italian quotation block
- The specific OCR composite-score numbers in §3 ("0.872 on 1885, 0.926 on 1910")
  — explicitly preserved as PASS-cited engineering-frustration texture

## 3. Paraphrase target (R71)

Sections to paraphrase:
- §1 Chapter 1: A missing newspaper — full chapter, 4 paragraphs, ~520 words
- §2.1 Existing digitised newspaper archives — 2 paragraphs, 253 words (re-paraphrase)
- §3 Chapter 3: How Mausoleo is built — full chapter, ~1,321 words
- §4.2 Two shorter cases — 1 paragraph, 151 words
- §4.3 wraparound paragraph after table — 216 words
- §5 Chapter 5: Discussion — selective on argumentative paragraphs (NOT the closer)

Total target: ~2,500-3,000 words paraphrased out of 6,724.

## 4. Stricter AuthorMist invocation

Improvements to `run_authormist.py`:
- Sentence-level pre-split for paragraphs > 80 words (paraphrase smaller units)
- Temperature 0.5
- Top_p 0.85
- Per-paragraph retry: if token-retention < 95% on attempt N, retry up to 3 times
  with re-roll. If still < 95%, fall back to original.
- Hallucination detection (keep R70's check)

## 5. Decision logic

If R71 lands 3/3: STOP, mission complete.
If R71 lands 2/3: COMMIT as new BEST_GAN (cleaner distribution-shifted).
If R71 lands 1/3: try R72 with even wider scope (incl. abstract paraphrase).
If R71 lands 0/3: PIVOT TO STRATEGY 2 (SICO voice-clone) at R72.
