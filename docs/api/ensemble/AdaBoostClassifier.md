# AdaBoostClassifier

Boosting for classification

For each incoming observation, each model's `learn_one` method is called `k` times where `k` is sampled from a Poisson distribution of parameter lambda. The lambda parameter is updated when the weaks learners fit successively the same observation.

## Parameters

- **model** (*[base.Classifier](../../base/Classifier)*)

    The classifier to boost.

- **n_models** – defaults to `10`

    The number of models in the ensemble.

- **seed** (*int*) – defaults to `None`

    Random number generator seed for reproducibility.


## Attributes

- **wrong_weight** (*collections.defaultdict*)

    Number of times a model has made a mistake when making predictions.

- **correct_weight** (*collections.defaultdict*)

    Number of times a model has predicted the right label when making predictions.


## Examples

In the following example three tree classifiers are boosted together. The performance is
slightly better than when using a single tree.

```python
>>> from river import datasets
>>> from river import ensemble
>>> from river import evaluate
>>> from river import metrics
>>> from river import tree

>>> dataset = datasets.Phishing()

>>> metric = metrics.LogLoss()

>>> model = ensemble.AdaBoostClassifier(
...     model=(
...         tree.HoeffdingTreeClassifier(
...             split_criterion='gini',
...             split_confidence=1e-5,
...             grace_period=2000
...         )
...     ),
...     n_models=5,
...     seed=42
... )

>>> evaluate.progressive_val_score(dataset, model, metric)
LogLoss: 0.37111

>>> print(model)
AdaBoostClassifier(HoeffdingTreeClassifier)
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update the model with a set of features `x` and a label `y`.

    **Parameters**

    - **x**    
    - **y**    
    
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
    
## References

[^1]: [Oza, N.C., 2005, October. Online bagging and boosting. In 2005 IEEE international conference on systems, man and cybernetics (Vol. 3, pp. 2340-2345). Ieee.](https://ti.arc.nasa.gov/m/profile/oza/files/ozru01a.pdf)

