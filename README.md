# Why?

In [FAIR principles](https://www.go-fair.org/fair-principles/), "R" stands for Reusable. On the other hand, [reproducibility (or replication) crisis](https://en.wikipedia.org/wiki/Replication_crisis) refers to reproducibility or replication. But what do these terms mean? What do they imply? What is required to make them work?

# Reproducible/Reusable/Repeatable/Replicable

* __Repeatable__ analysis workflow can be repeated exactly with identical outcome.
* __Reusable__ analysis workflow can be adopted to contibute to another workflow.
* __Reproducible__ analysis workflow can be reproduced with compatible results, but not necessarily with an identical workflow.
* __Replicable__ analysis is rather ambigious and is often used as synonym to **reproducible**

None of these terms as described above are directly informing about. So we also can point out a need for another term:

* __Generally Reproducible__ analysis can be reproduced ("verified") with multiple independent workflows

**Reproducible** is probably often used in the meaning of **Generally Reproducible**.


*Generally Reproducible analysis implies existence of objective (or at least common, collective, shared) knowledge, which can be reached with different paths. In this sense, general reproducibility is more valuable but more vague than simple repeatablility.*

We can point out the following:

1. Every repeatable workflow is strictly reproducible, but not every reproducible analysis can be repeated exactly.
1. Not every repeatable (and strictly reproducible) analysis is generally reproducible.
1. Triviarily repeatable analysis may, for example, output verbatim the required result. Clearly, this does not ensure any property of the analysis. Hence requirement of repeatable (or strictly reproducible) analysis is not on it's own useful.
1. In a very strict sense, no workflow can be reproduced exactly, since every new execution is at new point of time, in a new platform. This is not just of a theoretical concern - issues with computing happen, and data corruption can make any analysis deviate from it's expected outcome, even if it's meant to be deterministic. Provenance tracking ensures that every conrete computation is distingiushed.
1. **Generally reproducible result can be made of non-repeatable workflows, but it is benefitial to make every workflow repeatable and assemble them into a generally reproducible workflow**
1. Reusability benefits from substantially structuring the analysis, incorporating common analysis workflows.
1. Reusable (and especially substantially structured) analysis can be easily modified to produce an alternative but compatible workflows.
1. Hence, reproducibility of the analysis can be faciliated by making the analysis reusable and especially substantially structured.

*Repeatable analyses can be often easily adopted to ensure reproducibility. For example in ODA, substituting OSA version yields a new analysis, reproducing (or not) the original result.*

Use of results of non-repeatable analyses implies trust in coherence of the analysis provider. It's inevitable that non-repeatable processes will be present in the general scientific workflow. 

## Example

It's notable that general scientists are interested in scientific statements, like:

```
3 - 10 keV flux of 3C 273 in 2020-01-01 - 2020-01-02 is 1e-4 erg/cm2/s
```

Only more concrete forms of this statement can be computed, for example: 

```
3 - 10 keV flux of 3C 273 in INTEGRAL JEM-X pointings XXX,XXX,XXX is 1e-4 erg/cm2/s 
assuming powerlaw spectral model
all sources from INTREFCAT43 brighter than Crab
gain calibration XX, OSA version YY, archive revision 3, 
computed on MMODA 22.06.0000, backend on Baobab cluster, compiled AMD64, during the heatwave of June 2022 (etc)
```

One can imagine other, specialized, reified, possibilities of the aforementioned statement.

It is important that much of these further details do not affect the "scientific statement", for example neither the OSA version or weather should affect the flux.

# Data Tracking by its Provenance

Provenance describes every step that lead to Data production: every one of more Raw Data forms, every workflow as it was applied.
If the workflows referred in the Provenance are not Repeatable, the same Provenance will be generated for different Data.

Since Provenance describes every operation on the Data, it is in principle sufficient to repeat the data production, as long as the workflows involved are repeatable.

Even though Provenance is the most detailed way to describe Data origin, non-Repeatable workflows make it impossible to use Provenance to understand why some data are different from other, and reproduce each of the versions.



*Notably, the detailed Provenance, which is similar to the reified statement before, is not of a direct interest to scientists. Scientists are interested in shortcut, more abstract, low-resolution statements as the "scientific statement" above. It is important to preserve both detailed and (progressively) abstract statements.*

In **ODA**,  we thrive to make every workflow as repeatable as feasible. Every product ODA produces has a reference to workflow computing it, as an URI. Every URI reference to the product can be directly inserted in a publication or a legacy archive, as it is "promised" to be resolvable to the same data.

# Communication: Persistence, Permanence, Preservation, Provenance

Reproducibility/Repeatability is also crutial when referring to the workflows or data. For example, while **saying** that data from time period 2020-2022 was analysed with pipeline based on OSA11.2 we rely on the fact that this pipeline always returns the same result when applied to this time period.

# On "force recompute"

Sometimes the analyst may desire to "force recompute" the workflow, repeat it again to produce hopefully a different, better result. Indeed, such an approach is occasionally useful in real life, it allows to cirumvent computational incidents and various unfavorable situations which lead to a wrong result, but

**since repeatable analysis always produces the same outcome, it makes no sense to force-recompute it.**

In fact, if the analysis does not produce the same result, there is a deep problem in the workflow management system. Dealing with this sort of problem should not be left to the users, this issue should be tackled by the developers and prevented from happening in the future.

There might be cases when "force recompute" seems to make sense. E.g. when a workflow dealing with streaming data, may be producing "currently available list of observations from the archive" which depends on when it is produced. But instead of accepting an irreproducible workflow in the system (with all the issues it brings) this workflow can be made repeatable (insenstivie to the current time, the archive state) by providing state (version) of the archive as an input to the observation selection workflow.
A difficulty with this approach is that there likely to be many states of the archive which correspond to the same result, and they should not be meaningfully distinguished. This situation can be dealt with the abstraction (de-reification) procedure described above.


# DRAFT: Example Implementation in ODA

An analysis can be represented as set of relations. An example of prototype complete cycle is implemented in ODA self-test (introspection) engine.

https://github.com/volodymyrss/oda-tests

https://github.com/volodymyrss/literature-to-facts
