# GAN Round 34

Strip: TARGET 7,113 words.
Seeds: 159586728 (pos 3), 651322307 (pos 5), 885517005 (pos 4). All non-pos-1, distinct.

Edits applied:
- Dropped Preface reading-shaping paragraph entirely (Bartlett/Hutchins/Eichenbaum + 1885 fiction-header anecdote).
- Defused "supplies it for free" CS-blog tic.
- Defused "first-class node" CS-blog tic.
- Defused "These systems index articles. The missing day has no articles." chiasmus in §1.
- Restructured §5 limitations: collapsed cluster-paragraph into one shorter paragraph; merged "two extension directions" into one paragraph.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 159586728 | 3 | 3 (TARGET) | lean toward | FAIL |
| 651322307 | 5 | 5 (TARGET) | near certain | FAIL |
| 885517005 | 4 | 4 (TARGET) | near certain | FAIL |

Result: 0/3.

## Key residual tells (verbatim)

From seed 159586728 (lean toward, the softest FAIL):
- "Inter-judge κ is weak (0.33) and the paired sign test on quality (n = 6, p = 0.625) does not separate the two systems, so any conclusion here rests on the structural argument and not on a statistically separated outcome." — pre-emptive limitation hedging integrated into prose, flagged STRUCTURAL.
- "Existing digital newspaper archives are infrastructurally indispensable, but they are also overwhelmingly query-driven. The hierarchical-retrieval lineage in information retrieval has shown multi-resolution access to be perfectly tractable, but the hierarchies in question are normally induced from the data and not supplied by the source. And the cognitive-science material on memory and external cognition has been arguing for half a century that researchers organise temporal information hierarchically, without that argument really being operationalised in interface design." — three perfectly balanced "X is true, but Y" in a row.
- "Short epigrammatic declaratives doing summary work — characteristic LLM rhetorical flourish": "The publication calendar that the printers already followed is itself the index." "The index does not have to be smart."
- "Compact roadmap recitations": chapter map at end of §1.

From seed 651322307 (near certain):
- "Polished, rhythmically controlled prose with a suspicious cleanness."

From seed 885517005 (near certain):
- (verdict body abbreviated)

## Diagnosis

Round 34 regressed (0/3 vs round 33's 1/3). The Preface paragraph drop didn't buy anything. The CS-blog tic defusion didn't buy anything. The §1 chiasmus defusion didn't buy anything. The limitations collapse may have actually hurt.

The "pre-emptive limitation hedging integrated into prose" tell points at chapter 4's in-line caveats ("Inter-judge κ is weak..."), not at §5 cascade. Need to scrub IN-PROSE hedging in §4.

The "X is true, but Y" triplet at Ch2 opening is the new highest-leverage tell.

## Round 35 plan

1. Rewrite the Ch2 opening paragraph to break the "X but Y" triplet rhythm.
2. Scrub in-prose pre-emptive hedging in §4: remove the "so any conclusion rests on the structural argument" sentence, remove the "single-annotator construction is a limitation" tail in §4 setup paragraph.
3. Defuse "publication calendar that the printers already followed is itself the index" register tic.
4. Drop the §1 chapter-map sentence.
