# PredClipper

Clips the target after predicting.



## Parameters

- **regressor** (*[base.Regressor](../../base/Regressor)*)

    Regressor model for which to clip the predictions.

- **y_min** (*float*)

    minimum value.

- **y_max** (*float*)

    maximum value.



## Examples

```python
>>> from river import linear_model
>>> from river import meta

>>> dataset = (
...     ({'a': 2, 'b': 4}, 80),
...     ({'a': 3, 'b': 5}, 100),
...     ({'a': 4, 'b': 6}, 120)
... )

>>> model = meta.PredClipper(
...     regressor=linear_model.LinearRegression(),
...     y_min=0,
...     y_max=200
... )

>>> for x, y in dataset:
...     _ = model.learn_one(x, y)

>>> model.predict_one({'a': -100, 'b': -200})
0

>>> model.predict_one({'a': 50, 'b': 60})
200
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Fits to a set of features `x` and a real-valued target `y`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*numbers.Number*)    
    
    **Returns**

    *Regressor*:     self
    
???- note "predict_one"

    Predicts the target value of a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *Number*:     The prediction.
    
