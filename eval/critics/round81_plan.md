# Round 81 plan — push from 2/3 to 3/3

## Strategy

R80 hit 2/3 PASS at LEAN_TOWARD. The single FAIL critic (319113977 near-certain) flagged:
- Balanced antithesis "X handles Y; Z handles W" cadence (still in SICO §1, §2.1, §2.2)
- Abstract-noun-as-subject sentences "The pay-off shows up most clearly", "The failure mode here is at the level of the data model itself"
- Meta-hedging at every result
- Definitional paragraph openers "The X is Y" — flagged in §3 ("The dominant access mode...", "The OCR stage receives scanned JPEGs...", "The closest prior work...")

R81 targets the highest-leverage tells the FAIL critic flagged:

1. **§3 paragraph-opener variation**: change definitional openers to action-verb or context-clause openers. The R72 cross-model §3 still has "The OCR stage receives...", "The closest prior work...", and others. Vary at least 4 paragraph openers in §3.
2. **Abstract-noun-subject substitution in §1+§2**: scan §1 + §2.1 + §2.2 for "The X is Y" / "The X shows up" / "The X holds Y" sentence openers, substitute concrete-agent or first-clause-context openers.
3. **Aphoristic-closer scrub**: scan §1 + §2 + §3 (NOT §4 which has the Italian block, NOT §5 which is fresh) for short aphoristic closers, expand them.

## Implementation

a. Start from R80 v10 (now at /tmp/mausoleo/references/MAUSOLEO_FULL_DRAFT_v10.md).
b. Edit-tool §3 to vary 4 paragraph openers.
c. Edit-tool §1 + §2.1 + §2.2 abstract-noun-subject replacements.
d. Edit-tool aphoristic-closer expansions where present.
e. Strip + GAN.

## Pareto rule

If R81 ≥ R80 (2/3 LEAN), promote to v10. If R81 < R80 (i.e., 1/3 or 0/3), revert to R80 v10.

## Word count target

R80 = 7,124w. R81 changes net out to ~+50w. Expected ~7,175w. Within cap.

## Risk

The "definitional paragraph opener" tell is partly intrinsic to academic prose; over-varying may produce affected-sounding openers that introduce new tells. Test with sanity-check.
