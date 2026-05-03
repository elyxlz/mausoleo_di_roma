# GAN Round 41

Strip: TARGET 6,456 words.
Seeds: 435255288 (pos 2), 544285469 (pos 4), 606887493 (pos 6).

Edits applied:
- Stripped Preface to acknowledgment-only.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 435255288 | 2 | 2 (TARGET) | near certain | FAIL |
| 544285469 | 4 | 4 (TARGET) | near certain | FAIL |
| 606887493 | 6 | 6 (TARGET) | near certain | FAIL |

Result: 0/3, all near-certain (REGRESSED in confidence from round 40 lean-toward).

## Key signal: Strip-script bug introducing "an one-month" tells

Critic seed 435255288 flagged "an open-weight vision-language model" (twice), "an one-month corpus build", "an unconstrained research configuration", "an episodic-retrieval task" as "faintly stilted hyper-formal article use that LLMs produce."

"an one-month" is from the strip script's `\ba\s+([aeiouAEIOU])` → `an X` regex, which rewrites "a one-month" to "an one-month" because 'o' is matched as a vowel even when the word starts with a consonant-sound vowel (one, unique, university). This is a strip artifact, not in v10.

The other "an X" instances ("an open-weight", "an unconstrained", "an episodic-retrieval") are correct article use in the source, but their cluster reads as a tic.

## Round 42 plan

1. Patch the strip script's "a → an" regex to skip "one", "one-X", "U-words" (unanimous, university, unique, used, uniform).
2. Defuse "Italian-quote flourish" (the bracketed Italian summary block was flagged STRUCTURAL as authenticity-performance).
3. Restore a fuller Preface — the all-acknowledgment Preface didn't help.
