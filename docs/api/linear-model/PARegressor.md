# PARegressor

Passive-aggressive learning for regression.



## Parameters

- **C** – defaults to `1.0`

- **mode** – defaults to `1`

- **eps** – defaults to `0.1`

- **learn_intercept** – defaults to `True`



## Examples

The following example is taken from [this blog post](https://www.bonaccorso.eu/2017/10/06/ml-algorithms-addendum-passive-aggressive-algorithms/).

```python
>>> from river import linear_model
>>> from river import metrics
>>> from river import stream
>>> import numpy as np
>>> from sklearn import datasets

>>> np.random.seed(1000)
>>> X, y = datasets.make_regression(n_samples=500, n_features=4)

>>> model = linear_model.PARegressor(
...     C=0.01,
...     mode=2,
...     eps=0.1,
...     learn_intercept=False
... )
>>> metric = metrics.MAE() + metrics.MSE()

>>> for xi, yi in stream.iter_array(X, y):
...     y_pred = model.predict_one(xi)
...     model = model.learn_one(xi, yi)
...     metric = metric.update(yi, y_pred)

>>> print(metric)
MAE: 9.809402, MSE: 472.393532
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Fits to a set of features `x` and a real-valued target `y`.

    **Parameters**

    - **x**    
    - **y**    
    
    **Returns**

    self
    
???- note "predict_one"

    Predicts the target value of a set of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    The prediction.
    
## References

[^1]: [Crammer, K., Dekel, O., Keshet, J., Shalev-Shwartz, S. and Singer, Y., 2006. Online passive-aggressive algorithms. Journal of Machine Learning Research, 7(Mar), pp.551-585.](http://jmlr.csail.mit.edu/papers/volume7/crammer06a/crammer06a.pdf)

