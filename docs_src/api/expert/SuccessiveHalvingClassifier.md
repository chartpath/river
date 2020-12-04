# SuccessiveHalvingClassifier

Successive halving algorithm for classification.

Successive halving is a method for performing model selection without having to train each model on all the dataset. At certain points in time (called "rungs"), the worst performing will be discarded and the best ones will keep competing between each other. The rung values are designed so that at most `budget` model updates will be performed in total. 

If you have `k` combinations of hyperparameters and that your dataset contains `n` observations, then the maximal budget you can allocate is: 

$$\frac{2kn}{eta}$$ 

It is recommended that you check this beforehand. This bound can't be checked by the function because the size of the dataset is not known. In fact it is potentially infinite, in which case the algorithm will terminate once all the budget has been spent. 

If you have a budget of `B`, and that your dataset contains `n` observations, then the number of hyperparameter combinations that will spend all the budget and go through all the data is: 

$$\ceil(\floor(\frac{B}{(2n)})      imes eta)$$

## Parameters

- **models**

    The models to compare.

- **metric** (*river.metrics.base.Metric*)

    Metric used for comparing models with.

- **budget** (*int*)

    Total number of model updates you wish to allocate.

- **eta** – defaults to `2`

    Rate of elimination. At every rung, `math.ceil(k / eta)` models are kept, where `k` is the number of models that have reached the rung. A higher `eta` value will focus on less models but will allocate more iterations to the best models.

- **verbose** – defaults to `False`

    Whether to display progress or not.

- **print_kwargs**

    Extra keyword arguments are passed to the `print` function. For instance, this allows providing a `file` argument, which indicates where to output progress.


## Attributes

- **best_model**

    The current best model.


## Examples

As an example, let's use successive halving to tune the optimizer of a logistic regression.
We'll first define the model.

```python
>>> from river import linear_model
>>> from river import preprocessing

>>> model = (
...     preprocessing.StandardScaler() |
...     linear_model.LogisticRegression()
... )

```

Let's now define a grid of parameters which we would like to compare. We'll try
different optimizers with various learning rates.

```python
>>> from river import utils
>>> from river import optim

>>> models = utils.expand_param_grid(model, {
...     'LogisticRegression': {
...         'optimizer': [
...             (optim.SGD, {'lr': [.1, .01, .005]}),
...             (optim.Adam, {'beta_1': [.01, .001], 'lr': [.1, .01, .001]}),
...             (optim.Adam, {'beta_1': [.1], 'lr': [.001]}),
...         ]
...     }
... })

```

We can check how many models we've created.

```python
>>> len(models)
10

```

We can now pass these models to a `SuccessiveHalvingClassifier`. We also need to pick a
metric to compare the models, and a budget which indicates how many iterations to run
before picking the best model and discarding the rest.

```python
>>> from river import expert

>>> sh = expert.SuccessiveHalvingClassifier(
...     models=models,
...     metric=metrics.Accuracy(),
...     budget=2000,
...     eta=2,
...     verbose=True
... )

```

A `SuccessiveHalvingClassifier` is also a classifier with a `learn_one` and a
`predict_proba_one` method. We can therefore evaluate it like any other classifier with
`evaluate.progressive_val_score`.

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import metrics

>>> evaluate.progressive_val_score(
...     dataset=datasets.Phishing(),
...     model=sh,
...     metric=metrics.ROCAUC()
... )
[1] 5 removed       5 left  50 iterations   budget used: 500        budget left: 1500       best Accuracy: 80.00%
[2] 2 removed       3 left  100 iterations  budget used: 1000       budget left: 1000       best Accuracy: 84.00%
[3] 1 removed       2 left  166 iterations  budget used: 1498       budget left: 502        best Accuracy: 86.14%
[4] 1 removed       1 left  250 iterations  budget used: 1998       budget left: 2  best Accuracy: 84.80%
ROCAUC: 0.952889

```

We can now view the best model.

```python
>>> sh.best_model
Pipeline (
  StandardScaler (),
  LogisticRegression (
    optimizer=Adam (
      lr=Constant (
        learning_rate=0.01
      )
      beta_1=0.01
      beta_2=0.999
      eps=1e-08
    )
    loss=Log (
      weight_pos=1.
      weight_neg=1.
    )
    l2=0.
    intercept_init=0.
    intercept_lr=Constant (
      learning_rate=0.01
    )
    clip_gradient=1e+12
    initializer=Zeros ()
  )
)
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update the model with a set of features `x` and a label `y`.

    **Parameters**

    - **x**     (*dict*)    
    - **y**     (*Union[bool, str, int]*)    
    
    **Returns**

    *Classifier*:     self
    
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

[^1]: [Jamieson, K. and Talwalkar, A., 2016, May. Non-stochastic best arm identification and hyperparameter optimization. In Artificial Intelligence and Statistics (pp. 240-248).](http://proceedings.mlr.press/v51/jamieson16.pdf)
[^2]: [Li, L., Jamieson, K., Rostamizadeh, A., Gonina, E., Hardt, M., Recht, B. and Talwalkar, A., 2018. Massively parallel hyperparameter tuning. arXiv preprint arXiv:1810.05934.](https://arxiv.org/pdf/1810.05934.pdf)
[^3]: [Li, L., Jamieson, K., DeSalvo, G., Rostamizadeh, A. and Talwalkar, A., 2017. Hyperband: A novel bandit-based approach to hyperparameter optimization. The Journal of Machine Learning Research, 18(1), pp.6765-6816.](https://arxiv.org/pdf/1603.06560.pdf)

