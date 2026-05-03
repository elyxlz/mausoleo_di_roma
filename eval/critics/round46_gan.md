# GAN Round 46

Strip: TARGET 6,247 words.
Seeds: 505318722 (pos 6), 99568979 (pos 5), 32748809 (pos 3).

Edits applied (per round46_plan.md):
- Replaced abstract tricolon with one declarative + sequenced sentences naming missing-day/regime-change/balance.
- Rewrote Ch1 opener to lead with concrete archival encounter ("A query for *Il Messaggero* on the date 26 July 1943, addressed to any of the major digitised newspaper archives... returns an empty result page").
- Collapsed the now-duplicate archive-enumeration paragraph in §1.
- Cut §1 parenthetical "(typically either in the interface or, by default, in the reader's head)".
- Softened §4 "recall tie is more a property of the metric than of the systems" → "does not separate the systems on this case".
- Cut §4 "Sign-test p-values across the eighteen trials..." sentence.
- Plain-sequenced the §1 cognitive-science "with the everyday consequence" trailing clause.

| Seed | Target pos | Pick | Confidence | Verdict |
| --- | --- | --- | --- | --- |
| 505318722 | 6 | 6 (TARGET) | near certain | FAIL |
| 99568979 | 5 | 5 (TARGET) | near certain | FAIL |
| 32748809 | 3 | 3 (TARGET) | near certain | FAIL |

Result: 0/3 near-certain. REGRESSED from R45's 1/3 lean-toward.

## High-leverage tells flagged across all 3 critics
- **Hook recapitulation across abstract/§1/§2/§3/§4/§5** — seed 32748809 explicitly counts six restatements of the missing 26 July anchor. The R45 reopening did NOT remove the recap, only varied the wording.
- **"X handles Y; Z handles W" balanced antithesis with semicolons** — seed 32748809 quoted Preface, §2.1 (Topic-RAG), §4 ("rests on the index/rests on what the agent already knew"). The R45 split-into-two of the bicolon now reads as two-beat parallel.
- **"Three literatures and a corpus" Ch2 framing** — flagged as IMRAD survey-paper move.
- **"All eighteen planned trials completed (18/18)" parenthetical** — performative tidiness flagged twice.
- **Italian quotation block "La lacuna archivistica del 26 luglio è essa stessa documento"** — seed 505318722 says it "matches the surrounding English argument too neatly to be a quoted summary the system produced. It is the AI paraphrasing its own thesis in Italian costume".
- **Pre-emptive scope-hedging at chapter close** — seed 99568979 quotes "How a human reader actually engages..." and "A direct head-to-head on Impresso would be the obvious next step, except that the corpus is in French and German".
- **Vocabulary signature**: "calendar-shaped tree", "calendar-given hierarchy", "slot" (used 4+ times metaphorically), "prolepsis", "the substantive lesson is".

## Round 47 plan
PRIMARY: rewrite the §4 missing-day section to NOT recapitulate the 26 July framing — assume the reader has it from §1. Cut the §3 reference to "26 July with empty leaves" and the §3 "this is the architectural precondition for the lead case study" sentence. Cut the §5 final paragraph's restatement of the 26 July gap.
SECONDARY: replace "The Mausoleo answer rests on the index. The baseline answer rests on what the agent already knew." with single non-parallel sentence (this is now a DOUBLE-FLAG from r45 and r46). Replace the §2.1 "a Topic-RAG pipeline takes a query and looks for topically relevant articles, while Mausoleo takes a temporal slice..." with non-parallel construction.
