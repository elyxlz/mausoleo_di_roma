# GAN critic — Phase 3 Stage B, round 2

Run date: 2026-05-03 ~13:00 BST
Target: `/tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v2.md` (commit 3d615f8, v2 with 5 tells already scrubbed)
Cohort: 8 BASc 1st-class dissertations under `/tmp/gan_round1/extracted/`
Critic: claude-opus-4-7 via OAuth (`oauth-2025-04-20` beta), single call per seed
Strip script: `/tmp/gan_round2/strip_years.py`
Stripped inputs: `/tmp/gan_round2/stripped/`
Per-seed prompts + raw verdicts: `/tmp/gan_round2/runs/`

## 1. Year-strip verification

Stripped 41 citation-year tags from target; 271 from references (per-ref: 2018SKYS9=62, 2019YPGT5=0, 2020DPWM7=52, 2020FSXD0=10, 2020GDKT1=0, 2021KLSF5=84, 2022RDBR1=0, 2022SMMH0=63). Strip is post-2010 only and uniform across target + 8 refs. Pre-2010 citation years (Braudel 1958, Schellenberg 1956, Ketelaar 2001, Murialdi 1986) preserved; historical content years (1885, 1910, 1943, July 1943, 25 July 1943) preserved; titles, candidate codes, BASC0024/UCL tags, supervisor names, repo paths, model names, References sections all preserved.

## 2. Per-position table

| Seed | Target position | Critic's pick | Confidence | PASS/FAIL | Verbatim quoted span (truncated 150 chars) |
|------|-----------------|---------------|------------|-----------|---------------------------------------------|
| 1943 | 9 | Essay 9 | lean toward | FAIL | "The conclusion is the modest one: Mausoleo wins consistently on the cases tested, not that the win generalises with bounded confidence" |
| 1944 | 9 | Essay 9 | near certain | FAIL | "chronologically given, provenance-respecting hierarchies are the right interface form for archival research, not a decorative addition to it." |
| 1945 | 1 | Essay 6 (= 2022RDBR1, a reference) | lean toward | PASS | "Jean-Paul Sartre in Existentialism is a Humanism argues that freedom must be defined by the presence of a real choice of possibilities and not by the absence of constraints" |

## 3. Overall verdict

**FAIL at 2 of 3 positions** (seeds 1943 and 1944 both correctly identified the target; seed 1945 picked a reference essay). Per the updated skill, mixed results count as FAIL.

## 4. Verbatim tells the critic flagged for the target (drives round-3 edits)

Exhaustive list across both FAIL positions:

### Seed 1943 (target = Essay 9)

**Tell 1 — self-qualifying meta-commentary / hedging-with-precision:**
> "The conclusion is the modest one: Mausoleo wins consistently on the cases tested, not that the win generalises with bounded confidence"

Critic gloss: "this self-qualifying meta-commentary about its own claims is a recognizable LLM register."

**Tell 2 — formulaic three-part structural signposting that recurs:**
> "Three architectural commitments. First... Second... Third..."

> "Two methodological commitments are worth flagging. The first is cold-cache enforcement... The second is the 1885 page_accuracy floor"

Critic gloss: "the rigid enumerated scaffolding appears too consistently across sections."

**Tell 3 — synthetic "interdisciplinary reconciliation" framing / too-tidy doubling:**
> "The two literatures, read together, prescribe the same thing"

> "Mausoleo is one such design: its chronological hierarchy doubles as Braudelian stratification and Schellenbergian original order"

Critic gloss: "this neat doubling/coincidence claim ('happen to coincide cleanly') has the too-tidy quality of LLM synthesis where a human would show more friction between the traditions."

### Seed 1944 (target = Essay 9, near-certain pick)

**Tell 1 — "not X but Y" / antithesis-with-em-dash construction with distinctive rhythm, repeated:**
> "shaped by two commitments the historiographical and archival traditions already share, multi-resolution time and respect for provenance, rather than by a clustering induced from the data"

> "The contribution is an empirical demonstration that chronologically given, provenance-respecting hierarchies are the right interface form for archival research, not a decorative addition to it."

**Tell 2 — LLM meta-framing of its own argument:**
> "The claim is synthetic, tested empirically by the case studies, not a decorative pairing"

> "The case is reported throughout as definitional alongside the quantitative comparison."

**Tell 3 — signature "X supplies Y" parallel construction stacked repeatedly across the Preface:**
> "History supplies two things... Computer Science supplies the recent hierarchical-retrieval lineage... It also supplies the system implementation... Archival science supplies the second commitment."

**Tell 4 — RLHF-style hedging meta-commentary (overlaps Tell 1 from seed 1943):**
> "the conclusion is the modest one: Mausoleo wins consistently on the cases tested, not that the win generalises with bounded confidence"

> "the chapter does not over-claim."

**Tell 5 — triadic flourish ending sections, repeated almost verbatim across §1, §6.2, §8:**
> "a CS retrieval problem, an archival-science question, and a historical event"

**Tell 6 — Preface justification of interdisciplinarity that "reads like an LLM following a rubric":**
> "The discipline pair was chosen under the Cat 2 rationale because the question itself spans the two."

### Critic's summary characterisation of the target (verbatim)

Seed 1944: "Essay 9's prose is uniformly polished with that particular LLM cadence of balanced clauses and self-aware qualification."

Seed 1944: "The other essays show typical human dissertation messiness — uneven section quality, idiosyncratic emphases, occasional clunky phrasing."

## 5. Consolidated round-3 edit targets (verbatim spans, in priority order)

Highest-frequency / most-cited tells across the two FAIL seeds — these are the spans round 3 must rewrite:

1. **"The conclusion is the modest one: Mausoleo wins consistently on the cases tested, not that the win generalises with bounded confidence"** (cited at both seeds, both as a "strongest tell")
2. **"chronologically given, provenance-respecting hierarchies are the right interface form for archival research, not a decorative addition to it."** (cited at seed 1944 as strongest tell; same "not X but Y" rhythm)
3. **"shaped by two commitments the historiographical and archival traditions already share, multi-resolution time and respect for provenance, rather than by a clustering induced from the data"** (Abstract, same antithesis construction)
4. **"History supplies two things... Computer Science supplies the recent hierarchical-retrieval lineage... It also supplies the system implementation... Archival science supplies the second commitment."** (Preface, stacked "X supplies Y" parallel)
5. **"its chronological hierarchy doubles as Braudelian stratification and Schellenbergian original order"** (too-tidy interdisciplinary doubling)
6. **"The two literatures, read together, prescribe the same thing"** (same too-tidy doubling)
7. **"a CS retrieval problem, an archival-science question, and a historical event"** (triadic refrain repeated across §1, §6.2, §8 — break the repetition)
8. **"Three architectural commitments. First... Second... Third..."** (rigid enumeration; vary scaffolding)
9. **"Two methodological commitments are worth flagging. The first is cold-cache enforcement... The second is the 1885 page_accuracy floor"** (rigid enumeration)
10. **"The claim is synthetic, tested empirically by the case studies, not a decorative pairing"** (meta-framing)
11. **"The case is reported throughout as definitional alongside the quantitative comparison."** (meta-framing)
12. **"the chapter does not over-claim."** (hedging meta-commentary)
13. **"The discipline pair was chosen under the Cat 2 rationale because the question itself spans the two."** (Preface; reads as LLM following a rubric)

Underlying register-level pattern called out by the critic: "uniformly polished with that particular LLM cadence of balanced clauses and self-aware qualification." Round 3 should inject what the critic explicitly named as the human signature: "uneven section quality, idiosyncratic emphases, occasional clunky phrasing."

## 6. Cohort-signal note (PASS position only)

Seed 1945 (target at position 1): critic picked Essay 6 (= 2022RDBR1, a reference dissertation on online hate speech). Tells the critic cited for that ref:

- Confident misattribution of Sartre in Existentialism is a Humanism.
- Garbled paraphrase of Levinas's Totality and Infinity.
- Misrepresentation of Arendt's Eichmann thesis.

Critic's positive note on the target at this position: "Essay 1's ClickHouse details... [is] hard to fake." Concrete system-implementation detail reads as human in this seed; the LLM-cadence tells were not flagged here, suggesting position effects on attention.
