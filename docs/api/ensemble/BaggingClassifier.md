# BaggingClassifier

Online bootstrap aggregation for classification.

For each incoming observation, each model's `learn_one` method is called `k` times where `k` is sampled from a Poisson distribution of parameter 1. `k` thus has a 36% chance of being equal to 0, a 36% chance of being equal to 1, an 18% chance of being equal to 2, a 6% chance of being equal to 3, a 1% chance of being equal to 4, etc. You can do `scipy.stats.poisson(1).pmf(k)` to obtain more detailed values.

## Parameters

- **model** (*[base.Classifier](../../base/Classifier)*)

    The classifier to bag.

- **n_models** – defaults to `10`

    The number of models in the ensemble.

- **seed** (*int*) – defaults to `None`

    Random number generator seed for reproducibility.



## Examples

In the following example three logistic regressions are bagged together. The performance is
slightly better than when using a single logistic regression.

```python
>>> from river import datasets
>>> from river import ensemble
>>> from river import evaluate
>>> from river import linear_model
>>> from river import metrics
>>> from river import optim
>>> from river import preprocessing

>>> dataset = datasets.Phishing()

>>> model = ensemble.BaggingClassifier(
...     model=(
...         preprocessing.StandardScaler() |
...         linear_model.LogisticRegression()
...     ),
...     n_models=3,
...     seed=42
... )

>>> metric = metrics.F1()

>>> evaluate.progressive_val_score(dataset, model, metric)
F1: 0.877788

>>> print(model)
BaggingClassifier(StandardScaler | LogisticRegression)
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

    Averages the predictions of each classifier.

    **Parameters**

    - **x**    
    
## References

[^1]: [Oza, N.C., 2005, October. Online bagging and boosting. In 2005 IEEE international conference on systems, man and cybernetics (Vol. 3, pp. 2340-2345). Ieee.](https://ti.arc.nasa.gov/m/profile/oza/files/ozru01a.pdf)

