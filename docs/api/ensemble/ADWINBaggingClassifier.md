# ADWINBaggingClassifier

ADWIN Bagging classifier.

ADWIN Bagging [^1] is the online bagging method of Oza and Russell [^2] with the addition of the `ADWIN` algorithm as a change detector. If concept drift is detected, the worst member of the ensemble (based on the error estimation by ADWIN) is replaced by a new (empty) classifier.

## Parameters

- **model** (*[base.Classifier](../../base/Classifier)*)

    The classifier to bag.

- **n_models** – defaults to `10`

    The number of models in the ensemble.

- **seed** (*int*) – defaults to `None`

    Random number generator seed for reproducibility.



## Examples

```python
>>> from river import datasets
>>> from river import ensemble
>>> from river import evaluate
>>> from river import linear_model
>>> from river import metrics
>>> from river import optim
>>> from river import preprocessing

>>> dataset = datasets.Phishing()

>>> model = ensemble.ADWINBaggingClassifier(
...     model=(
...         preprocessing.StandardScaler() |
...         linear_model.LogisticRegression()
...     ),
...     n_models=3,
...     seed=42
... )

>>> metric = metrics.F1()

>>> evaluate.progressive_val_score(dataset, model, metric)
F1: 0.878788
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

    Averages the predictions of each classifier.

    **Parameters**

    - **x**    
    
## References

[^1]: Albert Bifet, Geoff Holmes, Bernhard Pfahringer, Richard Kirkby,
and Ricard Gavaldà. "New ensemble methods for evolving data streams."
In 15th ACM SIGKDD International Conference on Knowledge Discovery and
Data Mining, 2009.

[^2]: Oza, N., Russell, S. "Online bagging and boosting."
In: Artificial Intelligence and Statistics 2001, pp. 105–112.
Morgan Kaufmann, 2001.

