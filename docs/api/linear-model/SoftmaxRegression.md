# SoftmaxRegression

Softmax regression is a generalization of logistic regression to multiple classes.

Softmax regression is also known as "multinomial logistic regression". There are a set weights for each class, hence the `weights` attribute is a nested `collections.defaultdict`. The main advantage of using this instead of a one-vs-all logistic regression is that the probabilities will be calibrated. Moreover softmax regression is more robust to outliers.

## Parameters

- **optimizer** (*[optim.Optimizer](../../optim/Optimizer)*) – defaults to `None`

    The sequential optimizer used to tune the weights.

- **loss** (*[optim.losses.MultiClassLoss](../../optim/losses/MultiClassLoss)*) – defaults to `None`

    The loss function to optimize for.

- **l2** – defaults to `0`

    Amount of L2 regularization used to push weights towards 0.


## Attributes

- **weights** (*collections.defaultdict*)


## Examples

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import linear_model
>>> from river import metrics
>>> from river import optim
>>> from river import preprocessing

>>> dataset = datasets.ImageSegments()

>>> model = preprocessing.StandardScaler()
>>> model |= linear_model.SoftmaxRegression()

>>> metric = metrics.MacroF1()

>>> evaluate.progressive_val_score(dataset, model, metric)
MacroF1: 0.818765
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

    - **x**     (*dict*)    
    
    **Returns**

    *typing.Dict[typing.Union[bool, str, int], float]*:     A dictionary that associates a probability which each label.
    
## References

[^1]: [Course on classification stochastic gradient descent](https://www.inf.ed.ac.uk/teaching/courses/mlp/2016/mlp02-sln.pdf)
[^2]: [Binary vs. Multi-Class Logistic Regression](https://chrisyeh96.github.io/2018/06/11/logistic-regression.html)

