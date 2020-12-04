# SRPClassifier

Streaming Random Patches ensemble classifier.

The Streaming Random Patches (SRP) [^1] is an ensemble method that simulates bagging or random subspaces. The default algorithm uses both bagging and random subspaces, namely Random Patches. The default base estimator is a Hoeffding Tree, but other base estimators can be used (differently from random forest variations).

## Parameters

- **model** – defaults to `HoeffdingTreeClassifier`

    The base estimator.

- **n_models** (*int*) – defaults to `100`

    Number of members in the ensemble.

- **subspace_size** (*Union[int, float, str]*) – defaults to `0.6`

    Number of features per subset for each classifier where `M` is the total number of features.<br/> A negative value means `M - subspace_size`.<br/> Only applies when using random subspaces or random patches.<br/> * If `int` indicates the number of features to use. Valid range [2, M]. <br/> * If `float` indicates the percentage of features to use, Valid range (0., 1.]. <br/> * 'sqrt' - `sqrt(M)+1`<br/> * 'rmsqrt' - Residual from `M-(sqrt(M)+1)`

- **training_method** (*str*) – defaults to `patches`

    The training method to use.<br/> * 'subspaces' - Random subspaces.<br/> * 'resampling' - Resampling.<br/> * 'patches' - Random patches.

- **lam** (*float*) – defaults to `6.0`

    Lambda value for resampling.

- **drift_detector** (*Union[[base.DriftDetector](../../base/DriftDetector), NoneType]*) – defaults to `ADWIN`

    Drift detector. If `None`, disables concept drift detection and the background learner.

- **warning_detector** (*[base.DriftDetector](../../base/DriftDetector)*) – defaults to `ADWIN`

    Warning detector. If `None`, disables the background learner and ensemble members are reset if drift is detected.

- **disable_weighted_vote** (*bool*) – defaults to `False`

    If True, disables weighted voting.

- **nominal_attributes** – defaults to `None`

    List of Nominal attributes. If empty, then assumes that all attributes are numerical. Note: Only applies if the base model allows to define the nominal attributes.

- **seed** – defaults to `None`

    If `int`, `seed` is used to seed the random number generator; If `RandomState`, `seed` is the random number generator; If `None`, the random number generator is the `RandomState` instance used by `np.random`.

- **metric** (*river.metrics.base.MultiClassMetric*) – defaults to `Accuracy: 0.00%`

    Metric to track members performance within the ensemble.



## Examples

```python
>>> from river import synth
>>> from river import ensemble
>>> from river import evaluate
>>> from river import metrics

>>> dataset = synth.ConceptDriftStream(seed=42, position=500,
...                                    width=40).take(1000)
>>> model = ensemble.SRPClassifier(
...     n_models=3,
...     seed=42
... )

>>> metric = metrics.Accuracy()

>>> evaluate.progressive_val_score(dataset, model, metric)
Accuracy: 88.69%
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update the model with a set of features `x` and a label `y`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*Union[bool, str, int]*)    
    - **kwargs**    
    
    **Returns**

    self
    
???- note "predict_one"

    Predict the label of a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Union[bool, str, int]*:     The predicted label.
    
???- note "predict_proba_one"

    Predict the probability of each label for a dictionary of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    A dictionary that associates a probability which each label.
    
???- note "reset"

## References

[^1]: Heitor Murilo Gomes, Jesse Read, Albert Bifet.
      Streaming Random Patches for Evolving Data Stream Classification.
      IEEE International Conference on Data Mining (ICDM), 2019.

