# AdaptiveRandomForestClassifier

Adaptive Random Forest classifier.

The 3 most important aspects of Adaptive Random Forest [^1] are: 

1. inducing diversity through re-sampling 

2. inducing diversity through randomly selecting subsets of features for    node splits 

3. drift detectors per base tree, which cause selective resets in response    to drifts 

It also allows training background trees, which start training if a warning is detected and replace the active tree if the warning escalates to a drift.

## Parameters

- **n_models** (*int*) – defaults to `10`

    Number of trees in the ensemble.

- **max_features** (*Union[bool, str, int]*) – defaults to `sqrt`

    Max number of attributes for each node split.<br/> - If `int`, then consider `max_features` at each split.<br/> - If `float`, then `max_features` is a percentage and   `int(max_features * n_features)` features are considered per split.<br/> - If "sqrt", then `max_features=sqrt(n_features)`.<br/> - If "log2", then `max_features=log2(n_features)`.<br/> - If None, then ``max_features=n_features``.

- **lambda_value** (*int*) – defaults to `6`

    The lambda value for bagging (lambda=6 corresponds to Leveraging Bagging).

- **metric** (*river.metrics.base.MultiClassMetric*) – defaults to `Accuracy: 0.00%`

    Metric used to track trees performance within the ensemble.

- **disable_weighted_vote** – defaults to `False`

    If `True`, disables the weighted vote prediction.

- **drift_detector** (*Union[[base.DriftDetector](../../base/DriftDetector), NoneType]*) – defaults to `ADWIN`

    Drift Detection method. Set to None to disable Drift detection.

- **warning_detector** (*Union[[base.DriftDetector](../../base/DriftDetector), NoneType]*) – defaults to `ADWIN`

    Warning Detection method. Set to None to disable warning detection.

- **max_size** (*int*) – defaults to `32`

    [*Tree parameter*] Maximum memory (MB) consumed by the tree.

- **memory_estimate_period** (*int*) – defaults to `2000000`

    [*Tree parameter*] Number of instances between memory consumption checks.

- **grace_period** (*int*) – defaults to `50`

    [*Tree parameter*] Number of instances a leaf should observe between split attempts.

- **split_criterion** (*str*) – defaults to `info_gain`

    [*Tree parameter*] Split criterion to use.<br/> - 'gini' - Gini<br/> - 'info_gain' - Information Gain<br/> - 'hellinger' - Hellinger Distance

- **split_confidence** (*float*) – defaults to `0.01`

    [*Tree parameter*] Allowed error in split decision, a value closer to 0 takes longer to decide.

- **tie_threshold** (*float*) – defaults to `0.05`

    [*Tree parameter*] Threshold below which a split will be forced to break ties.

- **binary_split** – defaults to `False`

    [*Tree parameter*] If True, only allow binary splits.

- **stop_mem_management** – defaults to `False`

    [*Tree parameter*] If True, stop growing as soon as memory limit is hit.

- **remove_poor_attrs** – defaults to `False`

    [*Tree parameter*] If True, disable poor attributes.

- **merit_preprune** – defaults to `True`

    [*Tree parameter*] If True, disable pre-pruning.

- **leaf_prediction** (*str*) – defaults to `nba`

    [*Tree parameter*] Prediction mechanism used at leafs.<br/> - 'mc' - Majority Class<br/> - 'nb' - Naive Bayes<br/> - 'nba' - Naive Bayes Adaptive

- **nb_threshold** (*int*) – defaults to `0`

    [*Tree parameter*] Number of instances a leaf should observe before allowing Naive Bayes.

- **nominal_attributes** (*list*) – defaults to `None`

    [*Tree parameter*] List of Nominal attributes. If empty, then assume that all attributes are numerical.

- **attr_obs** (*str*) – defaults to `gaussian`

    [*Tree parameter*] The Attribute Observer (AO) used to monitor the class statistics of numeric features and perform splits. Parameters can be passed to the AOs (when supported) by using `attr_obs_params`. Valid options are:</br> - `'bst'`: Binary Search Tree.</br> - `'gaussian'`: Gaussian observer. The `n_splits` used to query  for split candidates can be adjusted (defaults to `10`).</br> - `'histogram'`: Histogram-based class frequency estimation.  The number of histogram bins (`n_bins` -- defaults to `256`) and the number of split point candidates to evaluate (`n_splits` -- defaults to `32`) can be adjusted.</br> See 'Notes' for more information about the AOs.

- **attr_obs_params** (*dict*) – defaults to `None`

    [*Tree parameter*] Parameters passed to the numeric AOs. See `attr_obs` for more information.

- **max_depth** (*int*) – defaults to `None`

    [*Tree parameter*] The maximum depth a tree can reach. If `None`, the tree will grow indefinitely.

- **seed** – defaults to `None`

    If `int`, `seed` is used to seed the random number generator; If `RandomState`, `seed` is the random number generator; If `None`, the random number generator is the `RandomState` instance used by `np.random`.



## Examples

```python
>>> from river import synth
>>> from river import ensemble
>>> from river import evaluate
>>> from river import metrics

>>> dataset = synth.ConceptDriftStream(seed=42, position=500,
...                                    width=40).take(1000)

>>> model = ensemble.AdaptiveRandomForestClassifier(
...     n_models=3,
...     seed=42
... )

>>> metric = metrics.Accuracy()

>>> evaluate.progressive_val_score(dataset, model, metric)
Accuracy: 72.87%
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

???- note "predict_one"

    Predict the label of a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Union[bool, str, int]*:     The predicted label.
    
???- note "predict_proba_one"

    Predict the probability of each label for a dictionary of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Dict[typing.Union[bool, str, int], float]*:     A dictionary that associates a probability which each label.
    
???- note "reset"

    Reset the forest.

    
## Notes

Hoeffding trees rely on Attribute Observer (AO) algorithms to monitor input features
and perform splits. Nominal features can be easily dealt with, since the partitions
are well-defined. Numerical features, however, require more sophisticated solutions.
Currently, three AOs are supported in `river` for classification trees:

- *Binary Search Tree (BST)*: uses an exhaustive algorithm to find split candidates,
similarly to batch decision trees. It ends up storing all observations between split
attempts. This AO is the most costly one in terms of memory and processing
time; however, it tends to yield the most accurate results when using `leaf_prediction=mc`.
It cannot be used to calculate the Probability Density Function (PDF) of the monitored
feature due to its binary tree nature. Hence, leaf prediction strategies other than
the majority class will end up effectively mimicing the majority class classifier.
This AO has no parameters.</br>
- *Gaussian Estimator*: Approximates the numeric feature distribution by using
a Gaussian distribution per class. The Cumulative Distribution Function (CDF) necessary to
calculate the entropy (and, consequently, the information gain), the gini index, and
other split criteria is then calculated using the fit feature's distribution.</br>
- *Histogram*: approximates the numeric feature distribution using an incrementally
maintained histogram per class. It represents a compromise between the intensive
resource usage of BST and the strong assumptions about the feature's distribution
used in the Gaussian Estimator. Besides that, this AO sits in the middle between the
previous two in terms of memory usage and running time. Note that the number of
bins affects the probability density approximation required to use leaves with
(adaptive) naive bayes models. Hence, Histogram tends to be less accurate than the
Gaussian estimator when adaptive or naive bayes leaves are used.

## References

[^1]: Heitor Murilo Gomes, Albert Bifet, Jesse Read, Jean Paul Barddal,
     Fabricio Enembreck, Bernhard Pfharinger, Geoff Holmes, Talel Abdessalem.
     Adaptive random forests for evolving data stream classification.
     In Machine Learning, DOI: 10.1007/s10994-017-5642-8, Springer, 2017.

