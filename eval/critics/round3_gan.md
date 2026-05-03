# GAN critic — Phase 3 Stage B, round 3

Run date: 2026-05-03 ~14:00 BST
Target: `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v2.md` (commit 27d4da9, round 3 register edits + cohort-fit moves)
Cohort: 8 BASc 1st-class dissertations under `/tmp/gan_round1/extracted/`
Critic: claude-opus-4-7 via OAuth (`oauth-2025-04-20` beta), single call per seed
Strip script: `/tmp/gan_round3/strip_years.py`
Stripped inputs: `/tmp/gan_round3/stripped/`
Per-seed prompts + raw verdicts: `/tmp/gan_round3/runs/`

## 1. Year-strip verification

Stripped 39 citation-year tags from target (down from 41 in round 2 due to trims); 271 from references (per-ref unchanged: 2018SKYS9=62, 2019YPGT5=0, 2020DPWM7=52, 2020FSXD0=10, 2020GDKT1=0, 2021KLSF5=84, 2022RDBR1=0, 2022SMMH0=63). Strip is post-2010 only and uniform across target + 8 refs. Pre-2010 citation years preserved; historical content years (1885, 1910, 1943) preserved; titles, candidate codes, BASC0024/UCL tags, supervisor names, repo paths, model names, References sections all preserved.

Target main-body word count: 9,948 (cap 10,000; safety buffer 50w respected).

## 2. Per-position table

| Seed | Target position | Critic's pick | Confidence | PASS/FAIL | Verbatim quoted span (truncated 150 chars) |
|------|-----------------|---------------|------------|-----------|---------------------------------------------|
| 1943 | 9 | Essay 9 | near certain | FAIL | "Both judges are Anthropic models, so the κ values are intra-vendor; §7.2 picks this up" |
| 1944 | 9 | Essay 9 | near certain | FAIL | "The tree is the calendar." / "Chronology is the substrate they both happen to be commitments about." |
| 1945 | 1 | Essay 6 (= 2022RDBR1, a reference) | lean toward | PASS | "Decision tree classifier[53] is a type of supervised learning method..." |

## 3. Overall verdict

**FAIL at 2 of 3 positions** (seeds 1943 and 1944 both correctly identified the target with near-certain confidence; seed 1945 picked a reference essay). Per the SKILL, mixed results count as FAIL. Round 3 succeeded in pushing seed 1943 from "lean toward" to picking-the-target-but-citing-different-tells, and seed 1944 confidence held at near-certain (no improvement). Seed 1945 PASS held.

## 4. Residual tells the critic flagged in round 3 (drives round-4 edits)

The 11 round-2 tells were neutralised — none of them were re-cited at the FAIL seeds. The critic now flags a different family:

### Seed 1943 (target = Essay 9)
- "the awkwardness in §2.2 and §7.3 is downstream of that" — meta-hedging cadence; the cohort-fit move (e) introduced new "downstream of that" phrasing that itself reads as LLM register.
- "The case studies in §6 are what the claim rests on" / "Mausoleo is one such encoding" / "Architecture and principle meet most legibly there" — balanced thesis-restating closing-flourish pattern persists across multiple sections.
- "Both judges are Anthropic models, so the κ values are intra-vendor; §7.2 picks this up" — over-tidy self-referential limitations bookkeeping.
- Bibliography entry "[Online; arXiv preprint by Zhang and Tang, 2025]" flagged as malformed/hallucinated. (Note: this is a real PageIndex VectifyAI ref the dissertation actually engages with; the formatting is non-standard but the work exists. Worth normalising for round 4.)

### Seed 1944 (target = Essay 9)
- Aphoristic single-sentence paragraph: "The tree is the calendar." Cohort-fit move (b) introduced punchy short sentences that read as LLM-generated; need to soften.
- "Chronology is the substrate they both happen to be commitments about." — same pattern.
- Recursive Braudelian triad: "the événement of the deposition, the conjoncture of regime collapse, the longue durée of fascist Italy" repeated across §1, §2.3, §7.3. The triadic refrain was cut at §1/§8 in round 3 but the Braudelian triad itself recurs and is now the new tell.
- "in Ketelaar's sense" / "in the sense Cook develops" — name-dropping shortcut flagged.
- "the disagreement I want to record is" — the cohort-fit close-reading opener (move b) reads as LLM hedging-as-confidence.
- Preface lacks grounding personal details (compared to refs that mention named relatives, named seminars).

## 5. Recommended round-4 edits (in priority order)

1. **Cut the new aphoristic single-sentence paragraphs** — "The tree is the calendar." and "Chronology is the substrate they both happen to be commitments about." Round 3 introduced these as cohort-fit register breaks; the critic reads them as LLM punchlines instead.
2. **Break the Braudelian triad repetition** — name *événement / conjoncture / longue durée* together ONCE (probably §2.3 where it belongs). In §1 and §7.3, refer obliquely or pick a single register.
3. **Rewrite the round-3 "downstream of that" preface insert** — the meta-hedging it introduced is itself the new tell.
4. **Soften "the disagreement I want to record is"** — replace with a less performed close-reading frame.
5. **Replace "in Ketelaar's sense" / "in the sense Cook develops"** with proper attribution sentences.
6. **Cut "Both judges are Anthropic models, so the κ values are intra-vendor; §7.2 picks this up"** — drop the cross-reference; let §7.2 carry the limitation.
7. **Add ONE personal-grounding detail to the Preface** (named seminar, classmate objection, or specific moment of confusion) per cohort-fit theory — refs cite "my cousin Carlota" type details; Preface currently has only abstract intellectual positioning.
8. **Normalise the VectifyAI / PageIndex bibliography entry** to a clean arXiv-form ref so it reads as a standard citation, not a malformed entry.

## 6. Cohort-signal note (PASS position only)

Seed 1945 (target at position 1): critic picked Essay 6 (= 2022RDBR1) with "lean toward". Tells the critic cited for the reference: textbook-style algorithm definitions, overconfident-yet-hedged synthesis on thin evidence ("emerging correlation" from tiny Twitter samples), confabulation-style just-so hypotheses. Same reference picked at this seed in round 2; suggests strong position effect at slot 1.
