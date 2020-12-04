# BoxCoxRegressor

Applies the Box-Cox transform to the target before training.

Box-Cox transform is useful when the target variable is heteroscedastic (i.e. there are sub-populations that have different variabilities from others) allowing to transform it towards normality. 

The `power` parameter is denoted λ in the literature. If `power` is equal to 0 than the Box-Cox transform will be equivalent to a log transform.

## Parameters

- **regressor** (*[base.Regressor](../../base/Regressor)*)

    Regression model to wrap.

- **power** – defaults to `1.0`

    power value to do the transformation.



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
...     meta.BoxCoxRegressor(
...         regressor=linear_model.LinearRegression(intercept_lr=0.2),
...         power=0.05
...     )
... )
>>> metric = metrics.MSE()

>>> evaluate.progressive_val_score(dataset, model, metric)
MSE: 5.898196
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
    
