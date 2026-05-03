# Round 70 plan — STRATEGY 1 (AuthorMist sentence-level paraphrase)

## 1. Strategy escalation context

Rounds 61–69 exhausted the surface + structural + combined-deletion playbook against
the cohort-variance noise floor. R61 holds 2/3 BEST_GAN with no improvement after
9 single- and combined-edit rounds.

Strategy escalation per Elio's Phase 3 Stage B 70+ directive: pivot to AuthorMist
sentence-level paraphrase on technical-methodology prose — the lowest argument-spine
cost sections — to introduce a measurable distribution shift on the surface text
without touching the load-bearing argument.

## 2. Concrete scope of AuthorMist application

Three sections selected for paraphrase, all low argument-spine cost:

(a) **§3 (Chapter 3: How Mausoleo is built)** — full chapter. Lines 78–108.
   Technical-methodology prose. Argument is "the system has these stages and they
   compose"; paraphrase cannot damage that. ~1,800 words.

(b) **§2.1 (Existing digitised newspaper archives)** — lines 44–48.
   Historical-survey prose. Argument is "three named systems define the field";
   paraphrase preserves names + numbers, only varies framing prose. ~400 words.

(c) **§4.2 (Two shorter cases mid-prose, line 136)** + **§4.3 caption-context
   prose around aggregate numbers (lines 138-156)**. Wraparound prose, NOT the
   numerical table itself or the headline numbers. ~300 words paraphrasable text.

Total target: ~2,500 words paraphrased out of 6,724 = ~37% of v10. Below the 50%
threshold above which the paraphrase model risks introducing register drift visible
to the critic.

## 3. Mask-and-restore protocol

Per essay-iter editorial-moves catalog: mask first, paraphrase, restore.

Mask classes (in order):
- §§Cnnn§§: every parenthetical (Author Year) citation + every narrative
  "Author (Year)" citation
- §§Pnnn§§: every proper noun (people, places, organisations: *Il Messaggero*,
  Mussolini, Pavone, Bartlett, ...)
- §§Innn§§: every italicised Italian phrase / quotation block
- §§Tnnn§§: every technical term (ClickHouse, HNSW, BM25, RAPTOR, GraphRAG,
  PageIndex, Topic-RAG, vLLM, Qwen, BGE-M3, ReAct, ...)
- §§Nnnn§§: every numerical figure (0.90, 6,480, 13.3, 27.0, 0.67, ...)
- §§Fnnn§§: every file path / API endpoint / identifier (e.g. `1943-07-26`,
  `nodes`, `documents`, `/root`, `1943-07-25_a127`)
- §§Hnnn§§: every section header / markdown table

After paraphrase: restore all masks. Spot-check that:
- All citations restored intact (count match)
- All numerics restored intact (count match)
- All proper nouns + Italian phrases restored intact (count match)
- All file paths + technical terms restored intact (count match)

## 4. AuthorMist invocation

Model: `authormist/authormist-originality` (Qwen2.5-3B-Instruct fine-tune, ~6GB
fp16, fits on the 8GB GTX 1080).

Run paragraph-by-paragraph with per-paragraph length cap to prevent register
drift across long paragraphs. Temperature 0.7, top_p 0.9.

Skip headers, tables, code blocks, < 8-word lines.

## 5. Expected outcome

Per Elio's escalation note: "Expect distribution shift to flip 1-2 seeds."

If R70 lands 3/3: STOP, mission complete.
If R70 lands 2/3 (matches R61): COMMIT as new BEST_GAN baseline (cleaner
distribution-shifted prose), continue R71 with refined AuthorMist scope.
If R70 lands 1/3 or 0/3: pareto-revert and try AuthorMist with different
scope (R71 different sections, R72 wider scope) before SICO pivot.

## 6. Prose-quality assessment per candidate section

(a) §3: low risk. Methodology prose. Paraphrase can only improve fluency.
(b) §2.1: low risk. Survey prose. Names + numbers masked, only framing varies.
(c) §4.2 wraparound: low risk. Already short. Paraphrase touches few sentences.

NO paraphrase of:
- Abstract (load-bearing positioning prose, would introduce register drift
  visible against the 8-essay cohort baseline)
- Preface (the R61 Pass critic explicitly cited Preface as positive cohort-mirror)
- §1 Chapter 1 (load-bearing thesis prose; R61 Pass critic cited Ch1 technical
  texture positively)
- §2.3 Memory/hierarchy/external (load-bearing cognitive-science argument spine)
- §4.1 missing 26 July headline (R61 Pass cohort-mirror exemplar)
- §5 Discussion (R61 closer was a cohort-mirror PASS)

## 7. Working directory

`/tmp/gan_round70/` — paraphrase intermediates + masked drafts + restored drafts.
v10 in `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v10.md` is touched only on
final commit. Pareto-revert is `git checkout v10`.
