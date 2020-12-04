# TransformedTargetRegressor

Modifies the target before training.

The user is expected to check that `func` and `inverse_func` are coherent with each other.

## Parameters

- **regressor** (*[base.Regressor](../../base/Regressor)*)

    Regression model to wrap.

- **func** (*<built-in function callable>*)

    A function modifying the target before training.

- **inverse_func** (*<built-in function callable>*)

    A function to return to the target's original space.



## Examples

```python
>>> import math
>>> from river import datasets
>>> from river import evaluate
>>> from river import linear_model
>>> from river import meta
>>> from river import metrics
>>> from river import preprocessing

>>> dataset = datasets.TrumpApproval()
>>> model = (
...     preprocessing.StandardScaler() |
...     meta.TransformedTargetRegressor(
...         regressor=linear_model.LinearRegression(intercept_lr=0.15),
...         func=math.log,
...         inverse_func=math.exp
...     )
... )
>>> metric = metrics.MSE()

>>> evaluate.progressive_val_score(dataset, model, metric)
MSE: 8.759624
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
    
