# PolynomialExtender

Polynomial feature extender.

Generate features consisting of all polynomial combinations of the features with degree less than or equal to the specified degree. 

Be aware that the number of outputted features scales polynomially in the number of input features and exponentially in the degree. High degrees can cause overfitting.

## Parameters

- **degree** – defaults to `2`

    The maximum degree of the polynomial features.

- **interaction_only** – defaults to `False`

    If `True` then only combinations that include an element at most once will be computed.

- **include_bias** – defaults to `False`

    Whether or not to include a dummy feature which is always equal to 1.

- **bias_name** – defaults to `bias`

    Name to give to the bias feature.



## Examples

```python
>>> from river import feature_extraction as fx

>>> X = [
...     {'x': 0, 'y': 1},
...     {'x': 2, 'y': 3},
...     {'x': 4, 'y': 5}
... ]

>>> poly = fx.PolynomialExtender(degree=2, include_bias=True)
>>> for x in X:
...     print(poly.transform_one(x))
{'x': 0, 'y': 1, 'x*x': 0, 'x*y': 0, 'y*y': 1, 'bias': 1}
{'x': 2, 'y': 3, 'x*x': 4, 'x*y': 6, 'y*y': 9, 'bias': 1}
{'x': 4, 'y': 5, 'x*x': 16, 'x*y': 20, 'y*y': 25, 'bias': 1}

>>> X = [
...     {'x': 0, 'y': 1, 'z': 2},
...     {'x': 2, 'y': 3, 'z': 2},
...     {'x': 4, 'y': 5, 'z': 2}
... ]

>>> poly = fx.PolynomialExtender(degree=3, interaction_only=True)
>>> for x in X:
...     print(poly.transform_one(x))
{'x': 0, 'y': 1, 'z': 2, 'x*y': 0, 'x*z': 0, 'y*z': 2, 'x*y*z': 0}
{'x': 2, 'y': 3, 'z': 2, 'x*y': 6, 'x*z': 4, 'y*z': 6, 'x*y*z': 12}
{'x': 4, 'y': 5, 'z': 2, 'x*y': 20, 'x*z': 8, 'y*z': 10, 'x*y*z': 40}

```

Polynomial features are typically used for a linear model to capture interactions between
features. This may done by setting up a pipeline, as so:

```python
>>> from river import datasets
>>> from river import evaluate
>>> from river import linear_model as lm
>>> from river import metrics
>>> from river import preprocessing as pp

>>> dataset = datasets.Phishing()

>>> model = (
...     fx.PolynomialExtender() |
...     pp.StandardScaler() |
...     lm.LogisticRegression()
... )

>>> metric = metrics.Accuracy()

>>> evaluate.progressive_val_score(dataset, model, metric)
Accuracy: 88.88%
```

## Methods

???- note "clone"

    Return a fresh estimator with the same parameters.

    The clone has the same parameters but has not been updated with any data.  This works by looking at the parameters from the class signature. Each parameter is either  - recursively cloned if it's a River classes. - deep-copied via `copy.deepcopy` if not.  If the calling object is stochastic (i.e. it accepts a seed parameter) and has not been seeded, then the clone will not be idempotent. Indeed, this method's purpose if simply to return a new instance with the same input parameters.

    
???- note "learn_one"

    Update with a set of features `x`.

    A lot of transformers don't actually have to do anything during the `learn_one` step because they are stateless. For this reason the default behavior of this function is to do nothing. Transformers that however do something during the `learn_one` can override this method.

    **Parameters**

    - **x**     (*dict*)    
    - **kwargs**    
    
    **Returns**

    *Transformer*:     self
    
???- note "transform_one"

    Transform a set of features `x`.

    **Parameters**

    - **x**     (*dict*)    
    
    **Returns**

    *dict*:     The transformed values.
    
