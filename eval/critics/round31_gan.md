# GAN Round 31 (Stage B, single focused round)

Strip script: `/tmp/gan_round31/strip_uniform.py` (TARGET = v10).
Stripped TARGET word count: 8,262.
Seeds: `random.SystemRandom()` draws 7540483 (pos 5), 109302126 (pos 7), 474270991 (pos 6). All non-pos-1, all distinct.
Critic: Claude Opus 4.7 via OAuth, single call per seed, ALL 3 INLINE. Prompt = `~/.claude/skills/essay-iter/adversarial_prompt.md`.

## Cohort example mining (Phase 0)

Three verbatim exemplars saved to `/tmp/gan_round31/cohort_examples.md`. Selected:

- **Type A (seminar / module reference)**: 2018SKYS9 Preface line 6, "Citizen Science for Radical Change taught by Dr Kat Austen first sparked my interest in introspection and subtleties of the physical experience". Gold-standard pattern: named module, named tutor, specific intellectual debt to the dissertation question.
- **Type B (sustained close-reading)**: 2021KLSF5 §4.1.2 lines 332-352, the Waldorf 2013 wrestling. Pattern: name the scholar and exact claim with page number; quote the claim; say "I argue"; bring a definitional source that adjudicates; apply back to the case.
- **Type C (scope acknowledgment)**: 2021KLSF5 §5.2 lines 1015-1020, "I have not addressed many cases of severe miscarriages of justice... a detailed account of the human rights toll of these trials was beyond the scope of this dissertation." Pattern: name the specific thing not done; name where to go for it; give an honest reason (theoretical focus, not capacity).

## Three moves applied to v10

1. **Preface, BASc reference**: appended a sentence to the third Preface paragraph naming the "autumn-term Cognitive Sciences seminar series" where Whittington's TEM was set as a core reading alongside Behrens et al., and recording the specific intellectual debt (the structure-content factorisation idea registering as something an interface could be designed against).
2. **§2.3 (Memory, hierarchy and external structure), Whittington close-reading**: expanded the original single paragraph into four. Three new paragraphs paragraph-by-paragraph engage with Whittington 2020: (a) gloss the structure-content factorisation with a quoted claim, (b) name where I would extend his argument (calendar-given vs learned structure) and a small disagreement, (c) mark the boundary on the borrowing (TEM is single-cell normative, ergonomics runs through Clark and Chalmers). ~430 words across the three new paragraphs.
3. **§5 (Discussion), scope acknowledgment**: added an "I cannot pursue a human-subjects evaluation... within the scope of this dissertation" sentence, naming exactly what the case-study design tests (LLM-agent proxy on a fixed three-question battery) and giving the honest structural reason (a properly powered think-aloud study would itself be a project of comparable size).

Word count: v9 = 8,268; v10 = 8,980 (+712, well under the 9,950 ceiling).

## Strip + seed verification

| Field | Value |
|---|---|
| Strip script | `/tmp/gan_round31/strip_uniform.py` |
| Strip target | `MAUSOLEO_FULL_DRAFT_v10.md` |
| Strip applied uniformly | TARGET + 8 refs |
| Stripped TARGET words | 8,262 |
| Seed source | `random.SystemRandom()` |
| Position-1 banned | yes (re-roll loop) |
| Distinct positions | yes (5, 7, 6) |

## Per-position table

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 7540483 | 5 | 5 (TARGET) | near certain | FAIL |
| 109302126 | 7 | 7 (TARGET) | near certain | FAIL |
| 474270991 | 6 | 6 (TARGET) | near certain | FAIL |

**Result: 0/3.**

## Overall verdict: FAIL

Worse than the round-30 baseline of 1/3. The three cohort moves did not transfer.

## Residual tells (round 31, by frequency across the three critics)

The cohort moves were each individually flagged as new tells:

- **Whittington close-reading section (move 2)** — flagged as a structural tell by both seed 109302126 and seed 474270991 in nearly identical language: "stages a 'close reading' with manufactured intellectual humility... then performs a 'small disagreement I would name' — this is the LLM tic of generating apparent intellectual independence by inventing a disagreement to mark" (seed 474270991); "performs interdisciplinary synthesis with suspicious smoothness — flags its own boundary, names the inferential leap, stages a 'small disagreement' with the source" (seed 109302126). The cohort exemplar B1 (Waldorf wrestling in the Rwanda essay) read as authentic; the same move executed on Whittington reads as performed. The difference appears to be that Waldorf is a named critic of the writer's own object (Gacaca), so disagreeing with him is forced by the topic; Whittington is a generic cog-sci-side underwriter the dissertation does not actually need to disagree with, so the manufactured disagreement reads as theatre.

- **Preface BASc reference (move 1)** — flagged by seed 474270991: "the preface performs interdisciplinarity-anxiety in a way that reads as prompt-following: 'The discipline pair this dissertation works within is cognitive science and computer science, which is the natural pairing given my BASc concentrations.' Then it inventories influences in a list-like cadence... that reads as constructed authenticity." The cohort exemplar A1 was placed in a preface dominated by a personal anecdote (the IB World Religions class memory of the Ghent altarpiece); the v10 module reference sits inside an already-structured discipline-pair paragraph and reads as inventory rather than memory.

- **Scope-acknowledgment sentence (move 3)** — flagged by seed 109302126 as part of "calibrated humility": "Pre-emptive self-limitation phrased as virtue... no human writer flags exactly the limitation a reader would flag in the exact register a reviewer would use." The cohort exemplar C1 was a paragraph header "Limitations and further research" with the scope-out sitting under a clearly demarcated sub-section; the v10 sentence is embedded inside an already-organised limitations chapter that the critics had already flagged as too tidy in earlier rounds.

Persistent tells from rounds 26-30 also recurred:

- "X rather than Y" balanced antithesis cadence (high-leverage, all three critics).
- Pre-emptive limitations enumeration (still flagged structural).
- Numerical-stuffing as rhetorical authority (recall figures, κ, p-values).
- Self-glossing meta-commentary about what the work does and does not warrant.
- Parenthetical asides that double back to qualify (the LLM substitute for em-dashes).

## Diagnosis

The cohort-moves hypothesis (that mirroring patterns A, B and C from real human exemplars would buy PASS) does not hold for Mausoleo on this run. Two reasons emerge from the verdicts. First, the moves were applied as additions on top of an already heavily-edited surface that the critics had already learned to recognise across rounds 26-30; the additions inherited the existing rhetorical scaffolding rather than displacing it. Second, the cohort exemplars work in their original essays partly because of their host environment (Waldorf is a real critic of Gacaca; the IB World Religions module is a memory anchored in 2013 Brussels); transplanting the formal move without the host environment produces the formal shape without its grounding, which the critics read as performed.

## Stage B status

Round 31 is the focused single-round attempt that the dispatch specified. It does not exceed the round-30 baseline of 1/3. The cohort-moves methodology that worked for the prior PHIL0046 essay does not transfer to Mausoleo under this configuration. Returning the v10 ship as the current best draft on substantive grounds rather than on GAN-clearance grounds: the close-reading addition strengthens §2.3 as scholarship, the scope acknowledgment strengthens §5 as honesty, and the BASc seminar reference grounds the Preface, all independently of whether the era-stripped GAN target picks the dissertation out of the cohort.
