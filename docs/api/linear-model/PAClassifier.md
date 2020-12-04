# PAClassifier

Passive-aggressive learning for classification.



## Parameters

- **C** – defaults to `1.0`

- **mode** – defaults to `1`

- **learn_intercept** – defaults to `True`



## Examples

The following example is taken from [this blog post](https://www.bonaccorso.eu/2017/10/06/ml-algorithms-addendum-passive-aggressive-algorithms/).

```python
>>> from river import linear_model
>>> from river import metrics
>>> from river import stream
>>> import numpy as np
>>> from sklearn import datasets
>>> from sklearn import model_selection

>>> np.random.seed(1000)
>>> X, y = datasets.make_classification(
...     n_samples=5000,
...     n_features=4,
...     n_informative=2,
...     n_redundant=0,
...     n_repeated=0,
...     n_classes=2,
...     n_clusters_per_class=2
... )

>>> X_train, X_test, y_train, y_test = model_selection.train_test_split(
...     X,
...     y,
...     test_size=0.35,
...     random_state=1000
... )

>>> model = linear_model.PAClassifier(
...     C=0.01,
...     mode=1
... )

>>> for xi, yi in stream.iter_array(X_train, y_train):
...     y_pred = model.learn_one(xi, yi)

>>> metric = metrics.Accuracy() + metrics.LogLoss()

>>> for xi, yi in stream.iter_array(X_test, y_test):
...     metric = metric.update(yi, model.predict_proba_one(xi))

>>> print(metric)
Accuracy: 88.46%, LogLoss: 0.325727
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

[^1]: [Crammer, K., Dekel, O., Keshet, J., Shalev-Shwartz, S. and Singer, Y., 2006. Online passive-aggressive algorithms. Journal of Machine Learning Research, 7(Mar), pp.551-585](http://jmlr.csail.mit.edu/papers/volume7/crammer06a/crammer06a.pdf)

