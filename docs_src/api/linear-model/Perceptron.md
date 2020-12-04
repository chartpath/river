# Perceptron

Perceptron classifier.

In this implementation, the Perceptron is viewed as a special case of the logistic regression. The loss function that is used is the Hinge loss with a threshold set to 0, whilst the learning rate of the stochastic gradient descent procedure is set to 1 for both the weights and the intercept.

## Parameters

- **l2** – defaults to `0.0`

    Amount of L2 regularization used to push weights towards 0.

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
>>> from river import linear_model as lm
>>> from river import metrics
>>> from river import preprocessing as pp

>>> dataset = datasets.Phishing()

>>> model = pp.StandardScaler() | lm.Perceptron()

>>> metric = metrics.Accuracy()

>>> evaluate.progressive_val_score(dataset, model, metric)
Accuracy: 85.84%
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
    
