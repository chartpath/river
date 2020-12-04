# EWARegressor

Exponentially Weighted Average regressor.



## Parameters

- **regressors** (*List[[base.Regressor](../../base/Regressor)]*)

    The regressors to hedge.

- **loss** (*[optim.losses.RegressionLoss](../../optim/losses/RegressionLoss)*) – defaults to `None`

    The loss function that has to be minimized. Defaults to `optim.losses.Squared`.

- **learning_rate** – defaults to `0.5`

    The learning rate by which the model weights are multiplied at each iteration.


## Attributes

- **regressors**


## Examples

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import expert
>>> from river import linear_model
>>> from river import metrics
>>> from river import optim
>>> from river import preprocessing
>>> from river import stream

>>> optimizers = [
...     optim.SGD(0.01),
...     optim.RMSProp(),
...     optim.AdaGrad()
... ]

>>> for optimizer in optimizers:
...
...     dataset = datasets.TrumpApproval()
...     metric = metrics.MAE()
...     model = (
...         preprocessing.StandardScaler() |
...         linear_model.LinearRegression(
...             optimizer=optimizer,
...             intercept_lr=.1
...         )
...     )
...
...     print(optimizer, evaluate.progressive_val_score(dataset, model, metric))
SGD MAE: 0.555971
RMSProp MAE: 0.528284
AdaGrad MAE: 0.481461

>>> dataset = datasets.TrumpApproval()
>>> metric = metrics.MAE()
>>> hedge = (
...     preprocessing.StandardScaler() |
...     expert.EWARegressor(
...         regressors=[
...             linear_model.LinearRegression(optimizer=o, intercept_lr=.1)
...             for o in optimizers
...         ],
...         learning_rate=0.005
...     )
... )

>>> evaluate.progressive_val_score(dataset, hedge, metric)
MAE: 0.494832
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
    
???- note "learn_predict_one"

???- note "predict_one"

    Predicts the target value of a set of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    The prediction.
    
## References

[^1]: [Online Learning from Experts: Weighed Majority and Hedge](https://www.shivani-agarwal.net/Teaching/E0370/Aug-2011/Lectures/20-scribe1.pdf)
[^2]: [Wikipedia page on the multiplicative weight update method](https://www.wikiwand.com/en/Multiplicative_weight_update_method)
[^3]: [Kivinen, J. and Warmuth, M.K., 1997. Exponentiated gradient versus gradient descent for linear predictors. information and computation, 132(1), pp.1-63.](https://users.soe.ucsc.edu/~manfred/pubs/J36.pdf)

