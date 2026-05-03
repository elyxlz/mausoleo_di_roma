# GAN Round 11

Date: 2026-05-03 (BST). Critic: Claude Opus 4.7 via OAuth.

## Strip + seeds

| Seed | Target position |
| --- | --- |
| 411805846 | 8 |
| 33253916 | 2 |
| 384920817 | 9 |

## Per-position results

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 411805846 | 8 | 8 (TARGET) | lean toward | FAIL |
| 33253916 | 2 | 2 (TARGET) | near certain | FAIL |
| 384920817 | 9 | 9 (TARGET) | near certain | FAIL |

## Overall verdict

**FAIL 0/3.** Same dominant tell: descriptor-substitution-with-citation. New tells called out:
- "research-grade GPU GPUs" doubling artefact from strip (RTX 3090 → "research-grade GPU" + "GPUs" appears twice)
- "the prose around it varies the presentation rather than enumerating identical comparisons" flagged as LLM tic — REMOVED for round 12
- "~a modest computational cost" / "~a moderate computational cost" remnants from strip's cost replacement applied to v8 prose

## Edits applied for round 12

- Removed "the prose around it varies..." sentence from §6.5
- Pre-emptively replaced "RTX 3090" with "consumer GPUs" in v8 to prevent the GPU GPUs double-noun strip artefact
- Replaced phantom-USD figures in §7.2 with descriptive cost prose so strip doesn't replace mid-sentence
