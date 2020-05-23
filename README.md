# Reproducibility Basics

* __Repeatable__ analysis workflow can be repeated exactly with identical outcome.
* __Reusable__ analysis workflow can be adopted to contibute to another workflow.
* __Reproducible__ analysis workflow can be reproduced with compatible results, but not necessarily with an identical workflow.
  * __Generally Reproducible__ analysis can be reproduced with multiple workflows. 


*Generally Reproducible analysis implies existence of objective (or at least common, shared) knowledge, which can be reached with different paths. In this sense, general reproducibility is more valuable but more vague than simple repeatablility.*


Every repeatable workflow is stricktly reproducible, but the opposite is not necessarily true.

Not every repeatable (and stricktly reproducible) analysis is generally reproducible.

Triviarily repeatable analysis may, for example, output verbatim the required result. Clearly, this does not ensure any property of the analysis. Hence requirement of repeatable (or stricktly reproducible) analysis is not on it's own useful.

Reusability benefits from substantially structuring the analysis, incorporating many common analysis workflows.

Reusable (and especially substantially structured) analysis can be easily modified to produce an alternative but compatible workflows.

Hence, reproducibility of the analysis can be faciliated by making the analysis reusable and especially substantially structured.

*Repeatable analyses can be often easily adopted to ensure reproducibility. For example in ODA, substituting OSA version yields a new analysis, reproducing (or not) the original result.*

Use of results of non-repeatable analyses implies trust in coherence of the analysis provider. It's inevitable that non-repeatable processes will be present in the general scientific workflow. 

## Implementation

An analysis can be represented as set of relations. An example of prototype complete cycle is implemented in ODA self-test (introspection) engine.

https://github.com/volodymyrss/oda-tests

https://github.com/volodymyrss/literature-to-facts
