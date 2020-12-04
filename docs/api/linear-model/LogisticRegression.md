# LogisticRegression

Logistic regression.

This estimator supports learning with mini-batches. On top of the single instance methods, it provides the following methods: `learn_many`, `predict_many`, `predict_proba_many`. Each method takes as input a `pandas.DataFrame` where each column represents a feature. 

It is generally a good idea to scale the data beforehand in order for the optimizer to converge. You can do this online with a `preprocessing.StandardScaler`.

## Parameters

- **optimizer** (*[optim.Optimizer](../../optim/Optimizer)*) – defaults to `None`

    The sequential optimizer used for updating the weights. Note that the intercept is handled separately.

- **loss** (*[optim.losses.BinaryLoss](../../optim/losses/BinaryLoss)*) – defaults to `None`

    The loss function to optimize for. Defaults to `optim.losses.Log`.

- **l2** – defaults to `0.0`

    Amount of L2 regularization used to push weights towards 0.

- **intercept_init** – defaults to `0.0`

    Initial intercept value.

- **intercept_lr** (*Union[float, [optim.schedulers.Scheduler](../../optim/schedulers/Scheduler)]*) – defaults to `0.01`

    Learning rate scheduler used for updating the intercept. A `optim.schedulers.Constant` is used if a `float` is provided. The intercept is not updated when this is set to 0.

- **clip_gradient** – defaults to `1000000000000.0`

    Clips the absolute value of each gradient value.

- **initializer** (*[optim.initializers.Initializer](../../optim/initializers/Initializer)*) – defaults to `None`

    Weights initialization scheme.


## Attributes

- **weights**

    The current weights.


## Examples

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import linear_model
>>> from river import metrics
>>> from river import optim
>>> from river import preprocessing

>>> dataset = datasets.Phishing()

>>> model = (
...     preprocessing.StandardScaler() |
...     linear_model.LogisticRegression(optimizer=optim.SGD(.1))
... )

>>> metric = metrics.Accuracy()

>>> evaluate.progressive_val_score(dataset, model, metric)
Accuracy: 88.96%
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_many"

    Update the model with a mini-batch of features `X` and boolean targets `y`.

    **Parameters**

    - **X**     (*pandas.core.frame.DataFrame*)    
    - **y**     (*pandas.core.series.Series*)    
    - **w**     (*Union[float, pandas.core.series.Series]*)     – defaults to `1`    
    
    **Returns**

    *MiniBatchClassifier*:     self
    
???- note "learn_one"

    Update the model with a set of features `x` and a label `y`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*Union[bool, str, int]*)    
    - **w**     – defaults to `1.0`    
    
    **Returns**

    *Classifier*:     self
    
???- note "predict_many"

    Predict the outcome for each given sample.

    Parameters --------- X     A dataframe of features.

    **Parameters**

    - **X**     (*pandas.core.frame.DataFrame*)    
    
    **Returns**

    *Series*:     The predicted labels.
    
???- note "predict_one"

    Predict the label of a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Union[bool, str, int]*:     The predicted label.
    
???- note "predict_proba_many"

    Predict the outcome probabilities for each given sample.

    **Parameters**

    - **X**     (*pandas.core.frame.DataFrame*)    
    
    **Returns**

    *DataFrame*:     A dataframe with probabilities of `True` and `False` for each sample.
    
???- note "predict_proba_one"

    Predict the probability of each label for a dictionary of features `x`.

    **Parameters**

    - **x**    
    
    **Returns**

    A dictionary that associates a probability which each label.
    
