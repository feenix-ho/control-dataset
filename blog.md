# Control Dataset for "Learning Optimal Conformal Classifiers"

The generation code and the dataset are available on Github [here]().

## Why this control dataset is a precise test of the paper's claim

Paper's focal claim

> Conformal Training (ConfTr) learns to shrink the average size of the prediction set ("inefficiency")—while keeping the formal coverage guarantee—compared with a vanilla cross-entropy network that is wrapped with Conformal Prediction only after training.

Property we must isolate

> Does training through the conformal wrapper actually help in regions of genuine class overlap, or is any observed gain just a side-effect of lucky class priors or easy points?

## How the toy dataset targets that property

| Experimental need                                                                | Design choice                                                                  | Rationale                                                                                                                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Non-trivial ambiguity zone** where a point can plausibly belong to 2-3 classes | Five 2-D Gaussians whose tails overlap in a large "doughnut" around the origin | Forces the conformal set to contain multiple labels whenever a point lands in the shared density region—exactly where inefficiency matters                                                     |
| **Clear low-ambiguity zones** near each mean                                     | Well-separated centres on a regular pentagon, radius = 4                       | Allows us to verify that both ConfTr and the baseline collapse to single-label sets when the class is obvious; any inefficiency reduction must therefore come from handling the overlap better |
| **Uniform class priors**                                                         | Equal number of samples per class                                              | Removes "lucky class-imbalance" as an explanation for smaller sets                                                                                                                             |
| **Full control & reproducibility**                                               | Purely synthetic generator with fixed seed                                     | Lets us repeat the test under different overlaps (tune _σ_) or number of classes without changing any other factor                                                                             |

Because we **know** which regions are ambiguous and which are not, we can cleanly attribute any drop in average set size to how each method treats the ambiguous ring—exactly the mechanism the paper claims to improve.
