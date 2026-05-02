# Cognitive Science: Hierarchical Knowledge & Memory

## Why this matters for Mausoleo

Mausoleo's 7-level hierarchy (Paragraph - Article - Day - Month - Year - Decade - Archive) mirrors a structural claim with broad cogsci support: biological cognition handles unbounded information by recursively compressing experience into nested levels of abstraction. Perceptual systems are modelled as hierarchical generative models (Friston, Clark); working memory chunks primitives into higher-order units (Miller, Cowan, Gobet); long-term memory uses schemas, prototypes, and cognitive maps to organise particulars under abstract relational frames (Bartlett, Rosch, Behrens, Eichenbaum). Mausoleo is an external scaffold that pre-computes summaries users would otherwise build on the fly.

Flat full-text search treats users as Boolean query machines, but historians reading 1943 newspapers are constructing situated mental models of a month, the war effort, the city. Mausoleo's nested summaries function as an extended-mind scaffold (Clark & Chalmers; Hutchins) handing users abstractions at the level their cognition is already operating at. Modern computational cognitive science converges on the same point: hierarchical attention in transformers, hierarchical Bayesian inference, and the hippocampal-entorhinal "Tolman-Eichenbaum machine" all imply that efficient generalisation needs multi-resolution representation - higher levels carrying structural information, lower levels instance detail.

## Foundational references

### Hierarchical predictive processing
- **Friston, K. (2010). The free-energy principle: a unified brain theory? *Nature Reviews Neuroscience*, 11(2), 127-138.** Brain modelled as a hierarchy of generative models in which higher levels predict lower-level activity; only prediction errors propagate upward.
- **Clark, A. (2013). Whatever next? Predictive brains, situated agents, and the future of cognitive science. *Behavioral and Brain Sciences*, 36(3), 181-204.** Brains as prediction machines using hierarchical generative models.
- *Connection*: justifies the seven-level summary stack as cognitively congenial. A historian browsing the Month summary is handed a top-down prior that absorbs the Article-level content with much less prediction error than raw OCR would.

### Chunking and working memory
- **Miller, G. A. (1956). The magical number seven, plus or minus two. *Psychological Review*, 63(2), 81-97.** Working memory operates on chunks; chunking is the principal route around capacity limits.
- **Cowan, N. (2001). The magical number 4 in short-term memory. *Behavioral and Brain Sciences*, 24(1), 87-114.** Pure capacity ~4 chunks; recoding into larger chunks is the main way humans hold complex structure in mind.
- **Baddeley, A. (2012). Working memory: theories, models, and controversies. *Annual Review of Psychology*, 63, 1-29.** Multi-component model with episodic buffer binding chunks across modality and LTM.
- **Gobet, F., & Simon, H. A. (1996). Templates in chess memory. *Memory & Cognition*, 24(4), 493-503.** Expert chunks recursively compose into hierarchical "templates" - direct empirical analogue of Mausoleo's nested summaries.
- *Connection*: each Mausoleo level is a pre-built chunk. A historian skimming a Day summary reads ~1 chunk where flat search would force them to hold dozens of articles in working memory simultaneously.

### Levels of processing
- **Craik, F. I. M., & Lockhart, R. S. (1972). Levels of processing: a framework for memory research. *Journal of Verbal Learning and Verbal Behavior*, 11(6), 671-684.** Memory is a by-product of processing depth; semantic processing yields more durable traces than surface processing.
- *Connection*: a higher-level summary is a *deeper*, more semantic encoding of the constituent paragraphs. The architecture forces both system and users through a depth ladder rather than letting them stay at surface OCR.

### Cognitive maps / hippocampal navigation
- **Tolman, E. C. (1948). Cognitive maps in rats and men. *Psychological Review*, 55(4), 189-208.** Animals navigate via internal map-like representations, not stimulus-response chains.
- **O'Keefe, J., & Nadel, L. (1978). *The Hippocampus as a Cognitive Map*. Oxford University Press.** Maps the Tolman idea onto hippocampal place cells.
- **Eichenbaum, H. (2017). The role of the hippocampus in navigation is memory. *Journal of Neurophysiology*, 117(4), 1785-1796.** The "map" generalises from physical space to relational memory more broadly.
- *Connection*: a historical archive is non-spatial cognitive territory. Mausoleo's hierarchy gives users grid-like waypoints (Decade, Year, Month) that mirror the relational structure the hippocampus would otherwise have to construct from scratch.

### Schema theory / mental models
- **Bartlett, F. C. (1932). *Remembering: A Study in Experimental and Social Psychology*. Cambridge University Press.** Classic source for schemas as top-down structures organising recall.
- **Johnson-Laird, P. N. (1983). *Mental Models*. Harvard University Press.** Reasoning works on internal models, not isolated propositions.
- *Connection*: a historian approaching 1943 already has a "wartime Rome" schema; Mausoleo's higher-level summaries can confirm, extend, or productively violate it - schema theory predicts improved memory for the underlying articles.

### Categorisation and abstraction
- **Rosch, E. (1978). Principles of categorization.** In Rosch & Lloyd (Eds.), *Cognition and Categorization*, 27-48. Lawrence Erlbaum. Basic-level categories: a privileged level of abstraction at which the cognitive system naturally operates.
- **Rosch, E., & Mervis, C. B. (1975). Family resemblances. *Cognitive Psychology*, 7(4), 573-605.**
- **Tversky, A. (1977). Features of similarity. *Psychological Review*, 84(4), 327-352.** Similarity is asymmetric, feature-driven.
- *Connection*: each Mausoleo level is a candidate "basic level" - Article for a journalist, Month for an event-historian, Decade for a longue-duree economic historian.

### Distributed cognition / extended mind
- **Hutchins, E. (1995). *Cognition in the Wild*. MIT Press.** Cognition is distributed across people, artefacts, and representations.
- **Clark, A., & Chalmers, D. (1998). The extended mind. *Analysis*, 58(1), 7-19.** Reliable, functionally integrated external structures count as part of the cognitive system.
- *Connection*: Mausoleo is exactly the kind of external scaffold these papers describe - a persistent, reliably accessed structure that off-loads chunking, categorisation, and abstraction.

## Recent literature (2015-2024)

- **Clark, A. (2016). *Surfing Uncertainty: Prediction, Action, and the Embodied Mind*. Oxford University Press.** Book-length synthesis of predictive processing; a single citable post-2015 source for the framework.
- **Behrens, T. E. J., Muller, T. H., Whittington, J. C. R., et al. (2018). What is a cognitive map? Organizing knowledge for flexible behavior. *Neuron*, 100(2), 490-509.** Hippocampal-entorhinal map mechanisms organise abstract, non-spatial knowledge of all kinds.
- **Whittington, J. C. R., Muller, T. H., Mark, S., Chen, G., Barry, C., Burgess, N., & Behrens, T. E. J. (2020). The Tolman-Eichenbaum machine: unifying space and relational memory through generalization in the hippocampal formation. *Cell*, 183(5), 1249-1263.** Computational model: same machinery learns spatial maps and relational knowledge graphs.
- **van Kesteren, M. T. R., Ruiter, D. J., Fernandez, G., & Henson, R. N. (2012). How schema and novelty augment memory formation. *Trends in Neurosciences*, 35(4), 211-219.** Schema-congruent information consolidates more rapidly via medial prefrontal cortex.
- **Alonso, A., van der Meij, J., Tse, D., & Genzel, L. (2020). Naive to expert: considering the role of previous knowledge in memory. *Brain and Neuroscience Advances*, 4.** Recent review on prior-knowledge effects on encoding. [verify volume / page]
- **Cowan, N. (2010). The magical mystery four. *Current Directions in Psychological Science*, 19(1), 51-57.** Accessible update of the chunking thesis.
- **Lake, B. M., Ullman, T. D., Tenenbaum, J. B., & Gershman, S. J. (2017). Building machines that learn and think like people. *Behavioral and Brain Sciences*, 40, e253.** Hierarchical, structured representations as a prerequisite for human-like generalisation.
- **Ullman, T. D., & Tenenbaum, J. B. (2020). Bayesian models of conceptual development. *Annual Review of Developmental Psychology*, 2, 533-558.** Hierarchical Bayesian inference produces human-like learning where higher-level abstractions can be acquired from sparse data.

These recent sources directly bridge cogsci to the LLM-summary techniques Mausoleo uses to produce its hierarchy: hierarchical attention is a rough computational analogue of cortical hierarchy.

## Key arguments to deploy in the dissertation

1. **Natural-format argument.** Friston/Clark + Behrens + Cowan: the brain's machinery is hierarchical and chunked, so a hierarchical chunked index lowers cognitive load relative to flat search - converting hierarchy from aesthetic preference into a measurable HCI claim.
2. **Schema-acceleration argument.** van Kesteren + Bartlett: pre-existing schemas accelerate consolidation. Mausoleo's high-level summaries are turn-key schemas for an unfamiliar month, predicting faster orientation.
3. **Basic-level argument.** Rosch: there is no single right granularity. Mausoleo's seven levels let users pick their basic level dynamically; flat search forces one (the article).
4. **Extended-mind argument.** Clark & Chalmers + Hutchins: Mausoleo should be evaluated as a cognitive prosthesis, not a database; metrics should include depth-of-comprehension, not only retrieval precision.
5. **Convergence argument.** Whittington et al. + Lake et al.: cortex, hippocampus, and transformer/Bayesian models converge on hierarchical relational representations. Mausoleo's design aligns with three independent lines of cogsci.

## Suggested case-study questions / hypotheses

1. **Schema-orientation hypothesis.** Two groups of historians do a 30-minute task on a random day from Il Messaggero, May 1943. Group A uses Mausoleo; Group B uses flat full-text search over the same OCR. Predict (van Kesteren, Bartlett, Cowan): Group A produces narratives with more cross-article connections, recalls more headlines correctly, and reports lower subjective effort, because Day/Month summaries pre-load a schema before any article-level reading.

2. **Basic-level flexibility hypothesis.** Users with different research questions (event-historian, social-historian, media-studies). Predict (Rosch + Behrens): each user's gaze/click data clusters at a *different* level of the hierarchy - their basic level - and cross-level navigation is smoother than equivalent zoom-in/out behaviour in flat search, evidencing genuine multi-resolution use.
