# LinearRegression

Linear regression.

This estimator supports learning with mini-batches. On top of the single instance methods, it provides the following methods: `learn_many`, `predict_many`, `predict_proba_many`. Each method takes as input a `pandas.DataFrame` where each column represents a feature. 

It is generally a good idea to scale the data beforehand in order for the optimizer to converge. You can do this online with a `preprocessing.StandardScaler`.

## Parameters

- **optimizer** (*[optim.Optimizer](../../optim/Optimizer)*) – defaults to `None`

    The sequential optimizer used for updating the weights. Note that the intercept updates are handled separately.

- **loss** (*[optim.losses.RegressionLoss](../../optim/losses/RegressionLoss)*) – defaults to `None`

    The loss function to optimize for.

- **l2** – defaults to `0.0`

    Amount of L2 regularization used to push weights towards 0.

- **intercept_init** – defaults to `0.0`

    Initial intercept value.

- **intercept_lr** (*Union[[optim.schedulers.Scheduler](../../optim/schedulers/Scheduler), float]*) – defaults to `0.01`

    Learning rate scheduler used for updating the intercept. A `optim.schedulers.Constant` is used if a `float` is provided. The intercept is not updated when this is set to 0.

- **clip_gradient** – defaults to `1000000000000.0`

    Clips the absolute value of each gradient value.

- **initializer** (*[optim.initializers.Initializer](../../optim/initializers/Initializer)*) – defaults to `None`

    Weights initialization scheme.


## Attributes

- **weights** (*dict*)

    The current weights.


## Examples

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import linear_model
>>> from river import metrics
>>> from river import preprocessing

>>> dataset = datasets.TrumpApproval()

>>> model = (
...     preprocessing.StandardScaler() |
...     linear_model.LinearRegression(intercept_lr=.1)
... )
>>> metric = metrics.MAE()

>>> evaluate.progressive_val_score(dataset, model, metric)
MAE: 0.555971

>>> model['LinearRegression'].intercept
35.617670

```

You can call the `debug_one` method to break down a prediction. This works even if the
linear regression is part of a pipeline.

```python
>>> x, y = next(iter(dataset))
>>> report = model.debug_one(x)
>>> print(report)
0. Input
--------
gallup: 43.84321 (float)
ipsos: 46.19925 (float)
morning_consult: 48.31875 (float)
ordinal_date: 736389 (int)
rasmussen: 44.10469 (float)
you_gov: 43.63691 (float)
<BLANKLINE>
1. StandardScaler
-----------------
gallup: 1.18810 (float)
ipsos: 2.10348 (float)
morning_consult: 2.73545 (float)
ordinal_date: -1.73032 (float)
rasmussen: 1.26872 (float)
you_gov: 1.48391 (float)
<BLANKLINE>
2. LinearRegression
-------------------
Name              Value      Weight      Contribution
      Intercept    1.00000    35.61767       35.61767
          ipsos    2.10348     0.62689        1.31866
morning_consult    2.73545     0.24180        0.66144
         gallup    1.18810     0.43568        0.51764
      rasmussen    1.26872     0.28118        0.35674
        you_gov    1.48391     0.03123        0.04634
   ordinal_date   -1.73032     3.45162       -5.97242
<BLANKLINE>
Prediction: 32.54607
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "debug_one"

    Debugs the output of the linear regression.

    **Parameters**

    - **x**     (*dict*)    
    - **decimals**     – defaults to `5`    
    
    **Returns**

    *str*:     A table which explains the output.
    
???- note "learn_many"

    Update the model with a mini-batch of features `X` and boolean targets `y`.

    **Parameters**

    - **X**     (*pandas.core.frame.DataFrame*)    
    - **y**     (*pandas.core.series.Series*)    
    - **w**     (*Union[float, pandas.core.series.Series]*)     – defaults to `1`    
    
    **Returns**

    *MiniBatchRegressor*:     self
    
???- note "learn_one"

    Fits to a set of features `x` and a real-valued target `y`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*numbers.Number*)    
    - **w**     – defaults to `1.0`    
    
    **Returns**

    *Regressor*:     self
    
???- note "predict_many"

    Predict the outcome for each given sample.

    Parameters --------- X     A dataframe of features.

    **Parameters**

    - **X**    
    
    **Returns**

    The predicted outcomes.
    
???- note "predict_one"

    Predicts the target value of a set of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    The prediction.
    
